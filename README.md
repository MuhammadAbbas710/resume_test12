# 📄 ATS Resume Checker

A Streamlit app that scores a resume for ATS (Applicant Tracking System) friendliness and tells you exactly how to improve it, powered by Google Gemini Flash.

## Features

- Upload a resume as **PDF, DOCX or TXT** (max 5 MB)
- Optional **job description** for a much more accurate keyword match
- **Estimated ATS score (0-100)** with a 5-part breakdown: keywords, formatting, content quality, impact/metrics, readability
- Strengths, weaknesses, matched and missing keywords
- Prioritised improvements (high / medium / low) and **rewritten bullet points**
- Instant rule-based checks (email, phone, sections, length, metrics)
- Download the full report as Markdown

> The score is an AI estimate. No tool can reproduce the exact scoring of every employer's ATS, so use it as guidance, not a guarantee.

## Project structure

```
.
├── app.py              # the whole app
├── requirements.txt    # dependencies
└── README.md
```

## Run locally

1. **Get a free Gemini API key** at https://aistudio.google.com/apikey

2. **Install** (Python 3.10+; 3.12 recommended):

   ```bash
   python -m venv .venv
   source .venv/bin/activate        # Windows: .venv\Scripts\activate
   pip install -r requirements.txt
   ```

3. **Provide your key**, using either option:

   - Paste it into the sidebar when the app starts, or
   - Create `.streamlit/secrets.toml` (never commit this file):

     ```toml
     GEMINI_API_KEY = "your-key-here"
     # optional: GEMINI_MODEL = "gemini-2.5-flash"
     ```

   - Or set an environment variable: `export GEMINI_API_KEY="your-key-here"`

4. **Start the app:**

   ```bash
   streamlit run app.py
   ```

## Changing the model

The default is `gemini-2.5-flash`. Google renames and retires models over time. If you see a "model not found" message, change the model name in the sidebar, or set `GEMINI_MODEL` in your secrets. Current names are listed at https://ai.google.dev/gemini-api/docs/models.

## Deploy on Streamlit Community Cloud

1. Push this project to a **GitHub repository** (see below).
2. Go to https://share.streamlit.io and sign in with GitHub.
3. Click **Create app**, pick your repository and branch, and set the main file path to `app.py`.
4. Open **Advanced settings**, choose Python 3.12, and paste your secrets:

   ```toml
   GEMINI_API_KEY = "your-key-here"
   ```

5. Click **Deploy**. You get a public `*.streamlit.app` URL.

> ⚠️ If the app is public, everyone who uses it spends **your** Gemini quota. Either keep the app private (invite specific viewers in the app's sharing settings), or leave `GEMINI_API_KEY` out of the secrets so each visitor enters their own key in the sidebar.

## Push to GitHub

```bash
git init
printf ".venv/\n__pycache__/\n.streamlit/secrets.toml\n.env\n" > .gitignore
git add .
git commit -m "Initial commit: ATS resume checker"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main
```

Create the empty repository on GitHub first (**New repository**, no README or .gitignore, since you already have them).

## Privacy

Resume text is sent to the Google Gemini API for analysis. This app does not store uploaded files or results. Check Google's API terms before using real candidate data.

## Troubleshooting

| Problem | Fix |
|---|---|
| "Gemini rejected the API key" | Re-copy the key from Google AI Studio; make sure there are no spaces. |
| "Model was not found" | Change the model name in the sidebar (see link above). |
| "Rate limit or quota reached" | Wait a minute, or use a key with a higher quota. |
| "Very little text could be extracted" | Your PDF is probably a scanned image. Export a text-based PDF or DOCX. |
| App works locally but crashes on Streamlit Cloud | Check the logs ("Manage app"), and confirm `requirements.txt` is in the repo root. |# resume_test12
