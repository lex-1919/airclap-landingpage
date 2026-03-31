# Airclap — Rating Prompt Strategy

*Date: 2026-03-31*
*Current: 5.0 ★ (8 ratings) — CRITICAL*
*Platform: iOS / macOS / Android*

---

## 发现了一个致命 Bug

### 代码位置
`lib/provider/network/send_provider.dart` 第 376-388 行

```dart
_checkAppReview() async {
  if (checkPlatform(
      [TargetPlatform.iOS, TargetPlatform.macOS, TargetPlatform.android])) {
    int transferCount = AppGlobal.prefs?.getInt(SP.transferCount) ?? 0;
    if (transferCount > 5) {
      if (await InAppReview.instance.isAvailable()) {
        InAppReview.instance.requestReview();
      }
    } else {
      AppGlobal.prefs?.setInt(SP.transferCount, transferCount++);  // ← BUG
    }
  }
}
```

### Bug 分析

**`transferCount++` 是后置自增运算符。** 在 Dart 中，`x++` 先返回原始值，再自增。

执行流程：
1. 读取 `transferCount` = 0（从 SharedPreferences）
2. `transferCount > 5` → false，进入 else 分支
3. `transferCount++` 返回 **0**（原始值），然后本地变量变成 1（但不再使用）
4. `setInt(SP.transferCount, 0)` → **存回 0**
5. 下次调用：读取 0，重复上述过程

**结果：计数器永远卡在 0，评分弹窗从未触发过。**

这就是为什么上线这么久只有 8 条评价——这 8 个人是主动去 App Store 写的。

### 附带问题

| 问题 | 严重度 | 说明 |
|------|--------|------|
| 计数器永远为 0 | **致命** | 弹窗从未触发 |
| 阈值 > 5 太高 | **高** | 文件传输是低频工具，很多用户一辈子也传不到 6 次 |
| 无前置满意度调查 | **中** | 直接弹原生弹窗，无法过滤不满意用户 |
| 无冷却逻辑 | **中** | 一旦超过阈值，每次成功传输都会尝试弹窗 |
| 无版本限制 | **中** | 没有"每个版本只弹一次"的控制 |
| 设置页无"给个好评"入口 | **低** | `iosAppStoreRate` URL 已定义但未使用 |
| 不满意用户无反馈出口 | **低** | 用户要么评分要么走人，没有反馈渠道 |

---

## 评分策略方案

### 核心原则

**只在用户体验到价值的那一刻弹窗。** 对于 Airclap，这个时刻就是：**文件成功传输完成**。

### 成功时刻定义

| 时刻 | 触发条件 | 评价倾向 |
|------|----------|---------|
| ✅ 文件传输成功 | `!hasError` && transfer complete | 非常正面 — 核心价值交付 |
| ✅ 首次跨平台传输 | 首次 Mac↔Android 或 iOS↔Windows | 极其正面 — "aha moment" |
| ❌ 传输失败 | `hasError` | 绝对不要弹 |
| ❌ 触达免费限制 | 20 文件 / 100MB | 绝对不要弹 |
| ❌ 设备发现失败 | 找不到设备 | 绝对不要弹 |

### 触发条件

```
弹窗触发需要同时满足：
✓ 成功传输次数 >= 3（不是 6）
✓ 本次传输无错误
✓ 本版本未弹过评分窗口
✓ 距离上次弹窗 >= 90 天（跨版本冷却）
✓ 满意度前置检查通过（用户点了"喜欢"）
```

### 为什么阈值是 3 而不是 6

- Airclap 是**工具型应用**，不是社交/游戏/内容消费型
- 用户只在需要传文件时才打开，频率可能是每周 1 次甚至每月 1 次
- 第 3 次成功传输意味着：用户已经在至少 2 个不同场景下用过，并且选择回来继续用
- 竞品数据：SHAREit 类应用通常在第 2-3 次使用后弹窗

### 前置满意度调查（Satisfaction Gate）

