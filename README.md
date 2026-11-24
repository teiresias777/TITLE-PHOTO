# Title Photo — AI Metadata & SEO Engine

**Title Photo** is a free macOS app that writes **titles, descriptions and SEO keywords** into your photos automatically. It looks at each image with an AI vision model (a local one through **Ollama**, or **Google Gemini** in the cloud) and saves the result straight into your files, ready for Lightroom, Adobe Stock, Shutterstock, your online shop or social media.

*by [Lambros Kazan](https://www.lambroskazan.com)*

<!-- Add a screenshot here: ![Title Photo](docs/screenshot.png) -->

---

## What it does

- Scans a folder (optionally with sub-folders) for **RAW** (`.arw .cr2 .cr3 .nef .dng .raf .orf`) and/or **JPG** files.
- Sends a small 512 px preview of each photo to the AI and asks for a title, a description and an exact number of keywords.
- Writes the result with ExifTool:
  - **RAW** → an `.xmp` sidecar next to the file (the RAW itself is never touched).
  - **JPG** → inside the file (XMP + IPTC).
- Skips photos that already have enough keywords (unless you tick *Overwrite existing*).

## Features

| | |
|---|---|
| **Two AI engines** | Local (Ollama, free and private) or Cloud (Gemini API, free and paid tiers, with automatic model fallback) |
| **Platform presets** | Adobe Stock, Shutterstock, Flickr/500px, Etsy (20-character keyword limit), Google Shopping, Facebook, Instagram, Pinterest, WooCommerce, Blog/SEO, Alt Text, plus your own saved presets. Each preset shows a short platform tip and the AI is told what that platform ranks first |
| **Full control of limits** | Min/max characters for title and description, exact keyword count and optional maximum length per keyword. Texts are never cut mid-sentence: the AI is asked to rewrite them to fit, and any last-resort trim happens at a natural break |
| **Language & style** | English or Greek output; Descriptive, Commercial, Minimal, Storytelling or SEO-focused tone; optional custom prompt |
| **Photo context & word rules** | Tell the AI the place or event, force keywords on every photo, ban unwanted words |
| **Auto context** | Optional hints from EXIF (date, focal length), the folder name and, if you choose, GPS |
| **RAW + JPG pairs** | Analyses the JPG once and writes the same metadata to both files |
| **Undo** | The original metadata is backed up before every batch; one click restores it |
| **Quality checks** | Warnings for duplicate or similar titles, texts below the minimum, missing keywords and banned words; singular/plural duplicate keywords are removed |
| **Live Inspector** | Review every processed photo, edit the text and save it back to the file |
| **Pause / Resume, ETA** | Elapsed time, estimated time left and number of AI requests |
| **CSV export** | File name, title, description and keywords of the whole session |
| **Correct orientation** | Vertical photos are previewed and analysed upright |

## Requirements

- **macOS**
- **[ExifTool](https://exiftool.org)** — `brew install exiftool`
- One AI backend:
  - **[Ollama](https://ollama.com)** with a vision model (the app can download recommended ones, e.g. `qwen2.5vl:7b`), **or**
  - a **Gemini API key** from [Google AI Studio](https://aistudio.google.com)

The packaged app needs nothing else: Python, Tk and all libraries are bundled inside.

## Installation

### Option A — the app (recommended)

1. Download `Title Photo.app` (zipped) from the [Releases](../../releases) page and move it to **Applications**.
2. The app is not signed by Apple. On the first launch, **right-click → Open**.
3. Install ExifTool (see above) and Ollama or get a Gemini key.


## Quick start

1. Choose the **File Type** and the **Source Folder**.
2. Choose the **AI Engine** (Ollama model, or Gemini model + API key; press *Test* to check the key).
3. Pick a **Preset** that matches where the photos will be used, and adjust the limits if you like.
4. Optional: write a **Photo context** (e.g. `Santorini, wedding, July 2026`) and add *Always add* / *Never use* words.
5. Press **▶ Start**. Watch the log and the Live Inspector. Use **⏸ Pause** or **■ Stop** at any time.
6. Not happy with the result? Press **↶ Undo batch** to restore the previous metadata.

Hover over any field in the app to see what it does.

## Notes on privacy and cost

- **Local (Ollama)**: photos never leave your computer.
- **Cloud (Gemini)**: a 512 px preview of each photo and the text prompt are sent to Google. If you enable **Include GPS**, the coordinates are sent too. Usage may be billed by Google depending on your tier.
- Your API key is stored only on your Mac, in `~/.title_photo_config.json`, and is sent to Google in a request header.
- Backups for *Undo* are stored in `~/.title_photo_backups` (the last 10 batches).

## Tips

- Keep the keyword count of the preset: stock agencies reject files with too few or too many.
- AI cannot know places or events. Use **Photo context** or **Auto context** to improve accuracy.
- With the free Gemini tier the app processes one photo at a time on purpose, to stay under the rate limits.
- Lightroom Classic: use *Metadata → Read Metadata from Files* to load the new data from the `.xmp` sidecars.

## Troubleshooting

| Problem | Solution |
|---|---|
| "exiftool was not found" | Install it with `brew install exiftool` and restart the app |
| "Ollama Not Detected" | Start the Ollama app, then press ↻ next to the model list |
| Gemini returns HTTP 429 | Rate limit. Keep *Auto-fallback* on, use *Free Tier* pacing or increase *Cooldown* |
| Photos show as "Skipping (Ready…)" | They already have enough keywords. Tick *Overwrite existing* to redo them |
| App will not open (not verified developer) | Right-click the app → **Open** |

## Support

Title Photo is free. If it saves you time you can [buy me a coffee ☕](https://buymeacoffee.com/lambroskazan).

## License

Free to use.
