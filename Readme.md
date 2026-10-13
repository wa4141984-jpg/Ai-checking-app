# ATS Resume Analyzer

Upload a resume (PDF, DOCX or TXT) and get an **ATS score** plus **prioritised, actionable improvements**, powered by Google Gemini Flash and a Streamlit UI.

## How the score works

| Part | Weight | Source |
|------|--------|--------|
| Format checks | 30% | Local rules: contact info, standard section headings, length, bullet points, quantified achievements |
| Content score | 70% | Gemini: keyword relevance, impact, clarity, skills coverage |

Paste a job description for a keyword-match score against that specific job. Without one, the app evaluates general ATS-readiness.

> ATS scores are **estimates**. Real systems (Workday, Greenhouse, Lever, etc.) have no public scoring standard, so treat the result as guidance, not a guarantee.

## Features
- PDF / DOCX / TXT upload (max 5 MB)
- Overall, format and content scores with breakdown
- Improvement suggestions with High/Medium/Low priority and example rewrites
- Missing-keyword list, strengths and weaknesses
- Downloadable JSON report
- Detects image-only (scanned) resumes that ATS can't read

## Run locally

```bash
git clone https://github.com/<your-username>/ats-resume-analyzer.git
cd ats-resume-analyzer
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

Get a free API key at <https://aistudio.google.com/apikey>, then either:

```bash
# Option A: secrets file
cp .streamlit/secrets.toml.example .streamlit/secrets.toml   # then edit the key

# Option B: environment variable
export GEMINI_API_KEY="your-key"      # Windows PowerShell: $env:GEMINI_API_KEY="your-key"
```

Start the app:

```bash
streamlit run app.py
```

You can also skip both options and paste the key into the sidebar.

## Configuration

| Setting | Default | Purpose |
|---------|---------|---------|
| `GEMINI_API_KEY` | - | Your Gemini API key (secret or env var) |
| `GEMINI_MODEL` | `gemini-flash-latest` | Model name; pin a version such as `gemini-3.5-flash` if you want |

## Deploy on Streamlit Community Cloud
1. Push this repo to GitHub (never commit `secrets.toml`; it is git-ignored).
2. Go to <https://share.streamlit.io>, sign in with GitHub, click **Create app**.
3. Choose the repo, branch `main`, main file `app.py`.
4. Open **Advanced settings -> Secrets** and add: `GEMINI_API_KEY = "your-key"`
5. Click **Deploy**.

## Privacy
Resume text is sent to the Gemini API for analysis. The app does not store uploads or results on disk.

## Project structure
```
app.py            # Streamlit app
requirements.txt  # Dependencies
README.md
.streamlit/secrets.toml.example
```
