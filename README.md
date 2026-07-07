# Multi-Agent PR Automator 🤖🚀

An autonomous, multi-agent code analysis pipeline built with **CrewAI** and powered by the **Gemini 2.5 Flash** LLM. This system mimics an enterprise code review workflow by automatically checking incoming scripts for severe security vulnerabilities (like hardcoded production credentials) and compiling structured, production-grade Pull Request (PR) summaries directly into Markdown.

---

## 🎯 Project Overview & Architecture

Instead of relying on rigid, rule-based static code analysis tools, this project utilizes an intelligent, sequential multi-agent architecture to contextualize code reviews and generate human-readable engineering reports.

```
[ Vulnerable Code Input ]
          │
          ▼
┌─────────────────────────────────┐
│     Senior Code Reviewer        │ ◄── Powered by Gemini 2.5 Flash
│ (Flags security risks & bugs)   │
└────────────────┬────────────────┘
                  │  (Raw Analysis Data)
                  ▼
┌─────────────────────────────────┐
│        Technical Writer         │ ◄── Powered by Gemini 2.5 Flash
│  (Structures Markdown Format)   │
└────────────────┬────────────────┘
                  │
                  ▼
        [ PR_SUMMARY.md Saved ]
```

### 👥 The AI Agents Crew

1. **Senior Code Reviewer** — Specialized agent tasked with diving into the source code, detecting syntax issues, spotting logical anti-patterns, and flagging critical security vulnerabilities (e.g., hardcoded API keys or credentials).
2. **Technical Writer** — Specialized documentation agent that takes raw analysis findings and structures them into clear, industry-standard pull request documentation.

---

## 🛠️ Technologies & Stack

- **Framework:** CrewAI (JSON-first declarative layout)
- **LLM Engine:** Google Gemini 2.5 Flash (utilizing advanced native thinking capabilities)
- **Language:** Python 3.13+
- **Environment & Packages:** `uv` package manager, python-dotenv, LiteLLM

---

## 📁 Repository Structure

```text
├── agents/                  # Declarative AI Agent definitions (JSONC format)
│   ├── senior_code_reviewer.jsonc
│   └── technical_writer.jsonc
├── tasks/                    # Task assignments and expected output configurations
├── crew.jsonc                # Central pipeline blueprint connecting agents and tasks
├── PR_SUMMARY.md              # The automated production-grade output file
├── .env.example                # Safe public template for environment configuration
└── pyproject.toml               # Core project dependencies managed via uv
```

---

## 🚀 Quick Start & Installation

### Prerequisites

Make sure you have the fast [`uv`](https://github.com/astral-sh/uv) package manager installed on your machine.

### 1. Clone & Navigate

```bash
git clone https://github.com/mohammedfkhan/Multi-Agent-PR-Automator.git
cd Multi-Agent-PR-Automator
```

### 2. Configure Environment Variables

Create a local `.env` file in the root directory:

```bash
cp .env.example .env
```

Open `.env` and provide your actual Gemini API credentials:

```env
MODEL=gemini/gemini-2.5-flash
GEMINI_API_KEY=your_actual_gemini_api_key_here
```

### 3. Install Dependencies

Install the required packages, including the Google GenAI native extensions:

```bash
uv add "crewai[google-genai]"
```

### 4. Execute the Pipeline

Run the multi-agent automation crew locally:

```bash
crewai run
```

---

## 📊 Example Output

When a single-line script containing vulnerable hardcoded credentials is fed into the system:

```python
def connect_to_database(username, password):
    admin_user = "root"
    admin_pass = "password123"
    return True
```

The pipeline automatically compiles and creates a local `PR_SUMMARY.md` containing:

- **Security Alarms:** High-priority warnings flagging hardcoded root strings.
- **Analysis Matrix:** Clean markdown tables organizing bug locations and severity.
- **Refactored Code Block:** Clean, production-grade alternatives implementing secure runtime configurations.
