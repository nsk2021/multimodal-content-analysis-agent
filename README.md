# Multi-Modal Content Analysis Agent (FlightAI)

This project demonstrates a **multi-modal, function-calling AI agent** for airline customer support. The agent can ingest **text, audio, and image** inputs, classify the request, call tools when needed (example: ticket price lookup), and return a **1-sentence support response**.

This repo is tailored to the resume project framing: **function-calling**, **multi-modal processing**, and **automated resolution** for complex content evaluation queries.

## What it does

- **Multi-modal inputs**
  - Text: direct user message
  - Audio: speech-to-text transcription, then analysis
  - Image: vision analysis for support context (ex: damaged luggage tag)

- **Content analysis output (structured JSON)**
  - intent: pricing | booking_change | baggage | policy | complaint | other
  - urgency: low | medium | high
  - sentiment: positive | neutral | negative
  - needs_tool + tool_args: if a tool lookup is required
  - final_reply: one sentence

- **Tool calling**
  - Example tool: `get_ticket_price(destination_city)` backed by a tiny local SQLite DB.

## Quickstart

### 1) Install
```bash
python -m venv .venv
source .venv/bin/activate
pip install -U openai python-dotenv gradio pillow
```

### 2) Configure env
Create `.env`:
```bash
OPENAI_API_KEY="YOUR_KEY_HERE"
# Optional overrides:
# OPENAI_MODEL="gpt-4o-mini"
# OPENAI_STT_MODEL="whisper-1"
```

### 3) Run the notebook
Open `multimodal-content-analysis-agent.ipynb` in Jupyter/VSCode and run all cells.

The last cell launches a Gradio UI where you can provide:
- a text message
- optionally an image file
- optionally an audio file

## Notes

- No secrets are committed: API keys are loaded from environment variables.
- The SQLite DB is created locally (`flightai.db`) when the notebook runs.