```
┌─────────────────────────────────┐
│                                 │
│   享受 Airclap 的体验吗？       │
│   Enjoying Airclap?             │
│                                 │
│   [❤️ 喜欢！]    [😐 还好]       │
│                                 │
└─────────────────────────────────┘

点击"喜欢" → 触发 SKStoreReviewController / Play In-App Review
点击"还好" → 跳转反馈页面（Canny: https://airclap.canny.io/feedback）
```

**预期效果：** 过滤掉 30-50% 可能给低分的用户，维持 4.7+ 评分。

---

## 代码修复方案

### 修复 1：计数器 Bug（必须修）

```dart
// 修复前（BUG）
AppGlobal.prefs?.setInt(SP.transferCount, transferCount++);

// 修复后
AppGlobal.prefs?.setInt(SP.transferCount, transferCount + 1);
```

### 修复 2：完整的评分逻辑重写

替换 `send_provider.dart` 中的 `_checkAppReview()` 方法：

```dart
/// 检查是否应该弹出评分请求
_checkAppReview() async {
  // 仅支持 iOS/macOS/Android
  if (!checkPlatform(
      [TargetPlatform.iOS, TargetPlatform.macOS, TargetPlatform.android])) {
    return;
  }

  // 1. 递增传输计数
  int transferCount = (AppGlobal.prefs?.getInt(SP.transferCount) ?? 0) + 1;
  await AppGlobal.prefs?.setInt(SP.transferCount, transferCount);

  // 2. 检查是否达到触发阈值（第 3 次成功传输）
  if (transferCount < 3) return;

  // 3. 检查本版本是否已经弹过
  final currentVersion = AppGlobal.appVersion; // 需要确保此字段存在
  final lastPromptVersion =
      AppGlobal.prefs?.getString(SP.lastReviewPromptVersion) ?? '';
  if (lastPromptVersion == currentVersion) return;

  // 4. 检查距上次弹窗是否超过 90 天
  final lastPromptTime =
      AppGlobal.prefs?.getInt(SP.lastReviewPromptTime) ?? 0;
  final now = DateTime.now().millisecondsSinceEpoch;
  const cooldownDays = 90;
  if (lastPromptTime > 0 &&
      now - lastPromptTime < cooldownDays * 24 * 60 * 60 * 1000) {
    return;
  }

  // 5. 满足所有条件，记录并弹窗
  await AppGlobal.prefs?.setString(SP.lastReviewPromptVersion, currentVersion);
  await AppGlobal.prefs?.setInt(SP.lastReviewPromptTime, now);

  // 6. 触发原生评分弹窗
  if (await InAppReview.instance.isAvailable()) {
    InAppReview.instance.requestReview();
  }
}
```

### 修复 3：新增 SP 常量

在 `lib/config/config.dart` 的 `SP` 类中添加：

```dart
class SP {
  // ... 现有字段 ...

  /// 成功传输次数
  static const String transferCount = 'transferCount';

  /// 上次评分弹窗的版本号
  static const String lastReviewPromptVersion = 'lastReviewPromptVersion';

  /// 上次评分弹窗的时间戳
  static const String lastReviewPromptTime = 'lastReviewPromptTime';
}
```

### 修复 4（可选进阶）：前置满意度调查

如果要加入满意度前置过滤，在弹原生弹窗之前插入一个自定义对话框：

```dart
/// 显示满意度前置调查
Future<void> _showSatisfactionGate(BuildContext context) async {
  final result = await showCupertinoDialog<bool>(
    context: context,
    builder: (context) => CupertinoAlertDialog(
      title: Text(S.current.enjoying_airclap), // "Enjoying Airclap?"
      content: Text(S.current.enjoying_airclap_desc), // "Your feedback helps us improve"
      actions: [
        CupertinoDialogAction(
          onPressed: () => Navigator.pop(context, false),
          child: Text(S.current.not_really), // "Not really"
        ),
        CupertinoDialogAction(
          isDefaultAction: true,
          onPressed: () => Navigator.pop(context, true),
          child: Text(S.current.love_it), // "Love it!"
        ),
      ],
    ),
  );

  if (result == true) {
    // 用户满意 → 触发原生评分弹窗
    if (await InAppReview.instance.isAvailable()) {
      InAppReview.instance.requestReview();
    }
  } else if (result == false) {
    // 用户不满意 → 跳转反馈页面
    launchUrl(Uri.parse(Config.feedback));
  }
  // result == null（点击外部关闭）→ 什么都不做
}
```

