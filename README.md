# Multi_Agent_Search_System_Python-ML
# 🔬 ResearchMind — Multi-Agent AI Research Assistant

ResearchMind is a multi-agent AI system that researches any topic end-to-end: it searches the web, reads the most relevant source in depth, writes a structured report, and critiques its own output — all through a Streamlit interface.

## How it works

```
Topic
  │
  ▼
[1] Search Agent   → Tavily web search, gathers titles/URLs/snippets
  │
  ▼
[2] Reader Agent   → picks the most relevant URL, scrapes full page content
  │
  ▼
[3] Writer Chain   → drafts a structured report (Intro, Key Findings, Conclusion, Sources)
  │
  ▼
[4] Critic Chain   → scores the report, lists strengths & areas to improve
  │
  ▼
Final Report + Feedback (downloadable as .md)
```

## Tech Stack

- **UI:** Streamlit
- **Orchestration:** LangChain (`langchain.agents.create_agent`), LangGraph
- **LLM:** Groq — `llama-3.1-8b-instant`
- **Web Search:** Tavily API
- **Scraping:** Requests + BeautifulSoup4

## Prerequisites

- Python 3.11+
- A [Groq API key](https://console.groq.com/keys)
- A [Tavily API key](https://app.tavily.com/)

## Setup

```bash
# 1. Clone / open the project folder
cd Multi_Agent

# 2. Create a virtual environment
python -m venv .venv

# 3. Activate it
.venv\Scripts\Activate.ps1        # Windows PowerShell
# .venv\Scripts\activate.bat      # Windows cmd
# source .venv/bin/activate       # macOS/Linux

# 4. Install dependencies
pip install -r requirements.txt

# 5. Add your API keys — create a .env file in the project root:
```

`.env`:
```
GROQ_API_KEY=your_groq_api_key_here
TAVILY_API_KEY=your_tavily_api_key_here
```

## Run

**Streamlit UI (recommended):**
```bash
streamlit run app.py
```

**CLI (no UI, prints each step to terminal):**
```bash
python pipeline.py
```

## Project Structure

```
Multi_Agent/
├── app.py             # Streamlit UI + pipeline orchestration
├── agents.py           # Agent/chain definitions (search, reader, writer, critic)
├── pipeline.py          # CLI entry point — runs the full pipeline sequentially
├── tools.py             # Tools used by agents: web_search (Tavily), scrape_url (BS4)
├── requirements.txt      # Python dependencies
└── .env                # API keys (not committed to version control)
```

## Environment Variables

| Variable          | Description                          |
|-------------------|---------------------------------------|
| `GROQ_API_KEY`    | API key for Groq LLM inference        |
| `TAVILY_API_KEY`  | API key for Tavily web search         |

## Known Limitations

- Reader agent scrapes only **one** URL per query (the one it judges most relevant).
- Scraping can fail on JavaScript-heavy pages (BeautifulSoup doesn't render JS).
- No memory across queries — each run is independent.

## Possible Improvements

- Scrape and synthesize multiple sources instead of one
- Export report as PDF in addition to Markdown
- Add caching to avoid re-searching the same topic
- Stream agent output live instead of waiting for each step to finish

## License

MIT (or update as needed).
