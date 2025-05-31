# YouTube Comment Sentiment Analysis Pipeline

An end-to-end real-time NLP pipeline that captures live YouTube comments, analyzes sentiment using Hugging Face Transformers and rule-based logic, and stores the processed data on Azure Blob Storage for further analysis via CSV or Tableau dashboards.

---

## 🚀 Architecture Overview

```mermaid
graph LR
    A[YouTube Comment Fetcher] --> B[Azure Event Hub]
    B --> C[Azure Stream Analytics]
    C --> D[Azure Blob Storage]
    D --> E[CSV Output or Tableau Dashboard]
