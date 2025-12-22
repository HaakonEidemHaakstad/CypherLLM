# CypherLLM

A powerful, single-file web application for interacting with multiple AI providers through a clean, modern chat interface. Built with streaming responses, advanced context management, and support for file attachments.

**Version:** 2.2  
**File:** `index.html` - completely self-contained (HTML + CSS + JavaScript)

---

## Features

### Multi-Provider Support
- **OpenAI** - GPT-5.1, GPT-5-mini/nano, GPT-4.1 variants, o4-mini, Codex models, Image generation
- **Google Gemini** - 3-pro, Flash variants, Image generation models
- **Anthropic Claude** - Opus 4.5, Sonnet 4.5, Haiku 4.5 with computer use & web search tools
- **xAI Grok** - Latest Grok models
- **DeepSeek** - Chat, Reasoner, and Coder variants
- **Perplexity** - Sonar, Sonar Pro, Reasoning, and Deep Research
- **Mistral** - Codestral, Large, Medium, and Small models

### Real-Time Streaming
- **Live response streaming** for all providers
- Words appear as they're generated (like ChatGPT)
- Real-time markdown rendering and code highlighting
- Auto-scroll to follow streaming text

### Advanced Context Management
- **System prompt** customization
- **Custom context entries** - quick notes and instructions always included in context
- **Pinned conversations** - keep important exchanges permanently in context
- **Selective inclusion** - toggle which messages to include
- **Context limit** control (0 = unlimited)
- **Token counter** - estimate API usage before sending
- **Pagination** - organize long conversations

### File Handling
- **Drag & drop** file attachments
- **Multiple file types**: PDF, DOCX, images (PNG, JPG, JPEG, GIF, WebP)
- **Clipboard paste** for images
- **Refresh attachments** from disk
- Binary files sent as base64 to compatible models

### User Experience
- **Conversation persistence** via localStorage
- **Import/Export** conversations as JSON
- **Custom avatars** for both user and assistant (per provider)
- **Collapsible code blocks** with copy buttons
- **Message retry** and deletion
- **Status logging** with visual indicators
- **Back to top** button for long conversations
- **Keyboard shortcuts** (Ctrl+S to save, etc.)
- **PWA support** - Install as standalone app on mobile/desktop (requires HTTPS)
- **Mobile optimized** - Responsive design with safe area support for tablet navigation bars

### Model-Specific Features
- **OpenAI GPT-5**: Reasoning effort (none/minimal/low/medium/high) and verbosity controls
- **OpenAI GPT-4**: Temperature control
- **Google Gemini**: Google Search and Code Execution tools
- **Anthropic Claude**: Computer use, text editor, bash, and web search tools
- **Image generation**: OpenAI gpt-image-1 and Gemini image models

---

## Why CypherLLM?

CypherLLM is designed for users who need:
- **Multiple AI providers** in one interface
- **Advanced context control** for complex conversations
- **Local-first privacy** - all data stored in your browser
- **Streaming responses** for immediate feedback
- **File attachment** support
- **Complete portability** - single HTML file, no installation
- **No backend required** - runs entirely in your browser

Perfect for developers, researchers, and AI enthusiasts who want full control over their AI interactions without vendor lock-in.

---

## Getting Started

### 1. Clone or download

```bash
git clone https://github.com/yourusername/Custom_GPT.git
cd Custom_GPT
```

### 2. Run a simple static server

Since it's a single HTML file, you can:

**Option A: Open directly**
- Simply open `index.html` in your browser

**Option B: Use a local server** (recommended for best compatibility)
```bash
# Python 3
python -m http.server 8000

# PHP
php -S localhost:8000

# Node.js (with http-server)
npx http-server -p 8000
```

Then visit: `http://localhost:8000`

### 3. Set API keys

1. Click the **🔑 API Key** button in the header
2. Select your provider (OpenAI, Google, Anthropic, etc.)
3. Enter your API key
4. Click **Save**
5. The key is validated and stored in your browser's localStorage

**Get API keys from:**
- OpenAI: https://platform.openai.com/api-keys
- Google: https://aistudio.google.com/app/apikey
- Anthropic: https://console.anthropic.com/
- xAI: https://console.x.ai/
- DeepSeek: https://platform.deepseek.com/
- Perplexity: https://www.perplexity.ai/settings/api
- Mistral: https://console.mistral.ai/

---

## Usage Guide

### Basic chat

1. Select your **Provider** and **Model** from the header
2. Type your message in the input field
3. Press **Enter** or click **Send**
4. Watch the response stream in real-time
5. Press **Stop** to cancel generation

**Streaming**: All providers now support real-time streaming - text appears as it's generated!

### Model settings

Click the **⚙ (gear icon)** next to the model selector to access:
- **Reasoning Effort** (GPT-5 models): None, Minimal, Low, Medium, High
- **Verbosity** (GPT-5 models): Low, Medium, High
- **Temperature** (GPT-4 models): 0.0 - 2.0

### Image generation

