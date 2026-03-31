# Airclap Landing Page — CRO 审计报告

*Date: 2026-03-31*
*URL: https://airclap.app*
*Page type: Product Homepage*
*Primary conversion: Download app*
*Traffic: Organic search, Product Hunt, direct*

---

## 当前评分：7.2/10（从 5.3 提升到 7.2）

你已经做了大量优化。Headline、Trust Strip、Problem/Solution、Testimonials 都很好。以下聚焦**还能提升的地方**。

---

## 页面结构扫描

| 区块 | 内容 | CRO 评分 | 问题 |
|------|------|----------|------|
| Nav | Logo + "Download Free" | 8/10 | ✅ 好 |
| Hero | PH badge + Headline + Sub + CTA + Image | 8/10 | ✅ "Drop files between any device. Instantly." 很好 |
| Trust Strip | 120+ / 4 / 5.0 / #1 / 44 | 8/10 | ✅ 有效 |
| Problem→Solution | 竞品痛点对比 | 9/10 | ✅ 最强的 section |
| Features (×5) | 图文交替展示 | 7/10 | ⚠️ 缺少中途 CTA |
| How It Works | 三步骤 | 7/10 | ⚠️ 紧跟 CTA 效果会更好 |
| Why Airclap | 6 张价值卡片 | 7/10 | ⚠️ 和 Features 有冗余 |
| Testimonials | 16+ 条多语言评价滚动 | 8/10 | ⚠️ 全是 5 星，缺来源标注 |
| Download | 4 平台 badge | 5/10 | ❌ 最弱的 section |
| Footer | Logo + copyright + 2 links | 4/10 | ❌ 太单薄 |

---

## Quick Wins — 立即可做

### 1. Download Section 加强（影响：高）

**当前问题：** "Get Airclap" + "Free download. No account required." + 4 个 badge。作为整个页面的终点转化区，太弱了。

**建议改为：**
```html
<h2>Get Airclap — it's free</h2>
<p>No account. No credit card. Works in 30 seconds.</p>

<!-- 在 badge 上方重复关键 trust signals -->
<div class="download__trust">
  ⭐ 5.0 App Store · 🏆 #1 on Product Hunt · 🌍 120+ countries
</div>

<!-- 4 platform badges -->
```

**为什么：** 用户决定下载的那一刻需要看到信任信号。现在 trust strip 在页面最顶部，用户滚到底部时早就忘了。

### 2. Features 后插入中途 CTA（影响：高）

**当前问题：** 从 Hero CTA 到 Download section 之间有 5 个 Feature + How It Works + Why Airclap + Testimonials，大约 4-5 屏的内容没有任何 CTA。

**建议在 "How It Works" 之后、"Why Airclap" 之前插入：**
```html
<section class="mid-cta">
  <a href="#download" class="btn btn--primary">Download Free</a>
  <span>Available on Mac, iOS, Windows & Android</span>
</section>
```

**为什么：** 部分用户在看完 How It Works 后已经被说服，但找不到下载按钮就继续滚。每个页面至少需要 2-3 个 CTA 触点。

### 3. Testimonials 标注来源（影响：中）

**当前问题：** 16 条评价全是 5 星，没有标注来源（App Store? Product Hunt? Twitter?）。对于信任度高的用户没问题，但对怀疑者看起来像假评价。

**建议：**
- 在 section 标题下加一行："From App Store, Product Hunt & our community"
- 至少有 1-2 条是 4 星评价（paradoxically increases credibility）
- 或在每条评价底部标注来源平台

### 4. "200% faster" 具体数据上页面（影响：中）

**当前问题：** App Store 描述里提到了 "200% faster"，但官网没有任何速度数据。"Maximum Speed" 卡片只说 "Transfers at the full speed your WiFi allows"——太模糊。

**建议在 "Why Airclap" 的 Speed 卡片中改为：**
```
200% Faster Than Alternatives
Transfer a 1GB file in under 30 seconds over WiFi 6. No cloud bottleneck.
```

---

## High-Impact Changes — 本周做

### 5. 添加 FAQ Section（影响：高）

**当前问题：** 没有 FAQ。用户的常见疑虑没有被 proactively 解答。

**建议添加在 Testimonials 之后、Download 之前：**

