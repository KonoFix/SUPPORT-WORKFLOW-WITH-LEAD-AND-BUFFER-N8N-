# AI Support Agent 

## Overview

This project consists of a high-complexity automation workflow developed in **n8n** to serve as a customer support agent 
The system uses **OpenAI** (LLMs), **Supabase** (PostgreSQL), and **Redis** to create a responsive, context-aware WhatsApp bot capable of handling text, audio, and image inputs seamlessly.

## Key Features

* **Multi-Modal Intelligence:**
    * **Text:** Context-aware conversations using LangChain agents.
    * **Audio:** Automatic transcription of voice notes using OpenAI Whisper (via API).
    * **Vision:** Image analysis to identify device defects or context using GPT-4o.
* **Smart Buffering:** Utilizes **Redis** to aggregate multiple rapid messages from a user into a single context, preventing fragmented bot responses.
* **User Management:** Automatically checks and registers users in **Supabase** to maintain conversation history and client data.
* **Safety & Filtering:** Includes logic to ignore groups, broadcasts, and handle offensive content gracefully.

## Tech Stack

* **Orchestration:** [n8n](https://n8n.io/)
* **AI & Logic:** OpenAI (GPT-4o, GPT-4.1-mini, Whisper) & LangChain
* **Database:** Supabase (PostgreSQL)
* **Caching/Buffering:** Redis
* **Messaging API:** MegaAPI (WhatsApp Gateway)

## Workflow Architecture

The `AGENTE DE ATENDIMENTO.json` workflow operates in the following stages:

1.  **Ingestion:** Receives the webhook from WhatsApp (MegaAPI).
2.  **Normalization:** Standardizes incoming data (Phone, Name, Message Type).
3.  **Buffering (Redis):** Stores incoming messages temporarily. If the user stops typing for a set time, the flow proceeds with the aggregated message.
4.  **Routing (Switch):** Detects if the input is Text, Audio, or Image.
    * *Audio:* Downloads and transcribes to text.
    * *Image:* Downloads and analyzes visual content for technical defects.
5.  **Agent Processing:** The aggregated context is sent to the **LangChain Agent**, which holds the persona of a helpful technical support specialist.
6.  **Response:** The generated reply is sent back to the user via WhatsApp API.

## How to Use

1.  **Import:** Download the `.json` file from this repo and import it into your n8n instance.
2.  **Credentials:** Configure the following credentials in n8n:
    * Supabase API
    * OpenAI API
    * Redis
    * MegaAPI (Header Auth)
3.  **Environment:** Ensure your Supabase tables.

## 📄 License

[Your License Here]
