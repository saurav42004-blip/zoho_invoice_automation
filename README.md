# Telegram Zoho Invoice Automation (n8n)

An AI-powered automation workflow built in n8n that enables users to generate invoices directly from Telegram using natural language and voice messages, with automatic customer management and PDF delivery via Zoho Invoice.

---

## 📌 Overview

This project connects Telegram, OpenAI, and Zoho Invoice (Zoho Books API) to build a conversational invoice generation system.

Users can send messages like:

- Create invoice for 3 adults and 2 kids for Mangrove tour, due next Friday for $560 in total.
- Generate invoice for Desert Safari for 4 adults at cost $200.
- Apply 10% discount and set due date 25 December 
- Confirm  

The workflow processes the message, extracts structured invoice details using AI, checks/creates the customer in Zoho, generates the invoice, and sends the PDF back to the user via Telegram.

---

## 🏗️ Workflow Architecture

### Main Components

- Telegram Trigger  
- Switch Node (Text / Voice handling)  
- Get File (for voice messages)  
- OpenAI Transcription (voice to text)  
- Edit Fields (preprocessing)  
- AI Agent (intent detection + invoice extraction)  
- Parse AI Output  
- Customer Tools:
  - Get Customer ID  
  - Create Customer  
- Invoice Processing:
  - Create Invoice  
- Get PDF (Invoice) 
- Telegram Send Message  
- Telegram Send Document (PDF delivery)

---

## 🔄 Workflow Visual

![Workflow](workflow.png)

---

## 🧠 How It Works

### 1. User Input (Telegram)
- Accepts text messages  
- Accepts voice messages (automatically transcribed)  

### 2. AI Processing
The AI Agent:
- Detects invoice intent  
- Extracts:
  - Client name  
  - Due date  
  - Discount  
  - Items/services  
  - Adult & Kids counts (separated into distinct line items)  
- Generates structured invoice JSON  
- Handles multi-turn confirmations  

### 3. Customer Handling (Automated)
The workflow:
- Searches for customer using Zoho API  
- If not found → Automatically creates a new customer  
- Ensures `customer_id` is always available before invoice creation  

### 4. Invoice Creation
Depending on confirmation:

- Creates a **Invoice**
- Applies:
  - Currency  
  - Exchange rate (if required)  
  - Entity-level discount  
  - Due date  
  - Custom invoice subject  

### 5. PDF Generation & Delivery
- Downloads the generated PDF from Zoho  
- Sends it directly to the initiating Telegram user  

---

## 🛠️ Tech Stack

- n8n (Workflow Automation)  
- Telegram Bot API  
- OpenAI (Chat Model + Audio Transcription)  
- Zoho Invoice (Zoho Books API v3)  
- OAuth2 Authentication  

---

## 🔐 Required Credentials

To run this workflow, configure the following in n8n:

- Telegram Bot Token  
- OpenAI API Key  
- Zoho OAuth2 Credentials  

---

## ✅ Features

- Natural language invoice generation  
- Voice message support  
- Automatic customer lookup & creation  
- Adult/Kids automatic line-item separation  
- Invoice-level discount handling  
- Multi-currency support (with exchange rate)  
- Automatic PDF download  
- Telegram PDF delivery  
- Confirmation-based workflow  
- Multi-turn conversation handling  

---

## 🎯 Use Cases

- Travel & tour booking automation  
- SME invoice automation  
- Conversational billing assistant  
- AI-powered financial workflow demo  
- Portfolio automation project  