```
Q: Is Airclap really free?
A: Yes. Basic file transfer is completely free with no account needed.
   Pro unlocks unlimited files and advanced features for $0.99/month.

Q: How is this different from AirDrop?
A: AirDrop only works between Apple devices. Airclap works between ANY
   combination — Mac to Android, iPhone to Windows, anything.

Q: Is it safe? Where do my files go?
A: Files transfer directly between your devices over local WiFi.
   Nothing goes to any server. We collect zero data.

Q: Do both devices need the app?
A: Yes, install Airclap on both devices. They find each other
   automatically — no pairing or setup needed.

Q: How fast is it?
A: As fast as your WiFi allows. Most files arrive in seconds.
   We've measured 200%+ faster than similar tools.
```

**为什么：** FAQ 做三件事——(1) 解答购买犹豫 (2) SEO 长尾关键词 (3) 可被 AI 搜索引擎引用。

### 6. Hero CTA 平台自动检测优化（影响：中高）

**当前状态：** 你已经有 `id="heroBtn"` 和 `id="heroBtnText"` 的 JS 逻辑。

**确认一下：** CTA 按钮文案是否根据访客系统自动变化？
- Mac 用户看到 "Download Free for Mac"
- Windows 用户看到 "Download Free for Windows"
- iPhone 用户看到 "Get on App Store"
- Android 用户看到 "Get on Google Play"

如果已实现 → ✅ 好。如果没有 → 这是高优先级改动。

### 7. 精简页面结构——合并 Features 和 Why Airclap（影响：中）

**当前问题：** Features（5 个图文 section）和 Why Airclap（6 张卡片）有内容重复：
- Feature "Cross-Platform" ≈ Why "Every Platform"
- Feature "Dead Simple" ≈ Why 的整体 messaging
- Feature "Any Format" ≈ Why "Zero Compression"

**建议：** 保留 Features 的图文展示（更有说服力），把 Why Airclap 中不重复的亮点（No Internet、Maximum Speed、Private by Design）**融入 Features section**，然后删除 Why Airclap section。

**为什么：** 更短的页面 = 更多用户到达 Download section。

---

## Test Ideas — A/B 测试假设

### T1: Hero Headline 测试
- **Control:** "Drop files between any device. Instantly."
- **Variant A:** "The AirDrop that works on everything."
- **Variant B:** "File transfer that just works — across every device you own."

**假设：** Variant A 更大胆、更有差异化，但可能引起 Apple 用户的误解。Variant B 更安全但可能更具共鸣。

### T2: Download Section 布局
- **Control:** 4 个并排 badge
- **Variant:** 智能检测后只显示 1 个主 badge（当前平台），其他 3 个缩小为文字链接

### T3: 页面长度
- **Control:** 当前完整页面（Features + How It Works + Why Airclap + Testimonials）
- **Variant:** 精简版（Features + Testimonials only）

---

## 不需要改的地方

这些你已经做得很好了：

- ✅ **Headline** — "Drop files between any device. Instantly." 清晰、具体、有节奏感
- ✅ **Trust Strip** — 数据选得好，120+/5.0/#1 都是强信号
- ✅ **Problem → Solution** — "AirDrop is Apple-only. Nearby Share is Android-only." 精准击中痛点
- ✅ **Hero hint** — "Free · No account needed · Works in 30 seconds" 降低门槛
- ✅ **Product Hunt badge** — 位置好，设计好
- ✅ **Testimonials** — 多语言、真实感强、数量充足
- ✅ **视觉设计** — 暗色主题、accent green、dot grid 背景——非常精致
- ✅ **i18n** — 44 语言支持，国际化做得非常到位

---

## 优先级排序

| # | 改动 | 影响 | 工时 | 建议 |
|---|------|------|------|------|
| 1 | Download section 加 trust signals | 高 | 15 分钟 | 立即做 |
| 2 | Features 后插入中途 CTA | 高 | 10 分钟 | 立即做 |
| 3 | 添加 FAQ section | 高 | 30 分钟 | 本周做 |
| 4 | Speed 卡片加具体数据 | 中 | 5 分钟 | 立即做 |
| 5 | Testimonials 标注来源 | 中 | 10 分钟 | 本周做 |
| 6 | 确认 Hero CTA 平台检测 | 中高 | 取决于现状 | 检查 |
| 7 | 精简合并 Features/Why | 中 | 1 小时 | 下周做 |

---

*报告由 marketingskills/page-cro 生成*
