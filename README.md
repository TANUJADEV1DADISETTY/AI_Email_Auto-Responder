# 📧 Local AI Email Auto-Responder using n8n + Ollama

## 🚀 Project Overview

This project is a fully local, privacy-focused AI email auto-responder built using n8n and Ollama. It automatically reads incoming emails, processes them using a local LLM, and sends intelligent replies without any external API.

### 🔑 Key Features

- 100% Local Processing (No cloud APIs)
- AI-powered email replies
- Automated workflow using n8n
- IMAP + SMTP integration
- Maintains email threads
- Loop prevention
- Zero API cost

---

## 🧱 Tech Stack

- n8n – Workflow automation
- Ollama – Local LLM server
- Docker & Docker Compose
- IMAP/SMTP protocols

---

## 📁 Project Structure

    ai-email-responder/
    │
    ├── docker-compose.yml
    ├── .env.example
    ├── workflow.json
    ├── submission.json
    └── README.md

---

## ⚙️ Prerequisites

- Docker Desktop installed and running
- Email account with IMAP and SMTP enabled
- App password (for Gmail users)

---

## 🐳 Setup Instructions

### 1. Clone Repository

    git clone <your-repo-url>
    cd ai-email-responder

---

### 2. Configure Environment Variables

Create .env file:

    cp .env.example .env

Edit .env:

    IMAP_HOST=imap.example.com
    IMAP_PORT=993
    IMAP_USER=your_email@example.com
    IMAP_PASSWORD=your_password

    SMTP_HOST=smtp.example.com
    SMTP_PORT=587
    SMTP_USER=your_email@example.com
    SMTP_PASSWORD=your_password

    N8N_HOST=localhost
    N8N_PORT=5678

---

### 3. Start Docker Containers

    docker-compose up -d

Check status:

    docker-compose ps

Both containers should be healthy.

---

### 4. Install LLM Model

    docker exec -it ollama_responder ollama pull llama3:8b

Verify:

    docker exec -it ollama_responder ollama list

---

### 5. Access n8n UI

Open in browser:

    http://localhost:5678

---

### 6. Import Workflow

- Click Import
- Upload workflow.json
- Activate workflow

---

## 🔁 Workflow Logic

1. IMAP Trigger detects new email
2. IF node prevents self-replies
3. Email content formatted as prompt
4. HTTP request sent to Ollama
5. LLM generates response
6. SMTP sends reply
7. Thread maintained using Message-ID

---

## 🧪 Testing

1. Send email to configured account
2. Check n8n executions
3. Verify reply received
4. Ensure reply is in same thread
5. Confirm no infinite loops

---

## 📌 Important Notes

- Use http://ollama:11434 (NOT localhost)
- Ensure model name matches exactly: llama3:8b
- Do not hardcode credentials
- Use environment variables

---

## 🔐 .env.example

    IMAP_HOST=imap.example.com
    IMAP_PORT=993
    IMAP_USER=your_email@example.com
    IMAP_PASSWORD=your_password

    SMTP_HOST=smtp.example.com
    SMTP_PORT=587
    SMTP_USER=your_email@example.com
    SMTP_PASSWORD=your_password

    N8N_HOST=localhost
    N8N_PORT=5678

---

## 📩 submission.json Format

    {
      "emailCredentials": {
        "imap": {
          "host": "imap.example.com",
          "port": 993,
          "user": "test@example.com",
          "password": "password"
        },
        "smtp": {
          "host": "smtp.example.com",
          "port": 587,
          "user": "test@example.com",
          "password": "password"
        }
      }
    }

---

## 🎯 Conclusion

This project demonstrates how to build a fully private AI-powered system using local infrastructure. It eliminates dependency on third-party APIs while maintaining scalability, flexibility, and cost efficiency.

---
