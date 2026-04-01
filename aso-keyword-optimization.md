# Airclap — ASO 关键词优化报告

*Date: 2026-03-31*
*App: Airclap (ID: 6467128147)*
*Framework: marketingskills/aso-keyword*

---

## Step 1: 诊断分析（en-US）

### 当前三段式布局

| 字段 | 当前内容 | 字符数 |
|------|---------|--------|
| **Title** | Airclap - Fast File Transfer | 28/30 |
| **Subtitle** | Share Across Any Device Free | 27/30 |
| **Keywords** | airdrop,wireless,send,photo,video,lan,wifi,nearby,offline,bluetooth,pc,mac,android,document,music | 95/100 |

### 已索引词（Title + Subtitle，不可重复）

Title 自动索引：`airclap`, `fast`, `file`, `transfer`
Subtitle 自动索引：`share`, `across`, `any`, `device`, `free`
系统自动索引：`app`, `iphone`, `ipad`, `apple`, `ios`, `utilities`

### 关键词逐条诊断

| 关键词 | 字符 | 相关性 | 搜索量 | 问题 | 判定 |
|--------|------|--------|--------|------|------|
| airdrop | 7 | ★★★★★ | 极高 | 竞品截流词，"airdrop for windows"搜索量大 | ✅ 保留 |
| wireless | 8 | ★★★☆☆ | 中 | **与 wifi 语义重复**，8字符性价比低 | ❌ 删除 |
| send | 4 | ★★★★☆ | 高 | "send file to pc" 高频搜索 | ✅ 保留 |
| photo | 5 | ★★★★☆ | 高 | "send photo" 高频搜索 | ✅ 保留 |
| video | 5 | ★★★★☆ | 高 | "send video" 高频搜索 | ✅ 保留 |
| lan | 3 | ★★★☆☆ | 中低 | 便宜（3字符），"lan transfer" 相关 | ✅ 保留 |
| wifi | 4 | ★★★★☆ | 高 | "wifi file transfer" 高频 | ✅ 保留 |
| nearby | 6 | ★★★★☆ | 中高 | nearby + share(subtitle) = "nearby share"（Android 竞品名） | ✅ 保留 |
| offline | 7 | ★★★★☆ | 中高 | "offline file transfer" 差异化搜索 | ✅ 保留 |
| bluetooth | 9 | ★★★☆☆ | 中 | **9字符太贵**，Bluetooth 只用于发现不用于传输 | ❌ 删除 |
| pc | 2 | ★★★★☆ | 高 | "transfer to pc" 高频，仅2字符 | ✅ 保留 |
| mac | 3 | ★★★★☆ | 高 | "transfer to mac" 高频，仅3字符 | ✅ 保留 |
| android | 7 | ★★★★☆ | 高 | "android file transfer" 高频 | ✅ 保留 |
| document | 8 | ★★★☆☆ | 中 | **8字符性价比低**，非核心使用场景 | ❌ 删除 |
| music | 5 | ★★☆☆☆ | 低 | **与产品核心功能不符**，Airclap 不是音乐应用 | ❌ 删除 |

### 删除词释放空间

| 删除词 | 释放字符（含逗号） |
|--------|-------------------|
| wireless | 9 |
| bluetooth | 10 |
| document | 9 |
| music | 6 |
| **总计** | **34 字符** |

### 缺失的高价值词

| 候选词 | 字符 | 可组成的搜索短语 | 优先级 |
|--------|------|-----------------|--------|
| **local** | 5 | "local file transfer", "local network" | ★★★★★ |
| **cross** | 5 | "cross device" (+ subtitle), "cross platform" | ★★★★★ |
| **platform** | 8 | "cross platform transfer" | ★★★★☆ |
| **text** | 4 | "text transfer", "text share" (clipboard 功能) | ★★★★☆ |
| **drop** | 4 | "drag drop", 强化 "airdrop" 信号 | ★★★★☆ |
| **drag** | 4 | "drag and drop file transfer" | ★★★☆☆ |
| cable | 5 | "cable free transfer" (+ subtitle "free") | ★★★☆☆ |
| folder | 6 | "transfer folder" (Pro 功能) | ★★★☆☆ |

---

## Step 2: 优化后的 en-US 关键词

### 最终关键词字符串

```
airdrop,send,photo,video,lan,wifi,nearby,offline,pc,mac,android,local,cross,platform,text,drop,drag
```

**字符数：99/100**

### 验证

| 规则 | 状态 |
|------|------|
| R1: 无重复词（含跨 Title/Subtitle） | ✅ |
| R2: 零空格 | ✅ |
| R3: 全部单数 | ✅ |
| R4: 无停用词 | ✅ |
| R5: 无自动索引词 | ✅ |
| R6: 简化用词 | ✅ |
| R7: 接近 100 字符 | ✅ 99/100 |
| R8: 核心词前置 | ✅ airdrop 居首 |
| R9: 与 Title/Subtitle 零重叠 | ✅ |
| R10: 无特殊字符 | ✅ |

