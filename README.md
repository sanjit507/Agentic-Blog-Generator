# Blog Writing Agent

A production-style AI blog generation system built with LangGraph, Streamlit, Gemini, and Tavily. The app takes a topic, plans a blog structure, optionally performs web research, writes the content section by section, and can generate supporting images for the final article.

<img width="1082" height="469" alt="Screenshot 2026-08-01 160417 (1)" src="https://github.com/user-attachments/assets/91b19c6c-7057-4554-988c-12096fe2b406" />


Full Explain of Code Click Here https://csestudy247.com/docs/building-an-agentic-blog-writing-system-with-langgraph-groq-and-streamlit/

## What this project does

This project turns a simple prompt like “Explain RAG for developers” into a complete technical blog draft in Markdown. It uses an agent workflow to:

- decide whether web research is needed
- plan the blog outline
- gather supporting evidence from the web
- write the article in sections
- optionally generate images and place them in the final Markdown

The result is a polished blog draft that can be reviewed, edited, and exported.

## Main features

- End-to-end blog generation from a single topic
- Smart routing between closed-book and research-assisted modes
- Optional web research with Tavily
- Structured planning with task-based outline generation
- Section-by-section writing for a more coherent article
- Image planning and image generation using Gemini
- Modern Streamlit UI for generating and previewing blog posts
- Support for loading previously generated Markdown blogs

## Tech stack

- Python
- LangGraph for workflow orchestration
- LangChain for LLM integration
- Google Gemini for writing and image generation
- Tavily for web research
- Streamlit for the web UI
- Pydantic for structured outputs

## Project files

- [backend.py](bwa_backend.py) — the LangGraph workflow and blog generation logic
- [frontend.py](bwa_frontend.py) — the Streamlit user interface
- [requirements.txt](requirements.txt) — Python package dependencies

## How the system works



<img width="1024" height="1536" alt="ChatGPT Image Aug 1, 2026, 02_57_35 PM" src="https://github.com/user-attachments/assets/24ecc9b0-024a-4ec4-bde6-a456ba95cccb" />



The backend uses a graph-based workflow with these stages:

1. Router
   - Decides whether the topic needs research
   - Chooses a mode such as closed-book, hybrid, or open-book

2. Research
   - Runs Tavily searches if research is needed
   - Collects evidence for the article

3. Orchestrator
   - Creates a detailed blog plan with tasks, goals, and target word counts

4. Worker
   - Writes each section of the blog in Markdown

5. Reducer / image stage
   - Merges sections into one final article
   - Decides whether images are useful
   - Generates images and inserts them into the Markdown

## Prerequisites

Make sure you have:

- Python 3.10+ installed
- A Google AI API key for Gemini
- A Tavily API key for web research

## Environment variables

Create a `.env` file in the project root or in the parent directory of the workspace and add:

```env
GOOGLE_API_KEY=your_google_gemini_key
TAVILY_API_KEY=your_tavily_key
```

The backend is already set up to load a workspace-root `.env` file automatically.

## Installation

From the project folder, run:

```bash
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```

On macOS or Linux, use:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## How to run the app

Start the Streamlit app:

```bash
streamlit run frontend.py
```

Then:

1. Enter a blog topic in the text area
2. Choose an as-of date
3. Click “Generate Blog”
4. Review the plan, evidence, markdown preview, and generated images

## Output files

When the app runs, it will generate:

- a Markdown file named after the blog title in the project root
- an images folder containing generated image assets when applicable

## Example usage

Example topic:

```text
How vector databases improve RAG systems
```

The agent may:

- research recent developments
- create a structured outline
- write an article with sections such as architecture, trade-offs, and practical examples
- add relevant images if the model decides they improve clarity

## Notes

- If the Tavily API key is missing, the app can still generate a blog in a closed-book mode, but it will have less external grounding.
- If the Google API key is missing, writing and image generation will fail until the key is configured.
- The generated blog is meant to be a strong draft that can be refined further by the user.

## Suggested next improvements

- Add export to PDF or DOCX
- Add support for custom writing styles or brand voices
- Add persistent blog history in a database
- Improve image fallback and quality controls
- Add user authentication or multi-user support
