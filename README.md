# CodeForge 🚀  
### AI-Powered Cloud IDE & Sandbox Platform

CodeForge is a **full-stack AI-assisted cloud development platform** that provisions isolated coding environments on Kubernetes and allows users to build applications directly from the browser with live preview, terminal access, file editing, and AI-powered code generation.

Inspired by platforms like **Replit** and **CodeSandbox**, CodeForge combines:
- ⚡ Ephemeral cloud sandboxes
- 🤖 AI-driven file editing
- 🖥️ Browser-based IDE
- ☁️ Kubernetes-native infrastructure
- 🔄 Persistent project storage
- 🧠 Real-time developer workflows

---

## ✨ Features

- 🔐 Google OAuth Authentication
- 🧠 AI Chat Assistant for Code Editing
- 📁 File Explorer with Live Updates
- 🖥️ In-Browser Terminal using `node-pty`
- ⚡ Live Preview with Vite HMR
- ☁️ Per-user Isolated Kubernetes Sandboxes
- 🗂️ Persistent Project Storage via S3
- 📨 Notification Service with RabbitMQ
- ⏳ Automatic Sandbox Cleanup using Redis TTL
- 🐳 Fully Containerized Microservice Architecture

---

## 🏗️ Architecture Overview

```text
                    ┌─────────────────────┐
                    │      Frontend       │
                    │  React + Vite IDE   │
                    └─────────┬───────────┘
                              │
          ┌───────────────────┼────────────────────┐
          │                   │                    │
          ▼                   ▼                    ▼
 ┌──────────────┐   ┌────────────────┐   ┌────────────────┐
 │ Auth Service │   │ Sandbox Server │   │ AI Orchestrator│
 │ Google OAuth │   │ Kubernetes API │   │ LangChain Agent│
 └──────┬───────┘   └────────┬───────┘   └────────┬───────┘
        │                    │                    │
        ▼                    ▼                    ▼
 ┌──────────────┐   ┌─────────────────────────────────────┐
 │ RabbitMQ     │   │      Sandbox Pod (Per User)        │
 └──────┬───────┘   │ ┌──────────┐ ┌──────────┐ ┌──────┐ │
        ▼           │ │ Template │ │  Agent   │ │ Sync │ │
 ┌──────────────┐   │ │  Vite App│ │ File APIs│ │ S3   │ │
 │ Notifications│   │ └──────────┘ └──────────┘ └──────┘ │
 └──────────────┘   └─────────────────────────────────────┘
```

---

## 🧠 How It Works

1. User logs in using Google OAuth.
2. A new project is created or an old one is reopened.
3. CodeForge provisions a dedicated sandbox pod inside Kubernetes.
4. The pod contains:
   - A React/Vite preview server
   - A file-system agent
   - An S3 sync service
5. Users interact with:
   - 📂 File Explorer
   - 💬 AI Chat
   - 🖥️ Terminal
   - 🌐 Live Preview
6. AI agents can directly read and modify files inside the sandbox.
7. Redis manages sandbox lifecycle and auto-cleanup.

---

# 🛠️ Tech Stack

## Frontend
- React 19
- Vite
- Tailwind CSS v4
- Socket.IO
- XTerm.js

## Backend Services
- Express.js
- MongoDB + Mongoose
- Redis + ioredis
- RabbitMQ
- Nodemailer

## AI Layer
- LangChain
- LangGraph
- Mistral AI

## Infrastructure
- Kubernetes
- Docker
- Skaffold
- AWS S3

---

# 📂 Project Structure

```bash
codeForge/
│
├── frontend/               # Main IDE frontend
├── auth/                   # Authentication service
├── notification/           # Email notification service
├── ai-orchestration/       # AI agent orchestration
│
├── sandbox/
│   ├── server/             # Sandbox provisioning service
│   ├── router/             # Wildcard routing layer
│   ├── agent/              # File + terminal APIs
│   ├── sync-agent/         # S3 synchronization
│   └── template/           # Starter React template
│
├── k8s/                    # Kubernetes manifests
├── skaffold.yml
└── README.md
```

---

# ⚙️ Sandbox Design

Every sandbox pod contains:

| Container | Purpose |
|---|---|
| `template` | Runs the Vite preview server |
| `agent` | Handles file operations + terminal |
| `sync-agent` | Syncs project files with S3 |

All containers share the same mounted workspace.

This enables:
- live editing
- instant preview updates
- persistent project storage

---

# 🤖 AI Editing Workflow

```text
User Prompt
    ↓
Frontend AI Chat
    ↓
/api/ai/invoke
    ↓
LangChain Agent
    ↓
Sandbox File APIs
    ↓
Files Updated
    ↓
Vite HMR Reload
```

Users can simply describe changes in natural language and see them reflected instantly inside the running application.

---

# 🚀 Getting Started

## Prerequisites

- Docker
- Kubernetes
- Skaffold
- Node.js
- MongoDB
- Redis
- RabbitMQ

---

## Clone Repository

```bash
git clone https://github.com/yourusername/codeForge.git
cd codeForge
```

---

## Install Dependencies

```bash
npm install
```

---

## Start Services Locally

```bash
skaffold dev
```

---

# 🔑 Environment Variables

Example:

```env
MONGO_URI=
REDIS_URL=
JWT_SECRET=
GOOGLE_CLIENT_ID=
GOOGLE_CLIENT_SECRET=
RABBITMQ_URL=
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
MISTRAL_API_KEY=
```

---

# 🌐 Kubernetes Routing

```text
/api/auth        → Auth Service
/api/sandbox     → Sandbox Controller
/api/ai          → AI Orchestrator

*.preview.domain → Live Preview
*.agent.domain   → Sandbox Agent
```

---

# 📸 Core Platform Components

### 🖥️ Browser IDE
- File Explorer
- Live Preview
- AI Chat
- Terminal

### ☁️ Kubernetes Sandboxes
- Isolated environments
- Auto cleanup
- Persistent storage

### 🤖 AI Agent
- Reads files
- Writes code
- Updates projects live

---

# 🔥 Key Highlights

- Multi-service architecture
- Kubernetes-native sandboxing
- AI-driven development workflow
- Persistent cloud projects
- Real-time preview system
- Dynamic wildcard routing
- Fully containerized infrastructure

---

# 📈 Future Improvements

- ✅ Production-grade CI/CD
- ✅ Better multi-language support
- ✅ Collaborative editing
- ✅ Workspace snapshots
- ✅ Advanced AI agents
- ✅ Observability & metrics
- ✅ Automated testing

---

# 👨‍💻 Inspiration

CodeForge is conceptually inspired by:
- CodeSandbox
- Replit
- GitHub Codespaces

while focusing heavily on:

> AI-assisted frontend development in isolated cloud sandboxes.

---

# 📜 License

MIT License

---

# ⭐ Support

If you like this project, consider giving it a ⭐ on GitHub!
