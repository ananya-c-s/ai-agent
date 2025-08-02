# 🧠 AI Referral Message Generator

A lightweight, offline‑capable AI agent that generates personalized LinkedIn‑style **referral request messages** using [LangChain](https://www.langchain.com/) and [Ollama](https://ollama.com/). This tool extracts relevant details from candidate and referrer profiles to write a professional, tailored message — **no OpenAI API key required**.

---

## 📌 Features

* ✅ Automatically extracts names, roles, organizations, and skills from two profile files
* ✅ Writes a concise, customized referral pitch in **under 100 words**
* ✅ Works **completely offline** with local LLMs like `llama3`, `mistral`, and `phi`
* ✅ Built with [LangGraph](https://www.langchain.com/langgraph) for clear, modular graph logic
* ✅ Uses the updated [`langchain-ollama`](https://pypi.org/project/langchain-ollama/) integration (no deprecation warnings)

---

## 🚀 Quick‑start Checklist

1. **Install Python deps**  → `pip install -r requirements.txt`
2. **Install Ollama** (macOS / Windows / Linux)  → [https://ollama.com/download](https://ollama.com/download)
3. **Download & run a model**  → `ollama run llama3`
4. Place your profile txt files in `./profiles/`
5. **Run the agent**  → `python agent/agent.py`

---

## 🛠 Full Setup Instructions

### 1. Create & activate a virtual environment (optional but recommended)

```bash
python -m venv .venv
source .venv/bin/activate  # Linux/macOS
# or
.venv\Scripts\activate    # Windows PowerShell
```

### 2. Install Python dependencies

```bash
pip install langchain langchain-community langchain-ollama python-dotenv
```

*(or simply `pip install -r requirements.txt` – see file below)*

### 3. Install **Ollama**

1. Download from [https://ollama.com/download](https://ollama.com/download) and follow the installer for your OS.
2. Confirm it works:

```bash
ollama --version   # prints version number
```

### 4. 🔥 **Run / Pull LLM models with Ollama**

> Ollama automatically downloads a model the first time you `run` it. You can also pre‑pull specific versions.

```bash
# Option A: One‑shot run (downloads if missing, then starts REPL)
ollama run llama3             # default 8‑billion‑parameter Llama 3

# Option B: Explicitly pull, then run
ollama pull llama3:8b         # pull a specific variant
ollama list                   # verify the model is downloaded
ollama run llama3:8b          # run it

# Try a lighter model if RAM‑constrained
ollama run phi

# Keep Ollama running as a background service (optional)
ollama serve &                # Unix/Mac – launches REST API on :11434
```

**💡 Tip:**  If you host Ollama on another machine or port, set `OLLAMA_BASE_URL` in `.env` (see below).

### 5. Prepare your profile files

```
profiles/
├── profile1.txt   # Referrer (Receiver)
└── profile2.txt   # Candidate (You)
```

Each file should contain résumé‑style or LinkedIn‑style text.

### 6. Run the agent

```bash
python agent/agent.py
```

You should see output similar to:

```
Referral Pitch
Hi Priya,

I noticed your work on high‑scale data systems at Amazon. With five years of experience building Java‑Kafka microservices on AWS, I’m excited about the AI Engineer opening on your team. Would you be willing to refer me?

– Ananya
```

---

## ⚙️ Optional `.env` Configuration

Create a `.env` file to override defaults without editing code:

```env
# Profile filenames
CANDIDATE_PROFILE=profile2.txt
RECEIVER_PROFILE=profile1.txt

# Which local model Ollama should use
MODEL_NAME=llama3:8b

# Point to a remote/alternate Ollama host (default is http://localhost:11434)
OLLAMA_BASE_URL=http://127.0.0.1:11434
```

The script reads these values via `python‑dotenv`.

---

## 🗂 Project Structure

```
.
├── agent/
│   └── agent.py               # Main LangGraph logic
├── profiles/
│   ├── profile1.txt           # Referrer profile
│   └── profile2.txt           # Candidate profile
├── requirements.txt           # Python dependencies
├── .env                       # (Optional) runtime config
└── README.md                  # You are here
```

---

## 📜 requirements.txt

```text
langchain>=0.1.14
langchain-community>=0.0.30
langchain-ollama>=0.0.6
python-dotenv>=1.0.1
```

Install all deps with:

```bash
pip install -r requirements.txt
```

---

## ❓ Troubleshooting

| Issue                                     | Solution                                                                        |
| ----------------------------------------- | ------------------------------------------------------------------------------- |
| `ModuleNotFoundError`                     | Activate the virtualenv and reinstall packages.                                 |
| `LangChainDeprecationWarning: ChatOllama` | Ensure you're importing from `langchain_ollama`, **not** `langchain_community`. |
| `Connection refused at 11434`             | Run `ollama run llama3` (or `ollama serve`) before starting the agent.          |
| High RAM usage                            | Use a smaller model: `phi`, `tinydolphin`, or `llama3:8b‑q4_K_M`.               |

---

## 🧑‍💻 To Do

* [ ] CLI interface for quick prompts
* [ ] Web UI (FastAPI / Streamlit)
* [ ] Job description parsing & matching
* [ ] Tone/style selectors (friendly / formal / enthusiastic)

---
* [ ] Job description parsing & matching
* [ ] Tone/style selectors (friendly / formal / enthusiastic)

---