# Resume ATS Checker

A beginner-friendly Streamlit app that analyzes a resume with Google's Gemini Flash model and returns an **estimated ATS-readiness score**, improvement suggestions, keyword feedback, and example bullet rewrites.

> **Important:** This is an AI-generated heuristic, not a score from a real Applicant Tracking System (ATS). Results are guidance, not a hiring guarantee. Always verify suggested rewrites and never add skills, achievements, or metrics that are not true.

## Features

- Upload a resume as PDF, DOCX, or TXT.
- Optionally paste the target job description for more relevant keyword feedback.
- See an estimated score out of 100 with a breakdown.
- Review strengths, improvements, missing/underused keywords, formatting checks, and sample bullet rewrites.
- Download the report as JSON.
- Uses a Gemini API key stored outside the source code.

## 1. Get a Gemini API key

Create an API key in Google AI Studio: https://aistudio.google.com/apikey

Keep the key private. Do not paste it into `app.py`, commit it to GitHub, or share it in screenshots.

## 2. Run locally

Use Python 3.10 or newer.

```bash
# Optional: create and activate a virtual environment
python -m venv .venv

# Windows PowerShell
.venv\Scripts\Activate.ps1

# macOS/Linux
source .venv/bin/activate

pip install -r requirements.txt
```

Set the API key in your terminal before running the app.

**Windows PowerShell**
```powershell
$env:GEMINI_API_KEY="YOUR_API_KEY_HERE"
streamlit run app.py
```

**macOS/Linux**
```bash
export GEMINI_API_KEY="YOUR_API_KEY_HERE"
streamlit run app.py
```

Then open the local URL shown in the terminal, usually `http://localhost:8501`.

## 3. Push to GitHub using the website UI

1. Sign in at https://github.com and create a **New repository**.
2. Give it a name such as `resume-ats-checker`. Choose Public or Private as you prefer.
3. Do not add a real API key or a file containing secrets to the repository.
4. Open the new repository and choose **Add file → Create new file**.
5. Create `app.py`, paste the contents of your local `app.py`, and commit the file.
6. Repeat **Add file → Create new file** for `requirements.txt` and `README.md`. Paste each file's contents and commit.
7. Confirm all three files appear in the repository. The `README.md` should appear on the repository home page.

If you already have these files on your computer, you can instead use **Add file → Upload files** and drag the three files into the repository, then commit.

## 4. Deploy on Streamlit Community Cloud

1. Push the repository to GitHub first.
2. Open https://share.streamlit.io/ and sign in with GitHub.
3. Choose **Create app** (or **Deploy an app**).
4. Select the repository, branch (usually `main`), and main file path `app.py`.
5. Open the app's **Advanced settings / Secrets** section before or during deployment.
6. Add the secret in TOML format:

   ```toml
   GEMINI_API_KEY = "YOUR_REAL_API_KEY_HERE"
   ```

   Keep the quotes. Do not commit this secret to GitHub.
7. Deploy the app and wait for the build to finish.
8. Open the app URL. Upload a sample resume and optionally paste a job description to test it.

If the app fails to deploy, open the app's **Manage app → Logs** page and check the error. Common causes are a missing dependency, invalid secret format, an invalid API key, or a model name not available to your account.

## Files

- `app.py` — Streamlit UI, file text extraction, Gemini call, and report display.
- `requirements.txt` — Python dependencies.
- `README.md` — setup, GitHub UI upload, and deployment instructions.

## Privacy and limitations

- Resume text is sent to Google's Gemini API for analysis.
- The app currently extracts text from text-based PDFs, DOCX, and TXT files. Scanned/image-only PDFs may need OCR before upload.
- Do not upload a resume without the document owner's permission.
- ATS systems vary; a real employer's ATS may score or parse the same resume differently.
- The app truncates extracted text beyond 40,000 characters to keep requests manageable.
