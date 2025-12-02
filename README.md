# CypherLLM

**Ignorance is bliss. Knowledge is power.**

CypherLLM is a single‑page, local, multi‑provider chat client for LLMs that gives you **surgical control over what your AI sees**. 

Named after the character from The Matrix, CypherLLM embraces the core question: *"What should I be aware of?"* Most chat interfaces hide the machinery and force you into "all or nothing" context. CypherLLM shows you everything – tokens sent, context included, API calls made – and lets you **choose what to keep**.

It runs entirely in your browser and talks directly to OpenAI, Google Gemini, Anthropic Claude, xAI Grok, DeepSeek, Perplexity, and Mistral using your own API keys.

> No backend, no build step – just open `index.html` with a static server and start chatting.

## Why CypherLLM?

**Context Management That Actually Works**
- **Pin critical context** that should always be present (setup instructions, requirements, examples)
- **Include/exclude specific pairs** to control exactly what the LLM sees
- **Real-time token counter** shows exactly what you're sending
- **Never lose your setup** when you hit token limits – just exclude old exploration, keep what matters

**Multi-Provider Flexibility**
- Switch between providers/models **within the same conversation**
- Compare responses without re-typing prompts
- Pay only for what you use via API (typically **$5-10/month** vs $60/month in subscriptions)
- No vendor lock-in – use the best model for each task

**Power-User Features**
- Request cancellation (stop button for in-progress requests)
- Status logging with clickable history (debug API issues instantly)
- File uploads (PDF, DOCX, images) with toggle control
- Export/import conversations with full metadata
- All data stays local – no telemetry, no tracking

---

## Features

- **Multi‑provider support**
  - OpenAI: `gpt-5.1`, `gpt-5.1-mini`, `gpt-image-1`
  - Google: `gemini-3-pro-preview`, `gemini-flash-latest`, `gemini-flash-lite-latest`, `gemini-2.5-flash-image`, `gemini-3-pro-image-preview`
  - Anthropic: `claude-opus-4-5-20251101`, `claude-sonnet-4-5`, `claude-haiku-4-5`
  - xAI: `grok-4-latest`
  - DeepSeek: `deepseek-chat`, `deepseek-reasoner`
  - Perplexity: `sonar-pro`, `sonar`, `sonar-reasoning`
  - Mistral: `mistral-large-latest`, `mistral-small-latest`, `pixtral-large-latest`
- **Image generation support**
  - **OpenAI**: `gpt-image-1` (up to 4096×4096 pixels)
  - **Google**: `gemini-2.5-flash-image` (Nano Banana), `gemini-3-pro-image-preview` (Nano Banana Pro, up to 4K)
  - Images display during session but are replaced with placeholders when saving (session-only to avoid storage bloat)
  - Generated images include alt text and captions
- **Provider‑specific controls**
  - OpenAI GPT‑5: reasoning effort + verbosity controls
  - Image models: no temperature/reasoning controls (not applicable)
  - Other models: temperature control
- **File upload support**
  - Native file upload for PDFs, DOCX, and images (JPEG, PNG, GIF, WebP)
  - Provider support:
    - Full support: OpenAI (all file types)
    - Partial support: Google Gemini, Anthropic Claude (PDF + images only)
    - Text fallback: xAI, DeepSeek, Perplexity, Mistral (converted to text)
  - 2MB file size limit to prevent context window overflow
  - Files can be toggled on/off per message
- **Request cancellation**
  - Stop button to cancel in-progress API requests
  - Immediate abort using AbortController API
- **Status indicator & logging**
  - Color-coded status dot (green/yellow/red) showing system state
  - Click status dot to view full status log with timestamps
  - Logs all messages (success, warning, error) with color coding
  - Clear log functionality
- **Token counter**
  - Real-time estimated token usage in Context Settings
  - Shows system prompt + pinned pairs + active context
  - Color-coded: green (<50k), yellow (50k-100k), red (>100k)