### 新增搜索短语覆盖

优化后 Apple 可自动组合的高价值搜索短语：

| 搜索短语 | 词来源 | 之前能否匹配 |
|----------|--------|-------------|
| "cross platform file transfer" | cross(kw) + platform(kw) + file(title) + transfer(title) | ❌ → ✅ |
| "cross device transfer" | cross(kw) + device(subtitle) + transfer(title) | ❌ → ✅ |
| "local file transfer" | local(kw) + file(title) + transfer(title) | ❌ → ✅ |
| "drag drop file" | drag(kw) + drop(kw) + file(title) | ❌ → ✅ |
| "text transfer" | text(kw) + transfer(title) | ❌ → ✅ |
| "airdrop android" | airdrop(kw) + android(kw) | ✅ 保持 |
| "wifi file transfer" | wifi(kw) + file(title) + transfer(title) | ✅ 保持 |
| "nearby share" | nearby(kw) + share(subtitle) | ✅ 保持 |
| "send photo to pc" | send(kw) + photo(kw) + pc(kw) | ✅ 保持 |
| "offline transfer" | offline(kw) + transfer(title) | ✅ 保持 |

**新增 5 个高价值搜索短语，同时保留所有原有有效组合。**

---

## Step 3: zh-Hans 关键词优化

### 当前状态

| 字段 | 内容 |
|------|------|
| **Title** | Airclap - 文件传输与快传 |
| **Subtitle** | WiFi极速发送，无需互联网 |
| **Keywords** | 无线,发送,照片,视频,文档,离线,近距离,拖拽,局域网,蓝牙,高速,PC,安卓,音乐,跨平台,隔空投送,面对面,分享,同屏 |

**当前字符数：62/100 — 浪费 38 个字符！**

### 诊断

| 问题 | 关键词 | 说明 |
|------|--------|------|
| ❌ 与 Subtitle 重复 | **发送** | Subtitle 含"发送"，浪费 3 字符 |
| ❌ 不相关 | **音乐** | 非核心功能 |
| ❌ 低相关 | **同屏** | 不是文件传输场景 |
| ⚠️ 严重浪费 | — | 62/100，38 字符未使用 |

### 优化后 zh-Hans 关键词

```
无线,照片,视频,文档,离线,近距离,拖拽,局域网,蓝牙,高速,PC,安卓,跨平台,隔空投送,面对面,分享,互传,闪传,手机,电脑,大文件,文本,剪贴板,Windows,秒传,Mac,传图,批量,本地
```

**字符数：100/100** ✅

### 新增词说明

| 新增词 | 字符 | 搜索意图 |
|--------|------|---------|
| **互传** | 2 | "手机互传"、"文件互传" — 中文用户高频搜索词 |
| **闪传** | 2 | 竞品"闪传"的品牌词截流 + 通用速度词 |
| **手机** | 2 | "手机传电脑"、"手机传文件" — 极高搜索量 |
| **电脑** | 2 | "电脑传手机"、"传文件到电脑" — 极高搜索量 |
| **大文件** | 3 | "大文件传输" — 差异化搜索（Airclap 无大小限制）|
| **文本** | 2 | "文本传输"、"文本分享" — Airclap 支持文本 |
| **剪贴板** | 3 | "剪贴板同步" — 高级功能词 |
| **Windows** | 7 | "Windows 传文件到 iPhone" — 跨平台搜索 |
| **秒传** | 2 | "秒传文件" — 速度相关高搜索量 |
| **Mac** | 3 | "Mac 传文件到 Android" — 跨平台搜索 |
| **传图** | 2 | "传图到电脑" — 图片传输简称 |
| **批量** | 2 | "批量传输" — Pro 功能词 |
| **本地** | 2 | "本地传输"、"本地网络" — 差异化关键词 |

---

## Step 4: 其他重点语言优化

### de-DE（德语）

**当前：** `senden,übertragen,drahtlos,foto,video,wlan,lokal,bluetooth,dokument,ordner,pc,offline,musik` (91/100)

**问题：** 浪费 9 字符；"musik" 不相关；"drahtlos" 与 "wlan" 重复

**优化后：**
```
senden,foto,video,wlan,lokal,dokument,ordner,pc,offline,android,mac,datei,teilen,kabellos,text
```
**字符数：94/100** — 删除 "übertragen"(title 已含)/"drahtlos"(与 wlan 重复)/"musik"(不相关)/"bluetooth"(9字符太贵)，增加 "android", "mac", "datei", "teilen", "kabellos", "text"

### fr-FR（法语）

**当前：** `envoyer,sans fil,photo,vidéo,wifi,local,bluetooth,document,dossier,appareil,pc,musique,offline` (94/100)

**优化后：**
```
envoyer,photo,vidéo,wifi,local,document,dossier,appareil,pc,offline,android,mac,glisser,partage,lan
```
**字符数：99/100** — 删除 "sans fil"(与 wifi 重复)/"musique"(不相关)/"bluetooth"(字符太贵)，增加 "android", "mac", "glisser"(drag), "partage"(share), "lan"

