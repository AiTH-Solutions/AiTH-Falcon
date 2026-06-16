# AiTH-Falcon

**The Millennium Falcon — Solo's autonomous, portable, all-in-one AI cockpit.**

> Not an agent. Not a dashboard. A ship. You pick it up and go.

---

## What Is This?

AiTH-Falcon is your self-contained AI toolkit — agent capabilities, model connections, research tools, and orchestrator workbench in one package. It runs anywhere Docker runs: GitHub Codespaces, your Stomach droplet, or any future server.

**Core: [AnythingLLM](https://anythingllm.com/)** — chat interface + agent mode + RAG + multi-model support in a single container.

---

## Quick Start

### Option 1: GitHub Codespaces (cloud — recommended)
1. Go to this repo on GitHub
2. Click **Code** → **Codespaces** → **Create codespace on main**
3. Wait for build (~2 min), then in the terminal run:
   ```bash
   docker compose up -d
   ```
4. AnythingLLM opens automatically at the forwarded port 3001

### Option 2: Any server with Docker
```bash
git clone https://github.com/AiTH-Solutions/AiTH-Falcon.git
cd AiTH-Falcon
docker compose up -d
```
Open `http://localhost:3001` in your browser.

### Option 3: Portainer on Stomach Droplet
Copy the contents of `docker-compose.yml` into a new Portainer stack. Deploy.

---

## First Launch Setup

On first launch, AnythingLLM shows a setup wizard. Connect your model providers:

| Provider | What It Gives You | Cost |
|---|---|---|
| **OpenRouter** | 21+ free models (Llama 3.3 70B, Qwen3, DeepSeek, GLM 4.5) | FREE |
| **HuggingFace** | Your Heretic models, Thai legal (WangchanX), Thai finance (Typhoon) | FREE (Inference API) |
| **Cloudflare Workers AI** | 50+ edge models, 10K neurons/day | FREE |
| **Ollama** | Local models on Stomach droplet (phi3, qwen2.5-coder, etc.) | FREE (already running) |

### Connecting OpenRouter (fastest — zero setup)
1. Go to https://openrouter.ai/keys — create a free API key
2. In AnythingLLM setup → LLM Provider → select "OpenRouter"
3. Paste your API key
4. Choose a model (e.g., `meta-llama/llama-3.3-70b-instruct:free`)

### Connecting HuggingFace (your Thai/Heretic models)
1. Go to https://huggingface.co/settings/tokens — create a free token
2. In AnythingLLM → LLM Provider → select "HuggingFace"
3. Paste your token
4. Select your model (Typhoon, WangchanX, etc.)

---

## What You Can Do

- **Chat** — Talk to any connected model, switch models mid-conversation
- **Agent Mode** — Give models tools: web browsing, code execution, file management
- **RAG** — Upload docs (like MemPalace files) and chat with them
- **Workspaces** — Separate contexts for different projects/clients
- **Test Models as Agents** — Evaluate which HuggingFace models can actually handle agent tasks

---

## Architecture

```
AiTH-Falcon (this repo)
├── docker-compose.yml          # AnythingLLM container
├── .devcontainer/              # GitHub Codespaces config
│   └── devcontainer.json
└── README.md                   # You are here

Data persists in Docker volumes:
├── anythingllm-storage         # Settings, workspaces, embeddings
└── anythingllm-hotdir          # Drop files here for auto-ingestion
```

---

## Adding to Falcon (Future)

This is component #1. More tools will be added as needed — each as a service in `docker-compose.yml`:

- n8n (workflow automation)
- SearXNG (private search)
- Open WebUI (if needed alongside AnythingLLM)
- Custom agent scripts
- Whatever Solo needs next

---

## Context

- **MemPalace** (knowledge): https://github.com/AiTH-Solutions/aith-mempalace
- **Falcon Cockpit site**: https://aithaidev.xyz (Cloudflare Pages)
- **Stomach Droplet**: 104.207.64.5 (Portainer on :9000)
