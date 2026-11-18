# LangChain Tutorial: Groq, Ollama, LangServe and RAG

Learning project working through LangChain basics: a Streamlit chatbot on a cloud LLM (Groq) and on a local LLM (Ollama), serving chains as a REST API with LangServe/FastAPI, and a simple retrieval-augmented generation (RAG) pipeline.

## Project structure
```
chatbot/
  app.py        Streamlit chatbot using Groq (llama-3.3-70b-versatile)
  localama.py   Same chatbot using a local Ollama model (gemma3:1b)
api/
  app.py        FastAPI + LangServe server exposing Groq and Ollama chains
  client.py     Streamlit client that calls the API
rag/
  simplerag.ipynb  Load text, web and PDF documents, split them, embed with
                   BAAI/bge-base-en-v1.5 and store/query them in Chroma
  speech.txt       Sample text document for the loader
```
The API part is also published on its own as [Deployment-LLM-As-API](https://github.com/Einooo/Deployment-LLM-As-API).

## Setup
```bash
python -m venv venv
venv\Scripts\activate        # Windows
pip install -r requirements.txt
copy .env.example .env       # then put your own keys in .env
```
- `GROQ_API_KEY`: from https://console.groq.com
- `LANGCHAIN_API_KEY`: from LangSmith (optional, for tracing)
- For the local model, install [Ollama](https://ollama.com) and run `ollama pull gemma3:1b`.
- For the RAG notebook, download the paper "Attention Is All You Need" (https://arxiv.org/abs/1706.03762) and save it as `rag/attention.pdf`.

## Run
```bash
streamlit run chatbot/app.py         # Groq chatbot
streamlit run chatbot/localama.py    # Ollama chatbot
python api/app.py                    # API on http://localhost:8000 (docs at /docs)
streamlit run api/client.py          # client for the API (start the API first)
```