- **Rich conversation management**
  - Pagination (newer/older) with configurable page size
  - "Context limit" for how many prior pairs are sent with each request
  - Per‑pair "Include in context" toggle
  - Per‑pair **Pin to context** (always included, doesn't count toward history limit)
  - Collapse/expand whole prompt/response pairs
  - Delete pairs, retry prompt (re‑ask same user message)
- **System prompt & context view**
  - Editable global system prompt, saved in `localStorage`
  - Settings view showing:
    - Estimated token usage
    - Pinned context pairs
    - Active context pairs (paginated & respecting context limit)
- **Text file attachments**
  - Attach one or more local text files (read in browser)
  - **Toggle inclusion**: Click an attachment chip to include/exclude it from the context (visualized by opacity)
  - Content is injected into a system message as `[FILE n]` references
  - "Refresh" menu to re‑read files from disk (e.g., after edits)
- **Chat persistence**
  - Automatic saving of:
    - Conversation pairs (images replaced with placeholders)
    - Attachments (text content + inclusion state)
    - System prompt
    - Chat name
    - Provider, model, and UI settings
  - Export conversation as JSON (with attachments + metadata, images as placeholders)
  - Import conversation from JSON
  - "New chat" with unsaved‑changes guard
- **API key management**
  - Per‑provider API keys stored in `localStorage`
  - In‑app **API key modal** with:
    - Show/hide key
    - Clear key
    - Live validation against each provider's API
  - API key status indicator in header
- **UI niceties**
  - Customizable user avatar and per‑provider assistant avatars (click avatar to upload)
  - Markdown rendering via [marked](https://github.com/markedjs/marked)
  - Syntax highlighting via [highlight.js](https://highlightjs.org/) (GitHub Dark theme)
  - Code blocks with:
    - Header/footer bars
    - Copy buttons (top and bottom)
    - Collapse/expand toggle
  - Images rendered inline with responsive sizing
  - "Thinking…" indicator with animated dots + live timer
  - Back‑to‑top floating button
  - Chat name field + quick Save/Load buttons
  - Status messages truncated with ellipsis to prevent header expansion

---

## Getting Started

### 1. Clone or download

Place `index.html` (and optionally `LICENSE`) into a folder, or clone the repo if you've set one up.

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
3. Paste your API key (obtain from: [OpenAI](https://platform.openai.com/account/api-keys) | [Google AI Studio](https://aistudio.google.com/app/apikey) | [Anthropic](https://console.anthropic.com/settings/keys) | [xAI](https://console.x.ai/) | [DeepSeek](https://platform.deepseek.com/) | [Perplexity](https://www.perplexity.ai/settings/api) | [Mistral](https://console.mistral.ai/)).
4. Click **Save** – the app will validate it against the provider.
5. Repeat for other providers as needed.

> Keys are stored in your browser's `localStorage` and sent directly from your browser to the provider APIs.  
> **Do not** use this with keys you consider highly sensitive on untrusted machines.

---

## Usage Guide

### Basic chat

1. Select **Provider** and **Model**.
2. (Optional) Adjust **Reasoning/Verbosity** (GPT‑5) or **Temperature** (if available).
3. Type into the **message box**.
4. Press **Enter** to send (Shift+Enter for a new line).
5. Click **Stop** button to cancel an in-progress request.

The app shows a temporary "Thinking…" assistant bubble with a live elapsed‑time counter during each request.

### Image generation

1. Select an image model:
   - OpenAI: `gpt-image-1`
   - Google: `gemini-2.5-flash-image` or `gemini-3-pro-image-preview`
2. Type a descriptive prompt (e.g., "a sunset over mountains")
3. Press Enter to generate
4. Images display during the session but are saved as placeholders to avoid storage bloat

**Note**: Provider-generated image URLs typically expire after 1-2 hours. Images are replaced with descriptive placeholders when saving/exporting conversations.

### Status indicator & logging

- The **colored dot** next to "CypherLLM" indicates system status:
  - **Green**: Normal operation
  - **Yellow**: Warning (e.g., validating API keys)
  - **Red**: Error
- **Click the dot** to open the status log dropdown showing:
  - All recent status messages with timestamps
  - Color-coded entries (success/warning/error)
  - Clear log button to reset history
- Status messages in the header are automatically truncated with "..." if too long

### Token counter

- Open **⚙ Context** settings to view estimated token usage
- Shows combined tokens for:
  - System prompt
  - Pinned context pairs
  - Active context pairs (respecting history limit)
  - Attached files
- Color-coded warnings:
  - **Green**: < 50,000 tokens (safe)
  - **Yellow**: 50,000 - 100,000 tokens (caution)
  - **Red**: > 100,000 tokens (may exceed context limits)
- Updates in real-time as you edit system prompt or change context

### File uploads

- Click **📎** (attach icon) near the input box to upload files.
- Supported file types:
  - **Documents**: PDF, DOCX (up to 2MB)
  - **Images**: JPEG, PNG, GIF, WebP (up to 2MB)
- Files larger than 2MB will be rejected to prevent context window overflow.
- Provider compatibility:
  - **OpenAI**: Full support for all file types
  - **Google Gemini & Anthropic Claude**: PDF and images only (DOCX converted to text)
  - **xAI, DeepSeek, Perplexity, Mistral**: All files converted to text
- Uploaded files appear as chips below the input and can be removed individually.

### System prompt & context

- Click **⚙ Context** to open the **Context Settings** panel.
- **Estimated Token Usage**:
  - Real-time token counter at the top
  - Color-coded based on usage level
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
- **📌 Pin to context**: move the pair to the "pinned" list (always included).
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

### Text file attachments

- Click **📄** near the input box to attach text files.
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
    - All pairs (images replaced with placeholders)
    - Attachments' text content and inclusion state
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
  - `marked` for Markdown parsing (handles image rendering).
  - `highlight.js` (GitHub Dark theme) for syntax highlighting.
- All state (conversation, attachments, prompts, settings, avatars, API keys) is stored in `localStorage`.
- **Image handling**:
  - Images display during active sessions via markdown rendering
  - Automatically stripped and replaced with descriptive placeholders when saving
  - Prevents localStorage bloat from base64 image data
- API calls:
  - **OpenAI Chat**: `POST https://api.openai.com/v1/responses`  
    - Uses `reasoning` and `text.verbosity` for GPT‑5.  
    - Optionally enables `web_search_preview` tool.
    - Supports native file upload (PDF, DOCX, images) via base64.
  - **OpenAI Images**: `POST https://api.openai.com/v1/images/generations`
    - Used for `gpt-image-1` model.
    - Returns image URLs (expire after 1-2 hours).
  - **Google**: `POST https://generativelanguage.googleapis.com/v1beta/models/*:generateContent`  
    - Uses `google_search` and `code_execution` tools for chat models.
    - Supports PDF and image uploads (DOCX as text).
    - Image models use `response_modalities: ["TEXT", "IMAGE"]`.
    - Returns base64-encoded images inline.
  - **Anthropic**: `POST https://api.anthropic.com/v1/messages`  
    - Uses beta tool APIs (`web_search`, `computer`, `bash`, `text_editor`) with appropriate headers.
    - Supports PDF and image uploads (DOCX as text).
  - **xAI**: `POST https://api.x.ai/v1/chat/completions`
    - OpenAI-compatible API.
    - File uploads converted to text.
  - **DeepSeek**: `POST https://api.deepseek.com/v1/chat/completions`
    - OpenAI-compatible API.
    - File uploads converted to text.
  - **Perplexity**: `POST https://api.perplexity.ai/chat/completions`
    - OpenAI-compatible API with web search capabilities.
    - File uploads converted to text.
  - **Mistral**: `POST https://api.mistral.ai/v1/chat/completions`
    - OpenAI-compatible API.
    - File uploads converted to text.
- Request cancellation via `AbortController` signal passed to all fetch calls.
- Token estimation using ~4 characters per token approximation.

You may want to audit/adjust the model IDs, tool configurations, and headers as providers evolve.

---

## Security Considerations

- API keys are stored in plain text in `localStorage` and used directly in browser‐side `fetch` calls.
- Anyone with access to your browser profile can potentially retrieve your keys.
- Use this tool only on **trusted machines** and with **keys you are comfortable exposing to the browser**.

For production or shared environments, consider moving API calls to a backend service and removing direct key usage in the browser.

---

## Troubleshooting

- **API errors**: 
  - Ensure your API key is valid (check the status indicator). 
  - Click the status dot to view detailed error logs.
  - Some models/tools may require specific beta access or billing enabled on your account.
- **File upload errors**:
  - Ensure files are under 2MB to prevent context window overflow.
  - Check provider compatibility (some providers only support certain file types).
  - Large PDFs may still exceed token limits even under 2MB.
- **Image generation issues**:
  - OpenAI image URLs expire after 1-2 hours.
  - Images are session-only and replaced with placeholders when saving.
  - Check console for detailed error messages.
- **Token limit warnings**:
  - Use the token counter in Context Settings to monitor usage.
  - Consider unpinning old context pairs or reducing history limit.
  - Remove unused file attachments.
- **CORS issues**: Always run via a local HTTP server, not `file://`.
- **File refresh not working**: After import or restart, re-attach files to enable the refresh feature (original File objects aren't persisted).
- **Performance**: Large conversations or attachments may slow down the browser due to `localStorage` limits (~5MB). Export and start new chats periodically.
- **Browser compatibility**: Tested on Chrome 120+, Firefox 120+, Edge 120+. May not work on older browsers or Safari (due to `localStorage` and `fetch` behaviors).

If you encounter issues, check the browser console for errors, view the status log (click the status dot), and ensure your API credits are sufficient.

---

## License

This project is licensed under the MIT License.  
See [`LICENSE`](./LICENSE) for details.
