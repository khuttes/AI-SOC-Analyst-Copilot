# AI-SOC-Analyst-Copilot
This project is a Local-First Security Operations Center (SOC) Assistant. It is designed to ingest security logs, store them locally, and use Artificial Intelligence (AI) to help you analyze them—all without sending sensitive data to the cloud.


# 🛡️ AI SOC Analyst Copilot

[![Local-First](https://img.shields.io/badge/Privacy-Local--First-blueviolet)](#-features--benefits)
[![Python 3.9+](https://img.shields.io/badge/Python-3.9%2B-blue)](https://www.python.org/)
[![React](https://img.shields.io/badge/Frontend-React-61DAFB)](https://reactjs.org/)
[![Ollama](https://img.shields.io/badge/AI-Ollama/Llama3-orange)](https://ollama.com/)

A **Local-First Security Operations Center (SOC) Assistant** designed to ingest, normalize, and analyze security logs locally. Using Retrieval-Augmented Generation (RAG), it provides context-aware AI analysis without ever sending sensitive data to the cloud.

---

## 🏗️ System Architecture & Logic Flow

The following diagram illustrates how data flows from raw log ingestion to AI-powered insights.

```mermaid
graph TD
    subgraph "A. Ingestion Phase (The Eyes)"
        Watcher[File Watcher: watchdog] -->|Event Trigger| Processor[Log Processor]
        Processor --> Parser{Parser Factory}
        Parser -->|.json| JSON[Structured Object]
        Parser -->|.log| Regex[Regex Pattern]
        JSON & Regex --> Norm[Normalization]
        Norm -->|Save| SQLite[(SQLite: security_logs)]
    end

    subgraph "B. Analysis Phase (The Brain)"
        Request[Analysis Request] --> RAG[RAG Engine]
        RAG <-->|Search| Chroma[(ChromaDB: MITRE/Sigma)]
        RAG --> Prompt[Prompt Construction]
        Prompt --> Ollama[Local LLM: Llama 3]
        Ollama --> Report[AI Analysis Report]
    end

    subgraph "C. Interface (The Face)"
        UI[React/Vite Dashboard] -->|Poll| API[Backend API]
        API --> UI
        UI -->|View| Report
    end



import os

def create_readme():
    content = """# 🛡️ AI SOC Analyst Copilot

[![Local-First](https://img.shields.io/badge/Privacy-Local--First-blueviolet)](#-features--benefits)
[![Python 3.9+](https://img.shields.io/badge/Python-3.9%2B-blue)](https://www.python.org/)
[![React](https://img.shields.io/badge/Frontend-React-61DAFB)](https://reactjs.org/)
[![Ollama](https://img.shields.io/badge/AI-Ollama/Llama3-orange)](https://ollama.com/)

A **Local-First Security Operations Center (SOC) Assistant** designed to ingest, normalize, and analyze security logs locally. Using **Retrieval-Augmented Generation (RAG)**, it provides context-aware AI analysis without ever sending sensitive data to the cloud.

---

## 🏗️ System Architecture & Logic Flow

The following diagram illustrates the lifecycle of a log entry, from file detection to AI analysis.

```mermaid
graph TD
    subgraph "A. Ingestion Phase (The Eyes)"
        Watcher[File Watcher: watchdog] -->|Event Trigger| Processor[Log Processor]
        Processor --> Parser{Parser Factory}
        Parser -->|.json| JSON[Structured Object]
        Parser -->|.log| Regex[Regex Pattern]
        JSON & Regex --> Norm[Normalization]
        Norm -->|Save| SQLite[(SQLite: security_logs)]
    end

    subgraph "B. Analysis Phase (The Brain)"
        Request[Analysis Request] --> RAG[RAG Engine]
        RAG <-->|Search| Chroma[(ChromaDB: MITRE/Sigma)]
        RAG --> Prompt[Prompt Construction]
        Prompt --> Ollama[Local LLM: Llama 3]
        Ollama --> Report[AI Analysis Report]
    end

    subgraph "C. Interface (The Face)"
        UI[React/Vite Dashboard] -->|Poll| API[Backend API]
        API --> UI
        UI -->|View| Report
    end
