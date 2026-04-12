# Korean Vocabulary Extractor

An Android app that uses Google Gemini AI to extract Korean vocabulary from text, PDFs, and images, then exports it as Anki flashcard decks.

## Download

Get the latest APK from the [**Releases**](../../releases/latest) page.

> **Requires Android 7.0 (API 24) or higher.**

## Features

- **AI-powered extraction** — paste text or upload PDF/image files; Gemini identifies Korean words automatically
- **Anki export** — generates `.apkg` files ready to import into Anki, including Korean, romanization, French translation, and part of speech
- **Vocabulary history** — SQLite-backed log of all extracted words with search and filtering
- **Batch processing** — process up to 10 files at a time; PDFs are split page by page (max 10 pages total across all files) for more thorough extraction
- **Configurable models** — choose between Gemini Flash and Pro variants
- **Secure key storage** — API key stored via Android Keystore, never hard-coded

## How to Use

### Step 1 — Add your Gemini API key (required first step)

Go to the **Settings** tab and paste your Gemini API key. You can get a free key at [Google AI Studio](https://aistudio.google.com/app/api-keys). Tap **Save**, then **Test** to verify it works. You can also set your default Anki deck name and choose the Gemini model here.

> **Getting your API key:** A Google Cloud project is required before generating a key. If this is your first time, don't worry — Google AI Studio will prompt you to create a project automatically during the API key creation flow. Just follow the on-screen steps and your key will be ready in under a minute.

<p align="center">
  <img src="Screenshots/Screenshot_settings.png" width="280" alt="Settings screen showing Gemini API key field">
</p>

---

### Step 2 — Import text or an image

Switch to the **Input** tab. Choose your source:

- **Text** — paste any Korean text directly into the field and tap **Extract Vocabulary**.
- **Image** — switch to the Image tab, tap **Choose Files** or **Take Photo** to import a screenshot or photo containing Korean.
- **PDF** — switch to the PDF tab and select up to 10 PDF files; each page is sent to Gemini individually (max 10 pages total) for maximum extraction accuracy.

<p align="center">
  <img src="Screenshots/Screenshot_input_text.png" width="280" alt="Text input screen with Korean sentence">
  &nbsp;&nbsp;
  <img src="Screenshots/Screenshot_image.png" width="280" alt="Image input screen with Choose Files and Take Photo buttons">
</p>

---

### Step 3 — Review extracted vocabulary

After extraction, the **Review** screen lists every word Gemini found, with its French translation, an example sentence, and part of speech. Before saving you can:

- Remove any word you don't want by tapping the **×** button.
- Apply a **thematic tag** to all entries at once (e.g. "Chapter 3", "Drama vocab").
- Tap any row to open the **Edit Entry** dialog and correct the Korean, French translation, example sentence, POS, or tag.

Once satisfied, tap **Commit to Database** to save everything.

<p align="center">
  <img src="Screenshots/Screenshot_review_text.png" width="280" alt="Review screen listing 4 extracted words">
  &nbsp;&nbsp;
  <img src="Screenshots/Screenshot_review_edit.png" width="280" alt="Edit Entry dialog for a single vocabulary card">
</p>

---

### Step 4 — Browse and export your vocabulary

The **Vocabulary** tab shows your full word list. You can:

- **Search** by Korean word, French translation, or example phrase.
- **Filter** by part of speech or tag.
- **Select** words and export them as an Anki `.apkg` deck or a CSV file.

<p align="center">
  <img src="Screenshots/Screenshot_vocabulary.png?v=2" width="280" alt="Vocabulary screen showing 4 saved words with search and filter">
</p>

---

### Step 5 — Track your progress

The **Stats** tab gives a live overview of your learning:

- **TOPIK Milestone** — two circular gauges track progress toward TOPIK I (800 words, green) and TOPIK II (3 500 words, purple).
- **Learning Velocity** — daily average over the last 30 days and a weekly bar chart to spot study streaks.
- **Source Analysis** — donut chart breaking down vocabulary by import source (PDF · CSV · Image · Text) with a per-source session count.
- **Breakdown** — horizontal bar chart of your vocabulary split by part of speech (Noun, Verb, Adjective…).

<p align="center">
  <img src="Screenshots/Screenshot_stats_1.png" width="280" alt="Stats screen showing TOPIK milestone gauges and learning velocity chart">
  &nbsp;&nbsp;
  <img src="Screenshots/Screenshot_stats_2.png" width="280" alt="Stats screen showing source analysis donut chart and part-of-speech breakdown">
</p>

---

## Supported Input Types

| Type | Details |
|---|---|
| Plain text | Paste any Korean text directly |
| PDF | Split page by page — max 10 pages total across all imported files |
| Images | JPEG, PNG screenshots of Korean content |
| CSV | Import existing vocabulary lists — see format below |

### CSV Import Format

The file must be UTF-8 encoded (Excel BOM is handled automatically). Two columns are required; the rest are optional:

| Column | Header name | Required | Description |
|---|---|---|---|
| Korean word | `korean` | Yes | The Korean word or expression |
| French translation | `french` | Yes | Translation (separate meanings with `,`) |
| Example sentence | `phrase` | No | An example sentence in Korean |
| Part of speech | `part_of_speech` | No | e.g. `Noun`, `Verb`, `Adjective`, `Adverb` |
| Thematic tag | `thematic_tag` | No | e.g. `Chapter 3`, `Drama vocab` |

**Example:**

```csv
korean,french,phrase,part_of_speech,thematic_tag
일찍,tôt,저는 매일 일찍 일어나요.,Adverb,Daily life
자다,dormir,밤에 일찍 자요.,Verb,Daily life
건강,santé,,Noun,
```

If no header row is present, columns are read positionally in the order above.

## Release Notes

### V0.5 — 2026-04-12

- **Page-by-page PDF extraction** — each PDF page is now sent to Gemini as a separate request, preventing context-window truncation on long documents and extracting significantly more vocabulary
- **10-page global cap** — total pages across all imported PDF files is capped at 10; pages beyond the limit are skipped with a warning

### V0.4 — 2026-04-11

- **TOPIK Milestone gauges** — green for TOPIK I (800 words) and purple for TOPIK II (3 500 words)
- **Learning Velocity** — daily average over the last 30 days and weekly bar chart
- **Source Analysis** — donut chart breaking down vocabulary by import source (Text · PDF · Image · CSV)
- **Import session tracking** — every extraction records an entry with correct source attribution

### V0.3 Beta — 2026-04-10

- **Custom extraction prompts** — edit the prompts sent to Gemini for Text, PDF, and Image modes
- **Prompt reset** — restore built-in defaults instantly

### V0.2 Beta — 2026-04-09

- **CSV import preview** — inspect and edit cards before saving
- **Custom export filenames**
- **Select all vocabulary**
- **Smart duplicate detection**

### V0.1 — Initial Release

- AI-powered Korean vocabulary extraction from text, PDF, and images via Gemini API
- Anki `.apkg` export
- SQLite vocabulary history
- Secure API key storage

## License

MIT
