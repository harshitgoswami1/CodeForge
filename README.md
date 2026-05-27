# CodeForge

## AI-Powered Cloud IDE & Sandbox Platform

CodeForge is a full-stack AI-assisted cloud development platform that provisions isolated coding environments on Kubernetes and allows users to build applications directly from the browser with live preview, terminal access, file editing, and AI-powered code generation.

Inspired by platforms like Replit and CodeSandbox, CodeForge combines ephemeral cloud sandboxes, AI-driven file editing, a browser-based IDE, Kubernetes-native infrastructure, persistent project storage, and real-time developer workflows.

---

## Features

- Google OAuth authentication for secure user management
- AI chat assistant for code editing and generation
- File explorer with live updates
- In-browser terminal using `node-pty`
- Live preview with Vite Hot Module Replacement
- Per-user isolated Kubernetes sandboxes
- Persistent project storage via AWS S3
- Notification service with RabbitMQ
- Automatic sandbox cleanup using Redis TTL
- Fully containerized microservice architecture

---

## Architecture Overview

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
 │Notifications │   │ └──────────┘ └──────────┘ └──────┘ │
 └──────────────┘   └─────────────────────────────────────┘
```

---

## How It Works

1. User logs in using Google OAuth
2. A new project is created or an existing one is reopened
3. CodeForge provisions a dedicated sandbox pod inside Kubernetes
4. The pod contains:
   - A React/Vite preview server
   - A file-system agent
   - An S3 sync service
5. Users interact with the file explorer, AI chat, terminal, and live preview
6. AI agents can directly read and modify files inside the sandbox
7. Redis manages sandbox lifecycle and automatic cleanup

---

## Tech Stack

### Frontend
- React 19
- Vite
- Tailwind CSS v4
- Socket.IO
- XTerm.js

### Backend Services
- Express.js
- MongoDB with Mongoose
- Redis with ioredis
- RabbitMQ
- Nodemailer

### AI Layer
- LangChain
- LangGraph
- Mistral AI

### Infrastructure
- Kubernetes
- Docker
- Skaffold
- AWS S3

---

## Project Structure

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

## Sandbox Design

Each sandbox pod contains three containers that share the same mounted workspace:

| Container | Purpose |
|-----------|---------|
| `template` | Runs the Vite preview server |
| `agent` | Handles file operations and terminal access |
| `sync-agent` | Synchronizes project files with S3 |

This design enables live editing, instant preview updates, and persistent project storage.

---

## AI Editing Workflow

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

Users can describe changes in natural language and see them reflected instantly in the running application.

---

## Getting Started

### Prerequisites

- Docker
- Kubernetes
- Skaffold
- Node.js
- MongoDB
- Redis
- RabbitMQ

### Clone the Repository

```bash
git clone https://github.com/yourusername/codeForge.git
cd codeForge
```

### Install Dependencies

```bash
npm install
```

### Start Services Locally

```bash
skaffold dev
```

---

## Environment Variables

Create a `.env` file in the project root with the following variables:

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

## Kubernetes Routing

```text
/api/auth        → Auth Service
/api/sandbox     → Sandbox Controller
/api/ai          → AI Orchestrator

*.preview.domain → Live Preview
*.agent.domain   → Sandbox Agent
```

---

## Platform Components

### Browser IDE
- File explorer with real-time updates
- Live preview with instant feedback
- AI-powered chat assistant
- Integrated terminal with shell access

### Kubernetes Sandboxes
- Isolated development environments per user
- Automatic cleanup and resource management
- Persistent storage integration

### AI Agent
- Autonomous file reading and modification
- Code generation and updates
- Live project synchronization

---

## Key Highlights

- Multi-service microservice architecture
- Kubernetes-native sandboxing with automatic scaling
- AI-driven development workflow
- Persistent cloud-based projects
- Real-time preview system with HMR
- Dynamic wildcard routing for multi-tenant support
- Fully containerized infrastructure for consistency

---

## Roadmap

- Production-grade CI/CD pipelines
- Multi-language support
- Collaborative editing capabilities
- Workspace snapshots and version control
- Advanced AI agents with specialized capabilities
- Observability and metrics dashboards
- Automated testing framework

---

## Inspiration

CodeForge is conceptually inspired by:
- CodeSandbox
- Replit
- GitHub Codespaces

While focusing specifically on AI-assisted frontend development in isolated cloud sandboxes.

---

## License

MIT License

---

## Support

For questions, issues, or contributions, please visit the [GitHub repository](https://github.com/yourusername/codeForge).
