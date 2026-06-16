# Falcon Models — Connection Guide

> **Token:** Use `HGF-Brains-Access.Token-AiTH-Falcon-All.Access-20260617` (finegrained, Falcon-specific)
> **Never hardcode tokens in files.** Enter them in AnythingLLM's setup wizard only.

---

## Priority Model List

### #1 — Athena's Brain (Heretic Uncensored)

| Field | Value |
|---|---|
| **Agent** | Athena — Executive Assistant |
| **Model** | DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF |
| **Link** | https://huggingface.co/DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF |
| **Format** | GGUF (quantized) |
| **Size** | ~40B parameters |
| **Use Cases** | Context upload, Goldfish Protocol re-establishment, general executive tasks, uncensored reasoning |

**How to connect in AnythingLLM:**

This is a GGUF model (quantized for local inference). It does NOT run on HuggingFace's free Inference API. Options:

1. **Via Ollama on Stomach Droplet** (recommended for 40B models):
   ```bash
   # On your Stomach droplet (SSH or Portainer terminal):
   ollama pull hf.co/DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF
   ```
   Then in AnythingLLM: Settings → LLM → select "Ollama" → Base URL: `http://100.122.20.113:11434` → select the model.

2. **Via Ollama in Codespace** (if droplet unavailable):
   ```bash
   # In Codespace terminal:
   curl -fsSL https://ollama.com/install.sh | sh
   ollama serve &
   ollama pull hf.co/DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF
   ```
   ⚠️ 40B model needs ~24GB RAM. Codespace may not have enough. Use a smaller quantization (Q4_K_M) or use the droplet.

---

### #2 — Typhoon Tycoon (Thai Finance + Legal)

| Field | Value |
|---|---|
| **Agent** | Tycoon — Thai Finance & Legal |
| **Model** | typhoon-ai/typhoon2.5-qwen3-30b-a3b |
| **Link** | https://huggingface.co/typhoon-ai/typhoon2.5-qwen3-30b-a3b |
| **Format** | Safetensors (native HuggingFace format) |
| **Size** | 30B parameters (MoE — only 3B active, FAST) |
| **Use Cases** | Thai legal research, finance, making money in Thailand, translation |

**How to connect in AnythingLLM:**

This model uses Mixture-of-Experts (30B total but only 3B active at a time) — it's fast and lightweight.

1. **Via HuggingFace Inference API** (try first — free tier):
   - In AnythingLLM: Settings → LLM → select "HuggingFace"
   - API Token: paste your `HGF-Brains-Access.Token-AiTH-Falcon-All.Access` token
   - Model: type `typhoon-ai/typhoon2.5-qwen3-30b-a3b`
   - If it works → you're done. Free. No GPU needed.