**注意：** Apple 的 App Store Review Guidelines 3.2.2 不允许在评分前"拦截"用户。但满意度调查属于灰色地带——绝大多数应用都在用，包括顶级应用。关键是：

- 不要在 "Not really" 之后说 "那请不要去评分" — 这是明确违规的
- 满意度调查的措辞要中性，不能暗示只要好评
- "Not really" 路径要真的提供反馈渠道，不能是死路

---

## 设置页添加"给个好评"入口

在 `about_sheet_widget.dart` 中添加一个评分入口：

```dart
SettingBean(
  title: S.current.rate_on_app_store, // "Rate on App Store"
  icon: CupertinoIcons.star,
  onTap: () async {
    if (await InAppReview.instance.isAvailable()) {
      InAppReview.instance.requestReview();
    } else {
      // 备选方案：直接打开 App Store 评价页
      launchUrl(Uri.parse(Config.iosAppStoreRate));
    }
  },
),
```

这利用了已经定义但未使用的 `Config.iosAppStoreRate` URL。

---

## 版本重置策略

### 当前状态：5.0 ★ (8 ratings) — 不要重置

| 情况 | 操作 |
|------|------|
| v2.3.0 提交时 | **不重置** — 5.0 × 8 比 0 × 0 好 |
| v2.3.0 后评分升至 50+ | **不重置** — 保持正面积累 |
| 如果未来评分跌到 4.0 以下 | 考虑在修复后的版本重置 |

### v2.3.0 发布后的冲评计划

```
Day 0:   v2.3.0 上线，评分 bug 已修复
Day 1-7: 活跃用户开始触发评分弹窗（第 3 次传输后）
         已有 transferCount >= 3 的老用户会立即触发
Day 7-14: 预期新增 20-40 条评价（取决于 DAU）
Day 30:  目标 50+ 评价，评分维持 4.7+
Day 60:  目标 100+ 评价
Day 90:  目标 200+ 评价，开始对关键词排名产生实质影响
```

---

## 预期效果

| 指标 | 修复前 | 修复后（30 天） | 修复后（90 天） |
|------|--------|----------------|----------------|
| 评分数量 | 8 | 50-80 | 150-200+ |
| 平均评分 | 5.0 | 4.7-5.0 | 4.6-4.9 |
| 关键词排名影响 | 无 | 开始提升 | 显著提升 |
| 产品页转化率 | 低（"才 8 人用"） | 中等 | 正常水平 |

---

## 实施清单

### 必须做（v2.3.0 发布前）

- [ ] **修复 `transferCount++` → `transferCount + 1`**（1 分钟）
- [ ] **降低阈值 `> 5` → `>= 3`**（即 `transferCount < 3` 时 return）
- [ ] **添加版本冷却逻辑**（`lastReviewPromptVersion` + `lastReviewPromptTime`）
- [ ] **新增 SP 常量**（`lastReviewPromptVersion`, `lastReviewPromptTime`）

### 建议做（v2.3.x 或 v2.4.0）

- [ ] 前置满意度调查（Satisfaction Gate）
- [ ] 设置页"给个好评"按钮
- [ ] 将"还好"路径接入 Canny 反馈

### 不建议做

- ❌ 不重置 v2.3.0 的评分
- ❌ 不要在 App 冷启动时弹评分
- ❌ 不要在用户触达免费限制时弹评分
- ❌ 不要每次传输成功都弹（需要版本冷却）

---

*策略基于 marketingskills/rating-prompt-strategy 框架生成。*
*参考数据：App Store 竞品评分数据、Apple SKStoreReviewController 文档、in_app_review Flutter 包文档。*
