# CypherLLM

CypherLLM is a single‑page, local, multi‑provider chat UI for LLMs (OpenAI, Google, Anthropic, xAI). It runs entirely in the browser, stores everything in `localStorage`, and lets you manage long conversations, system prompts, and file attachments without any backend.

> ⚠️ **Security note**  
> This app calls provider APIs directly from your browser and stores API keys in `localStorage`. Do **not** use it on untrusted machines or host it publicly with your real production keys.

---

## Features

- **Multiple providers in one UI**
  - OpenAI: `gpt-5.1`, `gpt-5.1-mini`
  - Google: `gemini-3-pro-preview`, `gemini-flash-latest`, `gemini-flash-lite-latest`
  - Anthropic: `claude-opus-4-5-20251101`, `claude-sonnet-4-5`, `claude-haiku-4-5`
  - xAI: `grok-4-latest`
- **Per‑provider controls**
  - GPT‑5: reasoning effort + verbosity
  - GPT‑4 / Claude / Gemini / Grok: temperature
- **Conversation management**
  - Pagination (page size configurable)
  - “Context limit” (how many recent pairs are sent to the model)
  - Per‑pair “Include in context” toggle
  - Per‑pair “📌 Pin to context” (always included, does not count towards limit)
  - Collapse/expand pairs for easier browsing
- **System prompt & context view**
  - Global system prompt sent on every request
  - Sidebar view of pinned and active context pairs
- **Attachments**
  - Attach multiple files; their contents are inlined into the system message
  - Refer to them in prompts as `[FILE n]`
  - “Refresh attachments” to re‑read from disk
- **Persistence**
  - All settings + conversation + attachments stored in `localStorage`
  - Export conversation to JSON
  - Import conversation JSON
  - “New” chat without losing API keys or model selection
- **Nice UX touches**
  - API key modal with per‑provider validation
  - Custom user + per‑provider assistant avatars
  - Markdown rendering via `marked`
  - Syntax highlighting via `highlight.js` with copy/collapse controls on code blocks
  - Back‑to‑top button, thinking indicator with elapsed time, chat naming field, etc.

---

## Getting Started

### 1. Clone or download

```bash
git clone <your-repo-url>.git
cd <your-repo>
