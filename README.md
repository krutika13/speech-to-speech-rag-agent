# 🗣️ Conversational AI Call Center Agent (RAG-based MVP)

This project is a functional **speech-to-speech AI agent** prototype designed for call centers. It uses **Retrieval-Augmented Generation (RAG)** to ground answers in domain-specific knowledge and simulates a voice conversation by combining **speech-to-text**, **RAG-based question answering**, and **text-to-speech**. The project demonstrates local LLM usage, vector search, and end-to-end conversational flow with a Gradio UI.

---

## 🎯 Objectives

- Build a local RAG pipeline using LangChain
- Enable users to speak to an AI agent and receive human-like audio responses
- Integrate Whisper (STT) and Coqui TTS for audio handling
- Optionally extend to a digital twin with avatar UI (future scope)

---

## 🛠️ Tech Stack & Tools

| Component        | Tool / Library                               |Purpose                                   |
|------------------|--------------------------------------------- |------------------------------------------|
| LLM              | TinyLlama 1.1B                               | Lightweight local language model         |
| Embeddings       | all-MiniLM-L6-v2 (HuggingFace)               | Sentence-level vector representation     |
| Vector Store     | FAISS                                        | Fast approximate nearest neighbor search |
| RAG Framework    | LangChain                                    | End-to-end QA system                     |
| STT              | OpenAI Whisper                               | Converts voice input to text             |
| TTS              | Coqui TTS (Tacotron2-DDC)                    | Converts text to spoken audio            |
| UI               | Gradio                                       | Interactive speech-based interface       |

---

## 🧠 RAG Flow Overview

1. User speaks into mic → converted to text using Whisper
2. LangChain retrieves top-k relevant chunks from a vector DB
3. A HuggingFace LLM (TinyLlama) generates a response
4. Response is converted back to speech using TTS
5. Audio response is returned via Gradio

---

## 🗂️ Dataset

A publicly availble pdf was used as the domain-specific knowledge base. The text is:

- Loaded and chunked using LangChain's `RecursiveCharacterTextSplitter`
- Embedded with `all-MiniLM-L6-v2`
- Stored in a FAISS vector store

---

## ⚙️ Setup Instructions

```bash
# Step 1: Install dependencies
pip install openai-whisper TTS gradio sentence-transformers faiss-cpu langchain transformers accelerate torch langchain-community

# Step 2: Run the script
python rag_callcenter.py  # or run all cells in the Jupyter Notebook


##🧩 Architecture Diagram
User Speech
   ↓
Whisper (STT)
   ↓
LangChain RAG → FAISS + TinyLlama
   ↓
Text Answer
   ↓
Coqui TTS
   ↓
Audio Reply