Available with:
- **OpenAI**: Select `gpt-image-1` model
- **Google**: Select `gemini-2.5-flash-image` or `gemini-3-pro-image-preview`

Simply describe the image you want and the AI will generate it inline in the response.

### Status indicator & logging

- **Green dot** (●) in header = Ready
- **Yellow dot** = Warning/Processing
- **Red dot** = Error

Click the status dot to view the **status log** with timestamps and detailed messages.

### Token counter

Open **Context Settings** (⚙ Context button) to see:
- Estimated token usage
- System prompt length
- Custom context entries count
- Pinned pairs count
- Active context pairs
- File attachments

Helps you stay within model token limits and manage API costs.

### File uploads

**Three ways to attach files:**

1. **Click attach button** (📄) - browse and select files
2. **Drag & drop** - drag files from file explorer onto the input area
3. **Paste images** - copy image and paste (Ctrl+V) into the chat

**Supported formats:**
- PDF documents
- DOCX documents
- Images: PNG, JPG, JPEG, GIF, WebP

**Refresh attachments**: If you modify an attached file on disk, click the refresh button (📄 ↻) to reload its contents.

### System prompt & context

Click **⚙ Context** to access settings:

1. **System Prompt** - Instructions sent with every message
2. **Pinned Context Pairs** - Permanent conversation history
3. **Active Context Pairs** - Recent messages (limited by Context Limit)
4. **Token Counter** - Estimated usage
2. **Custom Context Entries** - Quick notes and instructions always included in every request
   - Add with input field and "Add" button (or press Enter)
   - Entries are collapsed by default - click "Expand" to view full text
   - Click "Delete" to remove an entry
   - Distinguished by red theme (vs blue for pinned, green for active)
   - Persisted in localStorage across sessions
3. **Pinned Context Pairs** - Permanent conversation history
4. **Active Context Pairs** - Recent messages (limited by Context Limit)
5. **Token Counter** - Estimated usage

**Context Limit**: Set how many recent message pairs to include (0 = unlimited)

### Per-pair controls (main chat view)

Each conversation pair has:
- **Include checkbox** - toggle whether to send this pair as context
- **Pin** - keep this pair permanently in context (appears first)
- **Retry** - regenerate the assistant response
- **Delete** - remove this pair from conversation
- **Collapse/Expand** - hide/show full content

### Pagination & limits

In the toolbar:
- **Per page**: Number of conversation pairs to display per page (0 = all)
- **Context limit**: Max recent pairs to include as context (0 = unlimited)
- **Page navigation**: Browse older conversations with ← Newer / Older → buttons

### Drag & drop attachments

NEW! You can now drag files directly onto the input area:
1. Drag one or more files from your file explorer
2. Hover over the input area - you'll see a blue drop zone
3. Release to attach the files
4. Files are processed automatically

### Saving / Loading conversations

**Export conversation:**
1. Click **Save**
2. Downloads a JSON file with:
   - All conversation pairs
   - File attachments
   - System prompt
   - Provider/model info

**Import conversation:**
1. Click **Load**
2. Select a previously saved JSON file
3. Conversation is restored (replaces current chat)

**New chat:**
- Click **New** to start fresh (warns if unsaved changes)

---

## Implementation Notes

### Architecture

- **Single file**: Everything in `index.html` (~8000 lines)
- **No dependencies**: Pure HTML/CSS/JavaScript
- **CDN libraries**: Marked.js (markdown) and Highlight.js (syntax highlighting)
- **localStorage**: All data persisted in browser
- **Direct API calls**: Browser → AI Provider APIs (no backend)
- **PWA-ready**: Includes service worker and manifest for installable app experience

### Streaming Implementation

All providers use Server-Sent Events (SSE) for streaming:
- **OpenAI**: Responses API with `stream: true`
- **Google**: `streamGenerateContent` endpoint
- **Anthropic**: Claude Messages API with streaming
- **xAI, DeepSeek, Perplexity, Mistral**: OpenAI-compatible streaming

Each chunk is:
1. Parsed from SSE format (`data: {...}`)
2. Appended to the response
3. Rendered as markdown
4. Code blocks syntax-highlighted
5. Display auto-scrolls

### Context Management

Three layers of context:
Four layers of context:
1. **System prompt** - always included
2. **Pinned pairs** - user-selected permanent context
3. **Recent pairs** - last N included pairs (controlled by Context Limit)
2. **Custom context entries** - user-added notes and instructions, always included
3. **Pinned pairs** - user-selected permanent conversation context
4. **Recent pairs** - last N included pairs (controlled by Context Limit)

Total context sent = System Prompt + Files + Pinned Pairs + Recent Pairs
Total context sent = System Prompt + Custom Context + Files + Pinned Pairs + Recent Pairs

### File Processing

- **Text files**: Sent as plain text
- **Binary files** (PDF/DOCX/Images): Converted to base64
- **Max size**: 10MB per file (browser limit)
- **Storage**: File content cached in localStorage for refresh

### API Key Validation

