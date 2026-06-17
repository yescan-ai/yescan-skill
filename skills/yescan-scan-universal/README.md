# yescan-scan-universal

**English** | [简体中文](README.zh-CN.md)

Enhance, denoise, and optimize images — remove handwriting, watermarks, shadows, moire patterns, and more — powered by [Quark Scan King](https://scan.quark.cn/business).

## What it does

Send a single image (URL / local path / base64) to the Quark Scan King API and receive an enhanced image saved to the system temp directory. Designed for AI agents (Claude / Codex / Claude Code / Coze / etc.) to invoke as a skill.

| Category | Scenes |
|---|---|
| Enhancement | `exam-enhance`, `image-hd-enhance`, `certificate-enhance`, `scan-contract`, `scan-document` |
| Removal | `remove-handwriting`, `remove-watermark`, `remove-shadow`, `remove-screen-pattern`, `remove-background-color` |
| Transform | `image-crop-rectify`, `sketch-drawing`, `extract-lineart` |

## Quick start

1. Get an API key from `https://scan.quark.cn/business` (Developer Console → API Key)
2. Save it locally:
   ```bash
   echo 'SCAN_WEBSERVICE_KEY=<your_api_key>' > ~/.yescan_env
   chmod 600 ~/.yescan_env
   ```
3. Install the skill into your agent runtime (see your agent's skill installation docs)
4. Ask the agent: *"Enhance this blurry document photo: /path/to/image.png"*

## Repository layout

```
yescan-scan-universal/
├── SKILL.md                 # Agent-facing skill definition (intent dispatcher)
├── README.md                # English documentation
├── README.zh-CN.md          # 中文说明
├── LICENSE                  # MIT
├── SECURITY.md              # Security disclosure & data flow
├── scripts/
│   ├── scan.py              # Entry point
│   └── common/              # Scan King API client, file saver, validators, etc.
├── references/
│   ├── privacy.md           # Data flow, key configuration, rotation
│   ├── implementation.md    # Client-side script behavior, response fields
│   └── troubleshooting.md   # Error codes, common issues
└── examples/
    ├── exam-enhance-example.md
    ├── image-hd-enhance-example.md
    ├── certificate-enhance-example.md
    ├── remove-handwriting-example.md
    ├── remove-watermark-example.md
    ├── remove-shadow-example.md
    ├── remove-screen-pattern-example.md
    ├── remove-background-color-example.md
    ├── image-crop-rectify-example.md
    ├── sketch-drawing-example.md
    ├── extract-lineart-example.md
    ├── scan-contract-example.md
    └── scan-document-example.md
```

## Requirements

- Python 3.9+
- `SCAN_WEBSERVICE_KEY` environment variable (or `~/.yescan_env`)
- Network access to `scan-business.quark.cn`
- Image input ≤ 5 MB, format in jpg/jpeg/png/gif/bmp/webp/tiff/wbmp

## Security

This skill sends user-provided images to a third-party API. Read [SECURITY.md](SECURITY.md) and [references/privacy.md](references/privacy.md) before processing sensitive data.

## License

[MIT](LICENSE)

## Author

[yescan-ai](https://github.com/yescan-ai)
