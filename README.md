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
```

Then open:

```text
http://localhost:8000/index.html
```

in a modern browser (Chrome/Edge/Firefox).

### 3. Set API keys

1. Choose a **Provider** (top‑right dropdown).
2. Click the **key icon (🔑)**.
3. Paste your API key (obtain from: [OpenAI](https://platform.openai.com/account/api-keys) | [Google AI Studio](https://aistudio.google.com/app/apikey) | [Anthropic](https://console.anthropic.com/settings/keys) | [xAI](https://console.x.ai/settings)).
4. Click **Save** – the app will validate it against the provider.
5. Repeat for other providers as needed.

> Keys are stored in your browser’s `localStorage` and sent directly from your browser to the provider APIs.  
> **Do not** use this with keys you consider highly sensitive on untrusted machines.

---

## Usage Guide

### Basic chat

1. Select **Provider** and **Model**.
2. (Optional) Adjust **Reasoning/Verbosity** (GPT‑5) or **Temperature**.
3. Type into the **message box**.
4. Press **Enter** to send (Shift+Enter for a new line).

The app shows a temporary “Thinking…” assistant bubble with a live elapsed‑time counter during each request.

### System prompt & context

- Click **⚙ Context** to open the **Context Settings** panel.
- **System Prompt / Context**:
  - Global instructions sent with every request.
  - Auto‑saved to `localStorage`.
- **Pinned Context Pairs**:
  - Pairs you marked as **📌 Pin to context** in the main view.
  - Always included in context, do not count toward the history limit.
- **Active Context Pairs**:
  - Non‑pinned pairs currently included in context.
  - Paginated; respects **Context limit** from the top chat toolbar.

### Per‑pair controls (main chat view)

For each prompt/response pair:

- **Include in context**: whether to send this pair in future requests.
- **📌 Pin to context**: move the pair to the “pinned” list (always included).
- **Retry prompt**: re‑send the same user message as a fresh request (using current provider/model/settings).
- **Delete pair**: permanently remove the pair.
- **Collapse pair**: hides the full texts into a one‑line summary.

Assistant messages also have a **Copy response** button.

### Pagination & limits

- **Newer / Older**: navigate through pages of pairs.
- **Per page**: how many pairs to display per page.
- **Context limit**:
  - `0` = unlimited (all included non‑pinned pairs).
  - `>0` = number of most recent included non‑pinned pairs to send.

Pinned pairs are always sent, regardless of the context limit.

### Attachments

- Click **📄** near the input box to attach files.
- Files are read as text and listed as chips under the input.
- Content is injected into a system message as `[FILE 1]`, `[FILE 2]`, etc.
- You can:
  - **Toggle inclusion**: Click the file chip to enable/disable sending that specific file (dimmed = excluded).
  - Remove attachments (× on each chip).
  - Click **📄 ↻** to open the **Refresh** dropdown:
    - Select which files to refresh.
    - Re‑read them from disk (useful after editing locally).

> Note: only the *content* (not the original File objects) is persisted in `localStorage`.  
> After a browser restart, you may need to re‑attach files to enable the refresh feature.

### Saving / Loading conversations

- **Chat name**: a short label stored with the conversation in `localStorage`.
- **Save**:
  - Exports JSON containing:
    - All pairs
    - Attachments’ text content and inclusion state
    - Provider/model used
    - System prompt & chat name
- **Load**:
  - Imports a previously exported JSON file.
  - Replaces current conversation (with unsaved‑changes warning).
- **New**:
  - Clears conversation, attachments, chat name, and context (with unsaved‑changes warning).
  - Keeps provider/model and API keys.

---

## Implementation Notes

- Pure HTML/CSS/JS.
- External libs via CDN:
  - `marked` for Markdown parsing.
  - `highlight.js` (GitHub Dark theme) for syntax highlighting.
- All state (conversation, attachments, prompts, settings, avatars, API keys) is stored in `localStorage`.
- API calls:
  - **OpenAI**: `POST https://api.openai.com/v1/responses`  
    - Uses `reasoning` and `text.verbosity` for GPT‑5.  
    - Optionally enables `web_search_preview` tool.
  - **Google**: `POST https://generativelanguage.googleapis.com/v1beta/models/*:generateContent`  
    - Uses `google_search` (for certain stable models) and `code_execution` tools where available.
  - **Anthropic**: `POST https://api.anthropic.com/v1/messages`  
    - Uses beta tool APIs (`web_search`, `computer`, `bash`, `text_editor`) with appropriate headers.
  - **xAI**: `POST https://api.x.ai/v1/chat/completions`.

You may want to audit/adjust the model IDs, tool configurations, and headers as providers evolve.

### Extending with New Models/Providers

To add a new LLM provider or model to the CypherLLM UI, follow the step‑by‑step recipe in [`ADD_MODEL_SYSTEM_PROMPT.md`](./ADD_MODEL_SYSTEM_PROMPT.md).  
That document is written so that **either a human developer or an LLM** (acting as a code assistant) can mechanically apply all required changes across the codebase.

---

## Security Considerations

- API keys are stored in plain text in `localStorage` and used directly in browser‐side `fetch` calls.
- Anyone with access to your browser profile can potentially retrieve your keys.
- Use this tool only on **trusted machines** and with **keys you are comfortable exposing to the browser**.

For production or shared environments, consider moving API calls to a backend service and removing direct key usage in the browser.

---

## Troubleshooting

- **API errors**: Ensure your API key is valid (check the status indicator). Some models/tools may require specific beta access or billing enabled on your account.
- **CORS issues**: Always run via a local HTTP server, not `file://`.
- **File refresh not working**: After import or restart, re-attach files to enable the refresh feature (original File objects aren't persisted).
- **Performance**: Large conversations or attachments may slow down the browser due to `localStorage` limits (~5MB). Export and start new chats periodically.
- **Browser compatibility**: Tested on Chrome 120+, Firefox 120+, Edge 120+. May not work on older browsers or Safari (due to `localStorage` and `fetch` behaviors).

If you encounter issues, check the browser console for errors and ensure your API credits are sufficient.

---

## License

This project is licensed under the MIT License.  
See [`LICENSE`](./LICENSE) for details.
