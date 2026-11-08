# 📄 AI Resume ATS Checker

> **An LLM-powered Resume Analysis Assistant built with Python, Streamlit, and Google Gemini Flash**

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python&logoColor=white)](https://www.python.org/)
[![Streamlit](https://img.shields.io/badge/Streamlit-App-FF4B4B?logo=streamlit&logoColor=white)](https://streamlit.io/)
[![Google Gemini](https://img.shields.io/badge/Google-Gemini%20Flash-8E75B2?logo=google)](https://ai.google.dev/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

An AI-powered web application that analyzes resumes and provides an **estimated ATS readiness score**, strengths, ATS keywords, formatting checks, and actionable improvement suggestions.
<img width="1366" height="643" alt="image" src="https://github.com/user-attachments/assets/2cfa43ee-8f5b-4fe4-9fc2-d5334ec6f37e" />


🔗 **Live Demo:** https://lnkd.in/duEJw7dA  

---

## 🚀 Project Overview

Applicant Tracking Systems (ATS) are commonly used to parse, filter, and rank resumes during recruitment.

This project uses a **Large Language Model (LLM)** to simulate a structured resume-review workflow. A user uploads a resume, the application extracts its text, sends the content to **Google Gemini Flash**, and presents the model's analysis through an interactive Streamlit interface.

The project was developed as a hands-on skill-building project under the:

**Pak Angels × HEC-NCEAC Generative & Agentic AI Training Program — Cohort 11**

The goal was to move beyond theoretical Generative AI concepts and build a practical end-to-end application involving:

- LLM integration
- Prompt engineering
- Structured AI output
- Document processing
- Web application development
- API credential management
- GitHub-based version control
- Streamlit deployment

---

## ✨ Features

### 📤 Resume Upload

Supports:

- PDF
- DOCX
- TXT

For best results, upload a **text-based PDF** or DOCX file.

### 🤖 LLM-Powered Analysis

Google Gemini Flash evaluates the resume using a structured prompt designed for general ATS readiness.

### 📊 Estimated ATS Score

The application generates an estimated score from **0–100** with the following interpretation:

| Score | Assessment |
|---:|---|
| 90–100 | Excellent |
| 80–89 | Very Good |
| 70–79 | Good |
| 60–69 | Needs Improvement |
| 0–59 | Poor |

> ⚠️ The score is an **AI-generated estimate**, not an official score from a particular employer's ATS platform.

### 🔍 Resume Strengths

The model identifies positive aspects such as:

- Clear resume structure
- Relevant skills
- Searchable terminology
- Quantified achievements
- Concise bullet points
- Standard resume headings

### 🛠️ Actionable Improvements

The application returns improvement recommendations with:

- Priority
- Identified issue
- Recommendation
- Example wording

### 🔑 ATS Keywords

The model identifies potentially useful keywords already present or relevant to the resume.

### 📋 Formatting Checks

The application evaluates ATS-related formatting considerations and reports:

- Pass
- Needs Attention

### 🔄 Model Switching

The Gemini model can be changed directly from the **Streamlit sidebar**.

The default model is:

```text
gemini-3.7-flash
```

You can enter another model ID supported by your Gemini API account.

---

# 🏗️ Architecture

```text
                    ┌──────────────────────┐
                    │        User          │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │   Streamlit UI       │
                    │  Resume File Upload  │
                    └──────────┬───────────┘
                               │
                               ▼
                  ┌──────────────────────────┐
                  │    Document Processing   │
                  │                          │
                  │ PDF  → pypdf             │
                  │ DOCX → python-docx       │
                  │ TXT  → UTF-8 decoding    │
                  └────────────┬─────────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │  Prompt Engineering  │
                    │  + Resume Text       │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │    Google Gemini     │
                    │      Flash LLM       │
                    └──────────┬───────────┘
                               │
                         JSON Response
                               │
                               ▼
                  ┌──────────────────────────┐
                  │ JSON Parsing & Validation │
                  └────────────┬─────────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │   Results Dashboard  │
                    │                      │
                    │ ATS Score             │
                    │ Strengths             │
                    │ Improvements          │
                    │ Keywords              │
                    │ Formatting Checks     │
                    └──────────────────────┘
```

---

# 🧠 How the AI Analysis Works

The application sends the extracted resume text to Gemini with a structured prompt.

The prompt instructs the model to:

1. Evaluate general ATS readiness.
2. Avoid inventing candidate information.
3. Consider standard ATS-friendly headings.
4. Evaluate searchable keywords.
5. Look for measurable achievements.
6. Identify vague or weak bullet points.
7. Check clarity and structure.
8. Identify potential formatting concerns.
9. Produce actionable recommendations.
10. Return the result as structured JSON.

The expected response schema is approximately:

```json
{
  "ats_score": 82,
  "score_label": "Very Good",
  "summary": "The resume has a strong foundation...",
  "strengths": [
    "Clear professional summary",
    "Relevant technical skills"
  ],
  "improvements": [
    {
      "priority": "High",
      "issue": "Some bullets lack measurable outcomes",
      "recommendation": "Add metrics where possible",
      "example": "Reduced processing time by 25%..."
    }
  ],
  "ats_keywords": [
    "Python",
    "Machine Learning",
    "Data Analysis"
  ],
  "formatting_checks": [
    {
      "check": "Standard section headings",
      "status": "Pass",
      "comment": "Sections are clearly identifiable."
    }
  ]
}
```

The application also performs basic defensive validation before displaying the result.

---

# 🧰 Tech Stack

| Technology | Purpose |
|---|---|
| **Python** | Core application logic |
| **Streamlit** | Web UI and deployment |
| **Google Gemini Flash** | LLM-based resume analysis |
| **google-genai** | Gemini API integration |
| **pypdf** | PDF text extraction |
| **python-docx** | DOCX text extraction |
| **JSON** | Structured AI response handling |
| **GitHub** | Source control |
| **Streamlit Community Cloud** | Cloud deployment |

---

# 📁 Project Structure

```text
AI-Resume-ATS-Checker/
│
├── app.py
├── requirements.txt
├── README.md
│
└── .streamlit/
    └── secrets.toml       # Local only - DO NOT commit
```

---

# ⚙️ Installation & Setup

## 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
cd YOUR_REPOSITORY
```

## 2. Create a virtual environment

### Windows

```bash
python -m venv venv
venv\Scripts\activate
```

### macOS/Linux

```bash
python3 -m venv venv
source venv/bin/activate
```

## 3. Install dependencies

```bash
pip install -r requirements.txt
```

---

# 🔐 Configure Gemini API

The application reads the Gemini API key from either:

1. Streamlit Secrets
2. The `GEMINI_API_KEY` environment variable

## Option A — Streamlit Secrets

Create:

```text
.streamlit/secrets.toml
```

Add:

```toml
GEMINI_API_KEY = "YOUR_GEMINI_API_KEY"
```

**Never commit this file to GitHub.**

Add it to `.gitignore`:

```gitignore
.streamlit/secrets.toml
__pycache__/
*.pyc
venv/
.env
```

## Option B — Environment Variable

### Windows PowerShell

```powershell
$env:GEMINI_API_KEY="YOUR_GEMINI_API_KEY"
```

### macOS/Linux

```bash
export GEMINI_API_KEY="YOUR_GEMINI_API_KEY"
```

---

# ▶️ Run Locally

Start the Streamlit application:

```bash
streamlit run app.py
```

Streamlit will provide a local URL, typically:

```text
http://localhost:8501
```

---

# 🔄 Switching Gemini Models

The application provides a **Gemini model** field in the Streamlit sidebar.

For example:

```text
gemini-3.7-flash
```

To use another supported model, replace the value in the sidebar or configure:

```bash
GEMINI_MODEL=your-model-id
```

The application falls back to:

```python
DEFAULT_MODEL = "gemini-3.7-flash"
```

> Model availability, names, quotas, and rate limits can change. Check the current Google Gemini documentation before selecting a model for production use.

---

# ☁️ Deploy on Streamlit Community Cloud

## 1. Push the project to GitHub

Your repository should contain at least:

```text
app.py
requirements.txt
README.md
```

## 2. Open Streamlit Community Cloud

Go to:

https://share.streamlit.io/

Sign in using GitHub.

## 3. Create a new app

Select:

```text
Repository: YOUR_USERNAME/YOUR_REPOSITORY
Branch: main
Main file path: app.py
```

Then deploy.

## 4. Add the Gemini API key

In the deployed Streamlit app settings, open **Secrets** and add:

```toml
GEMINI_API_KEY = "YOUR_GEMINI_API_KEY"
```

Save the secrets and restart/redeploy the application.

---

# 🧪 Testing

Before deployment, perform these checks:

### Application test

```bash
streamlit run app.py
```

### Test PDF

Upload a normal text-based PDF resume.

### Test DOCX

Upload a `.docx` resume.

### Test TXT

Upload a `.txt` resume.

### Test missing API key

The application should show an API-key configuration error instead of crashing.

### Test empty/scanned PDF

Image-only PDFs may not contain extractable text. The application informs the user when no readable text is detected.

### Test model availability

If a selected Gemini model is unavailable or temporarily overloaded, try another supported model from the sidebar.

---

# ⚠️ Current Limitations

This project is intentionally a practical learning implementation and has several limitations.

### 1. ATS score is an estimate

There is no universal ATS scoring formula. Different ATS platforms and employers may use different parsing, matching, ranking, and screening logic.

### 2. General-purpose analysis

The current version evaluates the resume without a specific job description.

A future version could compare:

```text
Resume + Job Description
        ↓
Keyword Matching
        ↓
Skill Gap Analysis
        ↓
Job-Specific ATS Score
```

### 3. Image-only PDFs

Scanned/image-only PDFs may not produce usable text through standard PDF extraction.

OCR could be added in a future version.

### 4. LLM dependency

Analysis depends on Gemini API availability, model availability, quotas, and network connectivity.

### 5. No persistent database

The current application does not maintain a user account or permanent resume history.

---

# 🔮 Future Improvements

Potential next steps include:

- 🎯 Job-description-specific ATS scoring
- 🔎 Resume-to-job keyword matching
- 📊 Skill-gap analysis
- 🧠 Embedding-based semantic matching
- 📈 Resume scoring by individual categories
- 📄 AI-generated resume rewriting
- ✍️ Bullet-point improvement suggestions
- 📑 Resume template recommendations
- 🔐 User authentication
- 💾 Resume history/database
- 📥 Downloadable analysis reports
- 🧾 PDF report generation
- 👁️ OCR support for scanned resumes
- 🔄 More robust model fallback and retry handling
- 📊 Analytics dashboard
- 🤖 Agentic workflow for iterative resume optimization

---

# 🔒 Privacy & Security

A resume may contain personal information such as:

- Name
- Email
- Phone number
- Education
- Employment history
- Skills

The uploaded resume text is sent to the configured Gemini API for analysis.

**Do not upload sensitive information unless you are comfortable processing it through the configured AI service.**

Never expose your Gemini API key in:

- `app.py`
- GitHub repositories
- screenshots
- README files
- client-side code

Use Streamlit Secrets or environment variables instead.

---

# 📚 Learning Outcomes

This project provided practical experience with:

### Generative AI

- LLM API integration
- Prompt engineering
- Structured generation
- JSON-based model responses
- LLM error handling

### Python

- File processing
- PDF parsing
- DOCX parsing
- JSON handling
- Exception handling
- Type hints

### Application Development

- Streamlit UI development
- Session state
- File upload workflows
- Interactive model configuration

### Deployment

- GitHub repository management
- Dependency management
- Streamlit Community Cloud
- Secret management

---

# 🎓 Program & Acknowledgements

This project was developed as part of the:

**Pak Angels × HEC-NCEAC Generative & Agentic AI Training Program — Cohort 11**

Special thanks to:

- **Pak Angels (Silicon Valley, USA)**
- **PEC**
- **NCEAC-HEC**
- **iCodeGuru**
- **Aspire Pakistan**

And to the mentors who guided us throughout the cohort:

**Muhammad Anwar Khan, Dr. Zafar Shahid, Hassan Syed, Naeem Zafar, Muhammad Talha, Umaima Rizwan, Ayesha Andleeb, Rana Muhammad Moeen ud Deen, Muhammad Jawad, Mazhar Naseer, Zain Khan, Muhammad Raffay, and Sana Sajid.**

---

# 👨‍💻 Author

**Qaisar Khan**

This project represents hands-on practice in **Generative AI, LLM application development, Python, and AI-powered career technology**.

---

# 📌 Disclaimer

This project is intended for **educational, experimentation, and skill-building purposes**.

The ATS score and recommendations are generated by an AI model and should not be treated as an official assessment from an employer, recruiter, or Applicant Tracking System.

---

## ⭐ If you find this project useful

Consider giving the repository a ⭐ on GitHub and sharing feedback or ideas for future improvements.

**Built with Python 🐍 + Streamlit ⚡ + Gemini 🤖**
