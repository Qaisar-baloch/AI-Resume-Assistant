# AI Resume ATS Checker

An AI-assisted resume review application built with Python, Streamlit and Google Gemini. A user uploads a resume, the application extracts its text and requests a structured general-purpose ATS-readiness review.

**Project type:** training / portfolio application.

## Features

- Accepts PDF, DOCX and TXT resume uploads.
- Extracts PDF text with pypdf.
- Extracts paragraphs and table-cell text from DOCX files with python-docx.
- Uses Google Gemini through the google-genai SDK.
- Returns a structured analysis containing an estimated score, strengths, improvements, ATS keywords and formatting checks.
- Allows the Gemini model identifier to be changed in the sidebar.
- Reads the API key from Streamlit Secrets or the GEMINI_API_KEY environment variable.

> **Important:** the score is an AI-generated estimate, not an official result from an employer's ATS. The current implementation reviews a resume without a job description. Uploaded resume text is sent to the configured Gemini API, so do not upload information you do not want processed by that external service.

## Analysis pipeline

~~~text
Resume upload (PDF / DOCX / TXT)
          |
          v
Text extraction
(pypdf / python-docx / UTF-8)
          |
          v
Prompt construction
(general-purpose ATS review)
          |
          v
Google Gemini API
          |
          v
Structured JSON response
          |
          v
Defensive parsing and validation
          |
          v
Streamlit results dashboard
(score, strengths, improvements, keywords, checks)
~~~

The application truncates extracted resume text to a maximum of 50,000 characters before sending it to the model. The model is instructed not to invent experience, education, dates, skills or achievements.

## Technology stack

| Component | Technology |
|---|---|
| Language | Python |
| UI | Streamlit |
| LLM provider | Google Gemini |
| API SDK | google-genai |
| PDF extraction | pypdf |
| DOCX extraction | python-docx |
| Response format | JSON |
| Session state | Streamlit session state |

## Repository structure

~~~text
AI-Resume-Assistant/
├── app.py
├── requirements.txt
├── LICENSE
└── README.md
~~~

Local Streamlit Secrets are created by the user and should not be committed.

## Run locally

### 1. Clone the repository

~~~bash
git clone https://github.com/Qaisar-baloch/AI-Resume-Assistant.git
cd AI-Resume-Assistant
~~~

### 2. Create a virtual environment

~~~bash
python -m venv .venv
~~~

Activate it:

**Windows**

~~~powershell
.venv\Scripts\activate
~~~

**macOS / Linux**

~~~bash
source .venv/bin/activate
~~~

### 3. Install dependencies

~~~bash
pip install -r requirements.txt
~~~

### 4. Configure Gemini

Create .streamlit/secrets.toml:

~~~toml
GEMINI_API_KEY = "your_gemini_api_key"
~~~

Alternatively, set GEMINI_API_KEY as an environment variable.

Never commit the real API key or secrets file.

### 5. Run

~~~bash
streamlit run app.py
~~~

The local app normally opens at http://localhost:8501.

## Deploy

The app can be deployed to Streamlit Community Cloud:

1. Import this GitHub repository.
2. Select the main branch.
3. Set the main file path to app.py.
4. Add GEMINI_API_KEY in the deployment Secrets settings.
5. Deploy the application.

## Current limitations

- The ATS score is heuristic model output and is not tied to any specific recruitment system.
- The current prompt performs a general resume review; job-description matching is not implemented.
- Scanned or image-only PDFs may yield little or no extractable text.
- There is no user account, persistent resume history or database.
- Results depend on the configured Gemini model, API access, quota and response quality.
- The application provides suggestions, not guaranteed hiring outcomes.

## Possible next steps

- Add job-description-specific matching.
- Add a skills-gap comparison.
- Add downloadable PDF reports.
- Add OCR for scanned resumes.
- Add optional resume revision and bullet-point rewriting.
- Add a privacy-aware user history feature.

## Author and training context

**Qaisar Khan** · [GitHub profile](https://github.com/Qaisar-baloch)

This project was developed as a hands-on AI application exercise within the Generative & Agentic AI learning work of Pak Angels Cohort 11.

## License

See [LICENSE](LICENSE).
