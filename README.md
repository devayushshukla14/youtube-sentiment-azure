# YouTube Comment Sentiment Analysis Pipeline

An end-to-end real-time NLP pipeline that captures live YouTube comments, analyzes sentiment using Hugging Face Transformers and rule-based logic, and stores the processed data on Azure Blob Storage for further analysis via CSV or Tableau dashboards.

---

## Architecture Overview

```mermaid
graph LR
    A[YouTube Comment Fetcher] --> B[Azure Event Hub]
    B --> C[Azure Stream Analytics]
    C --> D[Azure Blob Storage]
    D --> E[CSV Output or Tableau Dashboard]
```
## Tech Stack

- **Python** (YouTube API client, Sentiment Analysis, Event Hub producer)
- **Hugging Face Transformers** (`distilbert-base-uncased-finetuned-sst-2-english`)
- **Azure Event Hub** (Real-time event ingestion)
- **Azure Stream Analytics** (Stream processing with SQL-like queries)
- **Azure Blob Storage** (Output sink for processed comment data)
- **Rule-Based Classifier** (Basic logic on keywords)

## How It Works

1. **YouTube Comment Fetcher (Python Script)**  
   - Connects to the YouTube Data API to fetch the latest comments from a given video (`
Mission: Impossible – The Final Reckoning | Official Trailer (2025 Movie)`).
   - For each comment:
     - Performs **sentiment analysis** using a **Hugging Face transformer model** (`hf_sentiment`).
     - Also applies a **rule-based sentiment classifier** (`rule_sentiment`).
   - Sends the enriched comment data as JSON messages to **Azure Event Hub**.

2. **Azure Event Hub**  
   - Acts as a **real-time event streaming platform**.
   - Receives the incoming comment events and holds them briefly for processing.

3. **Azure Stream Analytics**  
   - Subscribes to Event Hub as an input source.
   - Uses a SQL-like query to project and clean the data.
   - Writes the processed output to **Azure Blob Storage** in real time.

4. **Azure Blob Storage**  
   - Stores the results as **JSON files**, partitioned by date and time.
   - Files are named and structured by timestamp for easy retrieval.

5. **CSV Conversion & Tableau Visualization**  
   - JSON output is downloaded and converted to a **CSV file** manually or via script.
   
---

## Azure Stream Analytics Job overview

**Input Details**
![Screenshot 2025-05-31 192219](https://github.com/user-attachments/assets/494669e9-e510-456d-a6f1-c1d788a1d575)

**Output Details**
![Screenshot 2025-05-31 192257](https://github.com/user-attachments/assets/d0cda87a-82e4-43aa-ad85-93f6d5265b56)

**Query**
![Screenshot 2025-05-31 192341](https://github.com/user-attachments/assets/318d1b03-8c60-46b6-8c83-47ab91adf6d8)
    - Since I was trying to explore Azure I just copied all input into output

## Data Visualization
![image](https://github.com/user-attachments/assets/3a2e1d5b-1398-494c-a4cb-8212b83c0aa5)

![image](https://github.com/user-attachments/assets/2d73c4c3-cbdc-41c5-a48c-7dd43746ba8e)

![image](https://github.com/user-attachments/assets/1e38fe37-648c-4728-b992-e4448d1afac3)

![image](https://github.com/user-attachments/assets/97607f87-5258-42af-a854-d3576559eb72)


