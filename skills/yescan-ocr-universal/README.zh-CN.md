# yescan-ocr-universal

基于夸克扫描王的 AI OCR 文字识别技能，适用于 OpenClaw / Claude Code / Codex。支持 19 种识别场景，从图片中提取结构化文本。

## 功能特点

- **19 种 OCR 场景**：手写体、表格、身份证、社保卡、港澳通行证、学位证、增值税发票、火车票、数学公式、题目、驾驶证、行驶证、英文发票、医疗报告、药检报告、营业执照、商品图、图片翻译、通用文字
- **三种输入方式**：图片 URL、本地文件路径、Base64 字符串
- **结构化输出**：各场景返回特定字段的 JSON（非纯文本）
- **统一密钥**：一个 `SCAN_WEBSERVICE_KEY` 解锁全部场景

## 快速开始

```bash
# 配置 API 密钥（一次性设置）
echo 'SCAN_WEBSERVICE_KEY=<your_key>' > ~/.yescan_env
chmod 600 ~/.yescan_env
```

获取密钥：访问 [scan.quark.cn/business](https://scan.quark.cn/business)。

## 环境要求

- Python 3.9+
- `requests` 库
- 有效的 `SCAN_WEBSERVICE_KEY`

## 隐私说明

图片会发送到 `scan-business.quark.cn` 进行识别。完整数据流向见 [references/privacy.md](references/privacy.md)。

## 许可证

[MIT](LICENSE)
