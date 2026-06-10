<div align="center">

# Yescan Skills

<h3>强大的文档 AI 能力，为 OpenClaw Agent 而生</h3>

<h4>OCR 文字识别 | 文件扫描增强 | 图片转 Office</h4>

[English](./README.md) | [中文](./README_cn.md)

<p>
<img alt="License" src="https://img.shields.io/badge/license-Apache--2.0-blue.svg">
<img alt="Python" src="https://img.shields.io/badge/python-3.9%2B-green.svg">
<img alt="OpenClaw" src="https://img.shields.io/badge/OpenClaw-Compatible-orange.svg">
<img alt="Platform" src="https://img.shields.io/badge/platform-macOS%20%7C%20Linux%20%7C%20Windows-lightgrey.svg">
<img alt="Scenes" src="https://img.shields.io/badge/scenes-30%2B-brightgreen.svg">
<img alt="Stars" src="https://img.shields.io/github/stars/YOUR_ORG/openclaw-yescan-skills?style=social">
</p>

---

YesCan OpenClaw Skills 将 [夸克扫描王 (YesCan)](https://scan.quark.cn/business) 的文档 AI 能力封装为三个 [OpenClaw](https://github.com/anthropics/openclaw) Agent 技能。

只需一个 `pip install` 和一个 API Key，你的 OpenClaw Agent 即可获得 **30+ 文档处理场景**的能力——包括手写识别、表格 OCR、证件扫描、图像增强、去水印以及图片转 Word/Excel/PDF。

</div>

---

## 目录

- [核心特性](#核心特性)
- [支持场景](#支持场景)
  - [OCR 文字识别](#-ocr-文字识别)
  - [文件扫描增强](#-文件扫描增强)
  - [图片转 Office](#-图片转-office)
- [快速开始](#快速开始)
  - [环境要求](#环境要求)
  - [安装](#安装)
  - [配置](#配置)
- [使用示例](#使用示例)
  - [OCR 示例](#ocr-示例)
  - [扫描示例](#扫描示例)
  - [转换示例](#转换示例)
- [架构设计](#架构设计)
- [API 参考](#api-参考)
- [错误码说明](#错误码说明)
- [使用限制](#使用限制)
- [常见问题](#常见问题)
- [贡献指南](#贡献指南)
- [开源协议](#开源协议)
- [致谢](#致谢)

---

## 核心特性

> 三大核心能力，统一交互接口，零配置开销。

<div align="center">

| | **OCR 文字识别** | **文件扫描增强** | **图片转 Office** |
|---|:---:|:---:|:---:|
| **场景数** | 17 个专业模型 | 13 种增强模式 | 3 种输出格式 |
| **输入方式** | URL / 文件 / Base64 | URL / 文件 / Base64 | URL / 文件 / Base64 |
| **输出格式** | 结构化 JSON | 增强后图片 | Word / Excel / PDF |
| **语言支持** | 中文 + 英文 | — | 中文 + 英文 |

</div>

**为什么选择 YesCan OpenClaw Skills？**

- **Agent 原生**：从底层为 OpenClaw 的技能执行模型设计——意图匹配、场景路由、结构化 JSON 输出，开箱即用。
- **30+ 专业场景**：每个场景使用针对特定文档类型微调的模型，精度远超通用 OCR 方案。
- **一个 Key 全搞定**：一个 API Key 解锁全部三大能力和 30+ 场景。
- **隐私安全**：图片在夸克服务器上处理，不会永久保存；本地临时文件路径清晰可控。
- **中英双语**：完整支持中英文档处理，场景描述同时提供中英文版本。

---

## 支持场景

### 🔍 OCR 文字识别

OCR 技能覆盖 17 个专业识别场景，从手写字迹到发票到医疗报告。

| # | 场景名称 | 场景标识 | 关键词 |
|---|---------|---------|-------|
| 1 | 手写文档识别 | `handwritten-ocr` | 手写、笔迹、潦草字迹 |
| 2 | 表格识别 | `table-ocr` | 表格、报表、Excel |
| 3 | 身份证识别 | `idcard-ocr` | 身份证、居民身份证 |
| 4 | 社保卡识别 | `social-security-card-ocr` | 社保卡、医保卡 |
| 5 | 港澳通行证识别 | `travel-permit-ocr` | 港澳通行证、港澳台通行证 |
| 6 | 学位证识别 | `degree-certificate-ocr` | 学位证、学位证书 |
| 7 | 增值税发票识别 | `vat-invoice-ocr` | 增值税发票、发票 |
| 8 | 火车票识别 | `train-ticket-ocr` | 火车票、车票 |
| 9 | 公式识别 | `formula-ocr` | 数学公式、LaTeX、化学方程式 |
| 10 | 题目识别 | `question-ocr` | 题目、考题、习题 |
| 11 | 驾驶证识别 | `driver-license-ocr` | 驾驶证、驾照 |
| 12 | 行驶证识别 | `vehicle-license-ocr` | 行驶证、车辆 |
| 13 | 英文发票识别 | `commercial-invoice-ocr` | 英文发票、商业发票 |
| 14 | 医疗报告单识别 | `medical-report-ocr` | 化验单、医疗报告、检验 |
| 15 | 营业执照识别 | `business-license-ocr` | 营业执照、工商 |
| 16 | 商品图片识别 | `product-image-ocr` | 商品、产品、品牌 |
| 17 | 通用文字提取 | `general-ocr` | 提取文字、转文字（兜底） |

> 场景按优先级从上到下匹配，命中第一个即停止。无法匹配时，使用 `general-ocr` 兜底。
>
> **注意：** `handwritten-ocr` 标识同时出现在 OCR 和扫描技能中。OCR 技能返回结构化文本（JSON），扫描技能返回增强后的图片。Agent 会根据用户意图（提取文字 vs 增强图片）自动选择正确的技能。

### 📷 文件扫描增强

扫描技能提供 13 种图像增强和文档处理模式。

| # | 场景名称 | 场景标识 | 典型用途 |
|---|---------|---------|---------|
| 1 | 手写文档识别 | `handwritten-ocr` | 手写笔记转文字 |
| 2 | 考试增强 | `exam-enhance` | 试卷/学习资料高清化 |
| 3 | 画质增强 | `image-hd-enhance` | 模糊/低质量图片增强 |
| 4 | 证件票据增强 | `certificate-enhance` | 证件/票据清晰度优化 |
| 5 | 图像去手写 | `remove-handwriting` | 去除手写笔迹，保留印刷体 |
| 6 | 图像去水印 | `remove-watermark` | 精准去除水印文字和 Logo |
| 7 | 图像去阴影 | `remove-shadow` | 修复光照和阴影问题 |
| 8 | 图像去屏纹 | `remove-screen-pattern` | 消除屏幕翻拍的摩尔纹 |
| 9 | 文档去底色 | `remove-background-color` | 一键转为白底黑字 |
| 10 | 图像裁剪矫正 | `image-crop-rectify` | 自动矫正透视变形并裁剪 |
| 11 | 素描速写 | `sketch-drawing` | 照片转铅笔素描风格 |
| 12 | 提取线稿 | `extract-lineart` | 提取干净的线条图 |
| 13 | 扫描文件 | `scan-document` | 通用文档优化 |

### 📄 图片转 Office

转换技能将图片转化为可编辑的 Office 文档。

| # | 场景名称 | 场景标识 | 输出格式 |
|---|---------|---------|---------|
| 1 | 图片转 Excel | `image-to-excel` | `.xlsx` — 表格、数据、报表 |
| 2 | 图片转 Word | `image-to-word` | `.docx` — 文档、合同、文章 |
| 3 | 图片转 PDF | `image-to-pdf` | `.pdf` — 笔记、存档、报告 |

> 当目标格式不明确时，Agent 会主动询问用户选择 Word、Excel 还是 PDF。

---

## 快速开始

### 环境要求

- **Python** 3.9 或更高版本
- **OpenClaw** 已安装并配置完成（[安装指南](https://github.com/anthropics/openclaw#getting-started)）
- 一个 **夸克扫描王 API Key**（从 [scan.quark.cn/business](https://scan.quark.cn/business) 获取）

### 安装

**方式一：通过 OpenClaw CLI 安装（推荐）**

```bash
# 一键安装全部三个技能
openclaw skill install yescan-ocr-universal
openclaw skill install yescan-scan-universal
openclaw skill install yescan-transoffice-universal
```

**方式二：手动安装**

```bash
# 克隆本仓库
git clone https://github.com/YOUR_ORG/openclaw-yescan-skills.git
cd openclaw-yescan-skills

# 复制技能到 OpenClaw 技能目录
cp -r skills/yescan-ocr-universal ~/.openclaw/skills/
cp -r skills/yescan-scan-universal ~/.openclaw/skills/
cp -r skills/yescan-transoffice-universal ~/.openclaw/skills/

# 安装 Python 依赖
pip install -r requirements.txt
```

### 配置

前往 [夸克扫描王开发者后台](https://scan.quark.cn/business) 获取 API Key，然后在 OpenClaw 中配置：

```bash
# 为三个技能分别设置 API Key
openclaw config set skills.entries.yescan-ocr-universal.env.SCAN_WEBSERVICE_KEY "your_api_key_here"
openclaw config set skills.entries.yescan-scan-universal.env.SCAN_WEBSERVICE_KEY "your_api_key_here"
openclaw config set skills.entries.yescan-transoffice-universal.env.SCAN_WEBSERVICE_KEY "your_api_key_here"
```

或者直接设置环境变量：

```bash
export SCAN_WEBSERVICE_KEY="your_api_key_here"
```

> **提示：** 通过 CLI 配置后，需要重启 OpenClaw 或开启新会话才能生效（技能列表在 session 启动时加载）。

---

## 使用示例

安装并配置完成后，技能会自动对你的 OpenClaw Agent 可用。只需用自然语言描述你想做的事情。

### OCR 示例

**提取文档照片中的文字：**

> 用户："识别一下这张图片里的文字：https://example.com/document.jpg"

Agent 自动路由到 `general-ocr`，返回结构化 JSON：

<details>
<summary>点击查看响应</summary>

```json
{
  "code": "00000",
  "message": "success",
  "data": {
    "ocrText": "2025年度报告\n营业收入：¥8,500万\n净利润：¥1,580万...",
    "confidence": 0.97
  }
}
```

</details>

**识别增值税发票：**

> 用户："帮我读一下这张发票"（附带图片）

Agent 匹配到 `vat-invoice-ocr`，提取金额、日期、销售方等结构化字段：

<details>
<summary>点击查看响应</summary>

```json
{
  "code": "00000",
  "message": "success",
  "data": {
    "ocrText": "{\"invoiceCode\":\"011001...\",\"invoiceDate\":\"2025-06-10\",\"amount\":\"¥12,580.00\",\"seller\":\"XX科技有限公司\"}",
    "confidence": 0.96
  }
}
```

</details>

**识别手写字迹：**

> 用户："这张手写笔记写了什么内容？"（附带图片）

Agent 匹配到 `handwritten-ocr`，调用专门的手写识别模型。

### 扫描示例

**去除文档阴影：**

> 用户："这张文档照片有阴影，帮我去掉阴影变清晰"

Agent 路由到 `remove-shadow`，返回增强后的图片：

<details>
<summary>点击查看响应</summary>

```json
{
  "code": "00000",
  "message": "success",
  "data": {
    "path": "/tmp/imgs/enhanced_1718012345.png"
  }
}
```

</details>

**增强试卷：**

> 用户："这张试卷照片太糊了，增强一下并把题目提取出来"

Agent 使用 `exam-enhance` 生成高清、去噪的试卷图片。

**去水印：**

> 用户："把图片右下角的水印去掉"

Agent 选择 `remove-watermark` 进行精准水印去除。

### 转换示例

**表格图片转 Excel：**

> 用户："把这张表格照片转成 Excel"

Agent 路由到 `image-to-excel`，返回可编辑的 `.xlsx` 文件：

<details>
<summary>点击查看响应</summary>

```json
{
  "code": "00000",
  "message": "success",
  "data": {
    "downloadUrl": "https://scan-business.quark.cn/output/abc123.xlsx",
    "fileName": "table_output.xlsx",
    "fileSize": 45056
  }
}
```

</details>

**合同扫描件转 Word：**

> 用户："把这份合同扫描件变成可编辑的 Word 文档"

Agent 选择 `image-to-word`，生成保留排版的 `.docx` 文件。

---

## 架构设计

```
┌─────────────────────────────────────────────────────┐
│                  OpenClaw Agent                      │
│                                                     │
│  ┌─────────────┐  ┌──────────┐  ┌───────────────┐  │
│  │   意图匹配   │  │  场景    │  │   执行引擎     │  │
│  │   (Intent)   │→ │  路由    │→ │  (Execution)  │  │
│  └─────────────┘  └──────────┘  └───────┬───────┘  │
└─────────────────────────────────────────┼───────────┘
                                          │
                    ┌─────────────────────┼──────────────┐
                    │       YesCan Skills 能力层            │
                    │                                      │
                    │  ┌─────────┐  ┌────────┐  ┌──────┐ │
                    │  │  OCR    │  │  Scan  │  │Trans │ │
                    │  │  技能   │  │  技能  │  │技能  │ │
                    │  └────┬────┘  └───┬────┘  └──┬───┘ │
                    │       │           │           │      │
                    │  scripts/scan.py（统一 CLI 入口）     │
                    └──────────────┬──────────────────────┘
                                   │
                          ┌────────┴────────┐
                          │  夸克扫描王       │
                          │  API 服务        │
                          │  (scan-business. │
                          │   quark.cn)      │
                          └─────────────────┘
```

**工作流程：**

1. **意图匹配** — OpenClaw Agent 接收自然语言请求，根据 SKILL.md 的描述匹配对应技能（OCR / 扫描 / 转换）。

2. **场景路由** — 在匹配到的技能内，按优先级排序的场景列表确定正确的 `--scene` 标识符。

3. **命令执行** — 调用统一的 `scripts/scan.py` CLI，传入场景参数和图片输入（URL、文件路径或 Base64）。

4. **云端处理** — 脚本将图片发送至夸克扫描王云端 API，由 AI 模型进行处理。

5. **结构化输出** — 结果以 JSON 格式返回。OCR 返回结构化文本数据，扫描返回增强后的本地图片路径，转换返回可下载的文件链接。

---

## API 参考

三个技能共享统一的 CLI 接口：

```bash
# URL 输入
SCAN_WEBSERVICE_KEY=$SCAN_WEBSERVICE_KEY python3 scripts/scan.py \
  --scene "${SCENE_VALUE}" \
  --url "${IMAGE_URL}"

# 本地文件输入
SCAN_WEBSERVICE_KEY=$SCAN_WEBSERVICE_KEY python3 scripts/scan.py \
  --scene "${SCENE_VALUE}" \
  --path "${IMAGE_FILE_PATH}"

# Base64 输入
SCAN_WEBSERVICE_KEY=$SCAN_WEBSERVICE_KEY python3 scripts/scan.py \
  --scene "${SCENE_VALUE}" \
  --base64 "${IMAGE_BASE64}"
```

**参数说明：**

| 参数 | 类型 | 说明 |
|------|------|------|
| `--scene` | string | 场景标识符（见上方场景表） |
| `--url` | string | 公网 HTTPS 图片链接 |
| `--path` | string | 本地文件路径（jpg/png/gif/bmp/webp/tiff） |
| `--base64` | string | Base64 编码的图片数据 |

**响应格式（OCR）：**

```json
{
  "code": "00000",
  "message": "success",
  "data": {
    "ocrText": "识别到的文字内容...",
    "confidence": 0.98,
    "scene": "general-ocr"
  }
}
```

**响应格式（扫描 — 图片输出）：**

```json
{
  "code": "00000",
  "message": "success",
  "data": {
    "path": "/tmp/imgs/enhanced_1718012345.png"
  }
}
```

**响应格式（转换 — 文件输出）：**

```json
{
  "code": "00000",
  "message": "success",
  "data": {
    "downloadUrl": "https://...",
    "fileName": "output.docx",
    "fileSize": 102400
  }
}
```

---

## 错误码说明

| 错误码 | 说明 | 处理建议 |
|-------|------|---------|
| `00000` | 成功 | — |
| `A0100` | API Key 未配置 | 设置 `SCAN_WEBSERVICE_KEY` 环境变量 |
| `A0201` | 缺少图片输入 | 提供 URL、文件路径或 Base64 |
| `A0211` | API 配额不足 | 升级套餐或等待配额重置 |
| `A0406` | 图片链接不可达 | 检查 URL 是否可访问且为 HTTPS |
| `A0407` | 图片链接不安全 | 仅支持 HTTPS 链接 |
| `FILE_ERROR` | 本地文件读取失败 | 检查文件路径和权限 |
| `FILE_READ_ERROR` | 文件 I/O 错误 | 确认文件存在且未损坏 |
| `URL_VALIDATION_ERROR` | URL 格式不合法 | 提供格式正确的 HTTPS 链接 |
| `BASE64_*` | Base64 解码错误 | 检查 Base64 编码格式 |
| `HTTP_ERROR` | HTTP 请求异常 | 检查网络连接 |

---

## 使用限制

| 限制项 | 详情 | 解决方案 |
|-------|------|---------|
| **单次单图** | 每次 API 调用处理一张图片 | 批量处理请循环调用 |
| **文件大小** | 最大 5MB | 先压缩或裁剪 |
| **不支持视频** | 仅支持静态图片 | 先提取视频帧再逐帧处理 |
| **仅 HTTPS** | HTTP 链接会被拒绝 | 使用 HTTPS 链接 |
| **支持格式** | jpg, jpeg, png, gif, bmp, webp, tiff, wbmp | 先转换为支持的格式 |
| **实时流** | 不支持 | 使用专用视频处理服务 |

---

## 常见问题

**Q: 图片超过 5MB 怎么办？**
A: 发送前先压缩或裁剪图片。可以使用 ImageMagick 的 `convert` 命令或 Python 的 Pillow 库进行缩放。

**Q: 能否一次处理多张图片？**
A: 不能，每次 API 调用只处理一张图片。批量处理请循环调用。

**Q: 夸克扫描王 API 不可用时怎么办？**
A: 技能会返回 `HTTP_ERROR` 错误码。没有自动重试机制，你可以手动重试。

**Q: 如何提升 API 配额？**
A: 前往 [夸克扫描王开发者后台](https://scan.quark.cn/business) 查看当前套餐和升级选项。

**Q: 图片会被保存在夸克服务器上吗？**
A: 图片实时处理，**不会永久保存**在夸克服务器上。扫描技能返回的增强图片保存在本地 `/tmp/` 目录。

**Q: 可以使用 HTTP 链接吗？**
A: 不可以，出于安全考虑仅支持 HTTPS 链接。请使用 HTTPS 端点或将图片作为本地文件/base64 提供。

---

## 贡献指南

欢迎贡献代码！请按以下步骤操作：

1. **Fork** 本仓库。
2. 创建功能分支：`git checkout -b feature/new-scene`
3. 在对应的技能目录中添加或修改场景。
4. 使用示例图片测试你的改动。
5. 提交 **Pull Request**，附上清晰的变更说明。

**开发规范：**

- 每个技能目录遵循 OpenClaw 技能规范：`SKILL.md` + `scripts/` + `references/`。
- `scan.py` 是统一的执行入口——修改 CLI 接口时需同步更新三个技能。
- 场景匹配按**优先级排序**——将更具体的场景放在通用场景之前。
- 所有响应必须是合法的 JSON——下游系统直接解析。

---

## 开源协议

本项目基于 [Apache License 2.0](LICENSE) 开源。

夸克扫描王 API 是由 [夸克（阿里巴巴集团）](https://scan.quark.cn/business) 提供的第三方服务，使用需遵守其[服务条款](https://scan.quark.cn/business)。

---

## 致谢

- [OpenClaw](https://github.com/anthropics/openclaw) — 驱动这些技能的 Agent 框架。
- [夸克扫描王](https://scan.quark.cn/business) — 文档 AI 引擎与云基础设施。
- [PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR) — 项目结构和文档风格的灵感来源。

---

<div align="center">

<p>由 YesCan 团队用心打造</p>

<p><a href="https://scan.quark.cn/business">获取 API Key</a> · <a href="https://github.com/YOUR_ORG/openclaw-yescan-skills/issues">反馈问题</a> · <a href="https://github.com/YOUR_ORG/openclaw-yescan-skills/discussions">社区讨论</a></p>

</div>
