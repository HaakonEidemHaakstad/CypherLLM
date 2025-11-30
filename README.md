# CypherLLM

CypherLLM is a single‑page, local, multi‑provider chat client for LLMs.  
It runs entirely in your browser and talks directly to OpenAI, Google Gemini, Anthropic Claude, and xAI Grok using your own API keys.

> No backend, no build step – just open `index.html` with a static server and start chatting.

---

## Features

- **Multi‑provider support**
  - OpenAI: `gpt-5.1`, `gpt-5.1-mini`
  - Google: `gemini-3-pro-preview`, `gemini-flash-latest`, `gemini-flash-lite-latest`
  - Anthropic: `claude-opus-4-5-20251101`, `claude-sonnet-4-5`, `claude-haiku-4-5`
  - xAI: `grok-4-latest`
- **Provider‑specific controls**
  - OpenAI GPT‑5: reasoning effort + verbosity controls
  - Other models: temperature control
- **Rich conversation management**
  - Pagination (newer/older) with configurable page size
  - “Context limit” for how many prior pairs are sent with each request
  - Per‑pair “Include in context” toggle
  - Per‑pair **Pin to context** (always included, doesn’t count toward history limit)
  - Collapse/expand whole prompt/response pairs
  - Delete pairs, retry prompt (re‑ask same user message)
- **System prompt & context view**
  - Editable global system prompt, saved in `localStorage`
  - Settings view showing:
    - Pinned context pairs
    - Active context pairs (paginated & respecting context limit)
- **Attachments**
  - Attach one or more local files (text only; read in browser)
  - **Toggle inclusion**: Click an attachment chip to include/exclude it from the context (visualized by opacity)
  - Content is injected into a system message as `[FILE n]` references
  - “Refresh” menu to re‑read files from disk (e.g., after edits)
- **Chat persistence**
  - Automatic saving of:
    - Conversation pairs
    - Attachments (text content + inclusion state)
    - System prompt
    - Chat name
    - Provider, model, and UI settings
  - Export conversation as JSON (with attachments + metadata)
  - Import conversation from JSON
  - “New chat” with unsaved‑changes guard
- **API key management**
  - Per‑provider API keys stored in `localStorage`
  - In‑app **API key modal** with:
    - Show/hide key
    - Clear key
    - Live validation against each provider’s API
  - API key status indicator in header
- **UI niceties**
  - Customizable user avatar and per‑provider assistant avatars (click avatar to upload)
  - Markdown rendering via [marked](https://github.com/markedjs/marked)
  - Syntax highlighting via [highlight.js](https://highlightjs.org/) (GitHub Dark theme)
  - Code blocks with:
    - Header/footer bars
    - Copy buttons (top and bottom)
    - Collapse/expand toggle
  - “Thinking…” indicator with animated dots + live timer
  - Back‑to‑top floating button
  - Chat name field + quick Save/Load buttons

---

## Getting Started

### 1. Clone or download

Place `index.html` (and optionally `LICENSE`) into a folder, or clone the repo if you’ve set one up.

### 2. Run a simple static server

Opening `index.html` via `file://` may cause CORS issues for API calls.  
Use any static HTTP server, e.g.:

```bash
# Python 3
python -m http.server 8000

# Node (http-server)
npx http-server . -p 8000
