# Complytics Marketing Meme Generator

A Streamlit app that helps you:
- Collect business details (name, website, about).
- Generate marketing ideas as a CSV via Google Gemini with columns: [meme_template, prompt, company_background, marketing_message, call_to_action, target_audience, platform, theme].
- Turn those ideas into AI-generated meme images and export everything (data + images) to an Excel file.

## Features
- Step-by-step UI in three tabs:
  1) Business Info: capture basic business context.
  2) Generate Marketing Data: create a CSV of meme ideas tailored to your business.
  3) Generate Memes & Export: select rows (or Select All), generate images using Gemini, and export to Excel.
- Uses streaming image generation for reliability and saves images locally.
- Includes “Select All” for batch meme creation.

## How it works
- Text generation model: `gemini-2.5-flash` to produce CSV content.
- Image generation model: `gemini-2.5-flash-image-preview` to produce meme images.
- Exact image prompt assembled from each CSV row (using the specified columns) and sent to the image model.
- Results are saved as PNGs and summarized into an Excel workbook with OpenPyXL.

## Requirements
- Python 3.10+
- Google Gemini API key (AI Studio)

Python packages:
- streamlit
- pandas
- pillow
- openpyxl
- python-dotenv
- google-genai

## Setup
1) Clone or copy this repository under your workspace.
2) Create a virtual environment and install dependencies:

```
python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS/Linux
source .venv/bin/activate

pip install -U pip
pip install streamlit pandas pillow openpyxl python-dotenv google-genai
```

or 

```
pip install uv

# To create venv
uv venv

# Windows
.venv\Scripts\activate
# macOS/Linux
source .venv/bin/activate

uv sync
```

3) Create a .env file in the project root with your Gemini key:

```
gemini_api_key=YOUR_API_KEY_HERE
```

Note: Do not commit your API key. Keep .env out of version control.

## Run
From the repository root, launch Streamlit:

```
streamlit run marketing-meme-generator/app.py
```

This opens the app in your browser.

## Usage
1) Step 1: Business Info
   - Enter Business Name, Website, and About Business.
   - Click “Proceed to Generate Marketing Data”.

2) Step 2: Generate Marketing Data
   - Click “Generate Marketing Data CSV”.
   - The app asks Gemini to produce 10 rows with the required columns.
   - Review the table, and optionally download `generated_marketing_data.csv`.

3) Step 3: Generate Memes & Export
   - Select one or more rows, or choose “Select All”.
   - Click “Generate Memes for Selected Rows”. Images are generated and shown.
   - Click “Export to Excel” to create `memes_export.xlsx` containing the metadata and embedded images.

## Output files
- `generated_marketing_data.csv`: CSV of marketing ideas from Step 2.
- `meme_<index>.png`: Image files generated in Step 3.
- `memes_export.xlsx`: Excel workbook with one row per meme and the image embedded.

## Troubleshooting
- Missing API key: ensure `.env` contains `gemini_api_key=...` and restart the app.
- CSV parse issues: occasionally LLMs may produce malformed CSV. Regenerate or manually fix the CSV and reload.
- Rate limits or model errors: wait and retry, reduce batch size, or try again later.
- No images returned: regenerate with the same row or choose a different row.

## Customization
- Number of ideas: adjust the requested row count in the CSV generation prompt.
- Prompt content: the image prompt is assembled from CSV columns; tailor the prompt template in Step 3 if needed.
- File names/paths: update save prefixes or output directories in the app code.

## Security
- Keep your API key secret. Do not commit .env or share it publicly.

## Acknowledgements
- Google AI Studio (Gemini)
- Streamlit
- OpenPyXL
- Pillow

---
Happy meme making!