2. **Via Ollama** (if HF API doesn't support this model):
   ```bash
   ollama pull hf.co/typhoon-ai/typhoon2.5-qwen3-30b-a3b
   ```
   Then connect Ollama as provider in AnythingLLM.

---

### #3 — Kimi Unsloth (Creative Director Comparison)

| Field | Value |
|---|---|
| **Agent** | KIMI — Creative Director (comparison test) |
| **Model** | unsloth/Kimi-K2.6-GGUF |
| **Link** | https://huggingface.co/unsloth/Kimi-K2.6-GGUF |
| **Format** | GGUF (quantized by Unsloth) |
| **Size** | Large (check available quantizations) |
| **Use Cases** | Compare to original Kimi, creative direction, design thinking |

**How to connect in AnythingLLM:**

GGUF model — same approach as #1:

1. **Via Ollama:**
   ```bash
   ollama pull hf.co/unsloth/Kimi-K2.6-GGUF
   ```
   Then in AnythingLLM: Settings → LLM → "Ollama" → select model.

⚠️ Kimi-K2 is very large. Check which quantization fits your available RAM. On the droplet (16GB), use Q2_K or Q3_K_S quantization.

---

### #4 — Engine Qwen (Same Model as #1, Different Context)

| Field | Value |
|---|---|
| **Agent** | Engine Qwen — Technical Operations |
| **Model** | DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF |
| **Link** | https://huggingface.co/DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF |
| **Format** | GGUF |
| **Size** | ~40B parameters |
| **Use Cases** | Compare to Athena's use, technical operations, Engine Qwen context loading |

**Setup:** Same model as #1. In AnythingLLM, create a **separate Workspace** called "Engine Qwen" and load different system prompt + documents. Same model, different personality and context.

---

### #5 — OpenThaiGPT (General Thai)

| Field | Value |
|---|---|
| **Agent** | General Thai language tasks |
| **Model** | openthaigpt/openthaigpt1.5-72b-instruct |
| **Link** | https://huggingface.co/openthaigpt/openthaigpt1.5-72b-instruct |
| **Format** | Safetensors |
| **Size** | 72B parameters (LARGE) |
| **Use Cases** | General Thai NLP, Thai market research, Thai customer interactions |

**How to connect in AnythingLLM:**

1. **Via HuggingFace Inference API** (try first):
   - Same as Typhoon — select "HuggingFace" provider, paste token, type model name
   - 72B is large — may not be available on free Inference API

2. **Via Ollama** (if HF API unavailable):
   ```bash
   ollama pull hf.co/openthaigpt/openthaigpt1.5-72b-instruct
   ```
   ⚠️ 72B needs ~48GB RAM. Too large for your Stomach droplet (16GB). Either use a quantized version or skip this model for now in favor of Typhoon (#2) which is much more efficient.

---

## Quick Reference — Provider Setup in AnythingLLM

### HuggingFace (for Typhoon, OpenThaiGPT)
1. Settings → LLM Provider → **HuggingFace**
2. API Token: `HGF-Brains-Access.Token-AiTH-Falcon-All.Access-20260617`
3. Type the full model path (e.g., `typhoon-ai/typhoon2.5-qwen3-30b-a3b`)

### Ollama (for GGUF models — Heretic, Kimi)
1. Settings → LLM Provider → **Ollama**
2. Base URL: `http://100.122.20.113:11434` (Stomach droplet) or `http://localhost:11434` (local)
3. Select model from dropdown (must be pulled first via `ollama pull`)

### OpenRouter (21+ free models — backup/general use)
1. Settings → LLM Provider → **OpenRouter**
2. API Key: get free key at https://openrouter.ai/keys
3. Recommended free models:
   - `meta-llama/llama-3.3-70b-instruct:free` (general purpose)
   - `deepseek/deepseek-chat-v4-0324:free` (reasoning)
   - `qwen/qwen3-coder:free` (coding)
   - `google/gemma-3-27b-it:free` (fast, good quality)

### Cloudflare Workers AI (edge inference — 10K neurons/day free)
1. Settings → LLM Provider → **Generic OpenAI**
2. Base URL: `https://api.cloudflare.com/client/v4/accounts/{account_id}/ai/v1`
3. API Key: your Cloudflare API token
4. Model: e.g., `@cf/meta/llama-3.3-70b-instruct-fp8-fast`

---

## Recommended First Steps

1. **Start with Typhoon (#2)** — it's the most likely to work on HF free Inference API (MoE = lightweight)
2. **Set up OpenRouter** as backup — guaranteed to work, 21 free models
3. **Test Heretic (#1) via Ollama on Stomach droplet** — pull the model, connect AnythingLLM
4. **Create separate Workspaces** in AnythingLLM for each agent (Athena, Tycoon, Engine Qwen, Kimi)
5. **Upload MemPalace docs** to each workspace for RAG — give each agent its relevant context

---

## Size Reality Check

| Model | RAM Needed | Fits on Droplet (16GB)? | Fits in Codespace? |
|---|---|---|---|
| Typhoon 2.5 (MoE 3B active) | ~4GB | ✅ YES | ✅ YES |
| Heretic 40B (Q4_K_M) | ~24GB | ⚠️ Tight with swap | ❌ NO |
| Heretic 40B (Q2_K) | ~16GB | ⚠️ Just barely | ❌ NO |
| Kimi K2.6 (Q2_K) | ~16GB+ | ⚠️ Depends on quant | ❌ NO |
| OpenThaiGPT 72B | ~48GB | ❌ NO | ❌ NO |

**Bottom line:** Typhoon is your best bet for immediate testing. Heretic models need the droplet with a small quantization. OpenThaiGPT 72B is too large for current infrastructure — use Typhoon for Thai instead.
