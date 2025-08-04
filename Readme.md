# FinAdvisor – Digital Financial Literacy Agent

> **Status:** Proof-of-Concept  |  IBM Cloud Lite deployment

## Table of Contents

1. Problem Statement
2. Solution Overview
3. Key Features
4. Architecture
5. IBM Cloud Services Used
6. Prerequisites
7. Local Setup \& Project Structure
8. Deploying on IBM Cloud
9. Using the API / Web Chat
10. Customisation
11. Road-map
12. Contributing
13. License
14. Contact

## 1. Problem Statement

Indian citizens are adopting digital payments at record speed, yet large sections of the population lack clear, trustworthy guidance on:

* Safely using UPI, IMPS, NEFT and RuPay cards.
* Spotting OTP, QR-code and phishing scams.
* Understanding RBI regulations, interest-rate mechanics and government welfare schemes.

Traditional awareness campaigns cannot scale to 1.4 billion people or 22+ major languages.

## 2. Solution Overview

**FinAdvisor** is an Agentic-AI assistant that delivers India-specific, multilingual financial-literacy support.
The agent is built in IBM watsonx.ai **Agent Lab** using the **Granite** foundation model and a Retrieval-Augmented Generation (RAG) workflow over RBI / NPCI / GOI documents.

## 3. Key Features

* **Multilingual Q\&A** – English, Hindi and other Indic languages.
* **RAG-powered accuracy** – cites only trusted Indian sources.
* **Fraud-shield** – proactively warns against common scams.
* **24 × 7 availability** – served via a REST endpoint and embeddable chat widget.
* **Low-code development** – created entirely inside IBM Cloud Lite.


## 4. Architecture

```text
User (Web / Mobile)
        │
        ▼
 FinAdvisor Agent (Agent Lab, ReAct + LangGraph)
        │
 ┌────────────┐
 │  Gran   ite│  ← Foundation model, tuned
 └────────────┘
        │
 Vector Index (in-memory PoC)  ← RBI / NPCI PDFs
        │
Cloud Object Storage  ← project assets & logs
        │
Deployment Space (Online AI Service)
```


## 5. IBM Cloud Services Used

| Service | Purpose | Plan |
| :-- | :-- | :-- |
| **watsonx.ai Studio** | Low-code Agent design \& Prompt Lab | Lite |
| **watsonx.ai Runtime** | Model inference | Lite |
| **Cloud Object Storage** | Store PDFs, chat logs, vector files | Lite |
| **Deployment Space** | One-click REST deployment | Lite |

## 6. Prerequisites

* IBM Cloud Lite account.
* IBM Cloud CLI (optional for API calls).
* Python 3.10+ for local utilities (vectorisation, testing).


## 7. Local Setup \& Project Structure

```text
finadvisor/
├─ data/               # RBI / NPCI PDFs
├─ notebooks/          # Optional Jupyter analysis
├─ src/
│  ├─ ingest.py        # Convert PDFs → chunks
│  ├─ vectorise.py     # Create local vector store (dev only)
│  └─ api_demo.py      # Sample REST consumer script
└─ README.md
```

Clone the repo, create a virtual-env, install deps and run `python src/ingest.py` to reproduce the local vector store for testing.

## 8. Deploying on IBM Cloud

1. **Create Project** in watsonx.ai Studio.
2. **Attach Cloud Object Storage** (Lite).
3. **Associate watsonx.ai Runtime**.
4. **Agent Lab → New Agent**.
    * Select **Granite (gpt-neo-14b-instruct) or mistral-large**.
    * Upload PDFs via **Knowledge → New Vector Index**.
    * Add built-in **Google / Wiki search** tools if wider web recall is required.
5. **Save as Agent Asset**.
6. **Deploy as Online AI Service** into a new Deployment Space.
7. Copy the **API key** and endpoint for integration.

## 9. Using the API / Web Chat

* **Chat UI** – open the *Preview* tab in the deployment.
* **REST** – POST JSON to `{deployment_url}/ai_service?version=2021-05-01` with:

```jsonc
{
  "input": { "text": "UPI daily limit?" },
  "parameters": { "decoding_method": "greedy", "max_new_tokens": 128 }
}
```

Include the `Authorization: Bearer <IAM_TOKEN>` header obtained via IBM Cloud CLI or API.

## 10. Customisation

* **Add Documents** – upload more PDFs and rebuild the vector index.
* **Language Expansion** – fine-tune Granite on additional Indic datasets.
* **Persistent Vector Store** – switch to **Milvus** or **watsonx.data** for scale.
* **Frontend** – embed the REST call in React / Android mini-app.


## 11. Road-map

* Voice interface via Watson Speech-to-Text / Text-to-Speech.
* Push notifications for RBI circulars.
* Real-time fraud-alert feed integration.
* Analytics dashboard for usage \& impact metrics.


## 12. Contributing

Pull requests are welcome! Please open an issue first to discuss major changes.
Make sure your code follows **PEP-8** and includes unit tests.

## 13. License

This project is released under the MIT License – see `LICENSE` for details.

## 14. Contact

*Project Lead* – \<Your Name\>
*Email* – \<your-email@example.com\>

> *Built with ☁️ \& ♥ on IBM Cloud Lite*

<div style="text-align: center">⁂</div>

[^1]: SB4Academia_Problem-Statements_2025-1.pdf

[^2]: Agentic-AI-on-IBM-Cloud-2.pdf

[^3]: Project-template-for-AI-Agent-case-study.pptx


