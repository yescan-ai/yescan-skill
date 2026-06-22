# yescan-ocr-universal

AI-powered OCR text recognition skill for OpenClaw / Claude Code / Codex. Extract structured text from images across 19 scenes — handwriting, tables, IDs, invoices, formulas, image translation, and more.

## Features

- **19 OCR scenes**: handwriting, tables, ID cards, social security cards, travel permits, degree certificates, VAT invoices, train tickets, formulas, exam questions, driver's licenses, vehicle licenses, commercial invoices, medical reports, pharmaceutical inspection reports, business licenses, product images, image translation, and general text
- **Three input modes**: image URL, local file path, or Base64 string
- **Structured output**: scene-specific JSON fields (not just raw text)
- **Single API key**: one `SCAN_WEBSERVICE_KEY` unlocks all scenes

## Quick Start

```bash
# Configure API key (one-time setup)
echo 'SCAN_WEBSERVICE_KEY=<your_key>' > ~/.yescan_env
chmod 600 ~/.yescan_env
```

Get your key at [scan.quark.cn/business](https://scan.quark.cn/business).

## Requirements

- Python 3.9+
- `requests` library
- Valid `SCAN_WEBSERVICE_KEY`

## Privacy

Images are sent to `scan-business.quark.cn` for processing. See [references/privacy.md](references/privacy.md) for full data flow disclosure.

## License

[MIT](LICENSE)