Keys are validated on save:
- **OpenAI**: `/v1/models` endpoint
- **Google**: `/v1beta/models` endpoint
- **Anthropic**: `/v1/messages` test request
- **Others**: Provider-specific validation

Validation status shown as colored dot: ● Red (no key), ● Yellow (has key), ● Green (valid key)

---

## Security Considerations

### Important: This is a client-side application

**Security implications:**
- API keys stored in **browser localStorage** (not encrypted)
- API requests made **directly from browser** (keys visible in network tab)
- **No server-side protection** or rate limiting
- Anthropic requires `anthropic-dangerous-direct-browser-access: true` header

**Recommendations:**
- Only use on **trusted, personal devices**
- Don't share your device while keys are stored
- Consider using **API key restrictions** (IP/domain allowlists) when available
- **Monitor API usage** regularly via provider dashboards
- Use **separate keys** for production vs. testing
- **Clear localStorage** when using shared computers

**For production use**, consider:
- Building a backend proxy to handle API keys
- Implementing authentication/authorization
- Adding rate limiting and usage caps
- Using OAuth or session-based auth

---

## Troubleshooting

### API key validation fails
- Verify the key is correct (copy-paste carefully)
- Check the provider's API dashboard for key status
- Ensure billing is enabled (many providers require payment method)
- Some providers have region restrictions

### Streaming doesn't work
- Clear browser cache and reload
- Check browser console for errors
- Ensure you're using a modern browser (Chrome, Edge, Firefox, Safari)
- Some corporate firewalls block SSE - try different network

### Files won't attach
- Check file size (max 10MB)
- Verify file format is supported
- Try drag-and-drop instead of file picker (or vice versa)
- Check browser console for detailed errors

### Context limit issues
- OpenAI models: ~128K tokens for most, 400K for GPT-5
- Google Gemini: 1M-2M tokens
- Anthropic Claude: 200K tokens
- Check token counter in settings before sending

### Conversation not saving
- Check browser localStorage isn't full (usually ~10MB limit)
- Export conversations regularly as JSON backups
- localStorage can be cleared by browser in incognito/privacy modes

### CORS errors
- Anthropic requires the dangerous-direct-browser-access header
- Google and OpenAI support browser requests
- DeepSeek, xAI, Perplexity, Mistral follow OpenAI format
- If CORS issues persist, you'll need a backend proxy

### PWA installation not showing
- PWAs require **HTTPS** to work (not http:// or file://)
- Deploy to GitHub Pages, Netlify, Vercel, or any HTTPS host
- For local testing, use an HTTPS development server
- Check DevTools → Application → Manifest to verify PWA setup
- On mobile, look for "Add to Home Screen" in browser menu

### Mobile input field blocked by navigation bar
- The app includes safe area padding for mobile devices
- If issues persist, try adjusting the padding in the mobile media query
- Tested on tablets with bottom navigation bars

---

## Progressive Web App (PWA)

CypherLLM can be installed as a standalone app on your device:

### Installation Requirements
- **HTTPS connection** (required for PWA)
- Modern browser (Chrome, Edge, Safari, Firefox)

### How to Install

**Desktop:**
1. Visit the site via HTTPS
2. Look for install icon (⊕) in browser address bar
3. Click to install as desktop app

**Mobile/Tablet:**
1. Visit the site via HTTPS
2. Tap browser menu (⋮)
3. Select "Add to Home Screen" or "Install"
4. App icon appears on home screen

**iOS Safari:**
1. Tap share button (□↑)
2. Select "Add to Home Screen"
3. Customize name and tap "Add"

### PWA Features
- **Offline support** - App cached for offline access (API calls need connection)
- **Standalone window** - Runs without browser UI
- **Home screen icon** - Quick access like native apps
- **Optimized for mobile** - Safe area support for navigation bars

---

## License

This project is released under the MIT License.

```text
Copyright (c) 2025 CypherLLM

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

## Contributing

Contributions are welcome! This is a single-file project, so:
- Keep changes in `index.html`
- Test across multiple browsers
- Test with multiple AI providers
- Document new features in this README
- Consider backwards compatibility with localStorage data

---

## Changelog

### Version 2.1 (Current)
- ✨ Added Progressive Web App (PWA) support
- ✨ Added Custom Context Entries feature for quick, always-included notes
- ✨ Added mobile-optimized UI with safe area support for navigation bars
- ✨ Enhanced number input controls with seamless button integration
- 🔧 Removed chat name field for cleaner interface
- 🔧 Fixed load function compatibility (no longer requires chat name in JSON)
- 🔧 Fixed avatar rendering in custom context entries
- 📱 Mobile input field positioning improvements for tablets

### Version 2.0
- ✨ Added real-time streaming for all providers
- ✨ Added drag & drop file attachments
- ✨ Added detailed API key validation with provider names
- 🔧 Fixed model names to match current APIs
- 🔧 Fixed nano model compatibility (removed tools, conditional reasoning)
- 🔧 Improved streaming bubble targeting
- 📚 Complete README rewrite

### Version 1.0
- Initial release with multi-provider support
- Context management
- File attachments
- Import/export functionality