### es-ES（西语）

**当前：** `enviar,compartir,inalámbrico,foto,video,wifi,local,bluetooth,documento,carpeta,pc,música,offline` (96/100)

**优化后：**
```
enviar,compartir,foto,video,wifi,local,documento,pc,offline,android,mac,red,archivo,texto,gratis,lan
```
**字符数：100/100** — 删除 "inalámbrico"(与 wifi 重复)/"música"(不相关)/"bluetooth"/"carpeta"(低优先级)，增加 "android", "mac", "red"(network), "archivo"(file), "texto"(text), "gratis"(free), "lan"

### ja（日语）

**当前：** `ワイヤレス,送信,写真,動画,ドキュメント,オフライン,近距離,ドラッグ,ドロップ,LAN,ブルートゥース,高速,PC,マック,アンドロイド,音楽,クロスプラットフォーム,無線` (95/100)

**问题：** "ワイヤレス" 和 "無線" 重复（都是 "wireless"）；"音楽" 不相关

**优化后：**
```
送信,写真,動画,ドキュメント,オフライン,近距離,ドラッグ,ドロップ,LAN,高速,PC,マック,アンドロイド,クロスプラットフォーム,無線,テキスト,ローカル,フォルダ,Windows
```
**字符数：94/100** — 删除 "ワイヤレス"(与無線重复)/"音楽"(不相关)/"ブルートゥース"(昂贵)，增加 "テキスト", "ローカル", "フォルダ", "Windows"

### ko（韩语）

**当前：** `무선,보내기,사진,동영상,문서,오프라인,근거리,드래그,드롭,LAN,블루투스,고속,PC,맥,안드로이드,음악,크로스플랫폼,로컬` (91/100)

**优化后：**
```
무선,보내기,사진,동영상,문서,오프라인,근거리,드래그,드롭,LAN,고속,PC,맥,안드로이드,크로스플랫폼,로컬,텍스트,폴더,Windows,에어드롭,블루투스,와이파이,대용량,클립보드
```
**字符数：99/100** — 删除 "음악"(不相关)，增加 "텍스트"(text), "폴더"(folder), "Windows", "에어드롭"(AirDrop), "와이파이"(WiFi), "대용량"(large file), "클립보드"(clipboard)

---

## Step 5: 跨本地化策略（US 市场进阶）

### 原理

美国 App Store 同时索引 **en-US + es-MX（西班牙语-墨西哥）** 的关键词字段。这意味着你可以在 es-MX 的 keyword field 中放入**英文溢出关键词**，有效获得 200 个字符的美国市场关键词空间。

### 实施方法

1. 在 App Store Connect 中单独创建 **Spanish (Mexico)** 本地化（与 es-ES 分开）
2. es-MX 的 Title 和 Subtitle 保持西班牙语（给墨西哥用户看）
3. es-MX 的 **keyword field 填英文溢出词**

### 建议 es-MX 关键词字段（英文溢出词）

```
bluetooth,document,wireless,folder,cable,clipboard,network,quick,image,data,usb,private,secure,fast,sync
```

这些是 en-US 放不下但有价值的词，通过 es-MX 渠道为美国市场索引。

**注意：** 这个技巧广泛使用且不违反 Apple 政策，但需要单独维护一个 es-MX locale。

---

## 30-30-100 全局建议总览

### en-US

| 字段 | 建议 | 字符数 |
|------|------|--------|
| **Title** | Airclap - Fast File Transfer | 28/30（保持不变，"File Transfer" 是 #1 搜索词） |
| **Subtitle** | Share Across Any Device Free | 27/30（保持不变，已有合理关键词覆盖） |
| **Keywords** | `airdrop,send,photo,video,lan,wifi,nearby,offline,pc,mac,android,local,cross,platform,text,drop,drag` | 99/100 |

### 变更摘要

| 类型 | 数量 | 详情 |
|------|------|------|
| **删除** | 4 词 | wireless, bluetooth, document, music |
| **新增** | 5 词 | local, cross, platform, text, drop, drag |
| **新增可匹配短语** | 5 个 | cross platform transfer, local file transfer, cross device transfer, drag drop file, text transfer |
| **字符利用率** | 95→99 | +4 字符 |
| **关键词数量** | 15→17 | +2 个 |

---

## 实施注意事项

1. **不要一次改太多** — 如果你想 A/B 验证效果，先只改关键词字段，观察 2-3 周排名变化后再动 Title/Subtitle
2. **关键词效果滞后** — 新关键词上线后需要 24-72 小时被 Apple 索引，2-4 周才能看到排名稳定
3. **定期复审** — 每 3-4 周检查关键词排名，根据数据调整
4. **评分量是前提** — 关键词优化的效果在评分量 > 50 后才会显著体现

---

*报告由 marketingskills/aso-keyword 生成*
