# CypherLLM

<p align="center">
  <img src="https://img.shields.io/badge/License-MIT-green.svg" alt="License: MIT">
  <img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg" alt="PRs Welcome">
  <img src="https://img.shields.io/badge/No_Backend-100%25_Client--Side-blue.svg" alt="No Backend">
</p>

CypherLLM is a single‑page, local, multi‑provider chat UI for LLMs (OpenAI, Google, Anthropic, xAI). It runs entirely in the browser, stores everything in `localStorage`, and lets you manage long conversations, system prompts, and file attachments without any backend.

> ⚠️ **Security Note**  
> This app calls provider APIs directly from your browser and stores API keys in `localStorage`. Do **not** use it on untrusted machines or host it publicly with your real production keys.

---

## Table of Contents

- [Features](#features)
- [Screenshots](#screenshots)
- [Getting Started](#getting-started)
- [Configuration](#configuration)
- [Using the App](#using-the-app)
- [Keyboard Shortcuts](#keyboard-shortcuts)
- [Browser Compatibility](#browser-compatibility)
- [Troubleshooting](#troubleshooting)
- [FAQ](#faq)
- [Contributing](#contributing)
- [Tech Stack](#tech-stack)
- [Acknowledgments](#acknowledgments)
- [License](#license)

---

## Features

| Feature | Description |
| :--- | :--- |
| 🤖 **Multi-Provider** | Switch between OpenAI, Google, Anthropic, and xAI from a single UI. |
| 🔑 **Secure Key Storage** | API keys are stored locally in your browser and validated on save. |
| 📝 **System Prompts** | Define a persistent system prompt sent with every request. |
| 📌 **Pin to Context** | Pin important message pairs so they're always included in context. |
| 📄 **File Attachments** | Attach text files and reference them as `[FILE n]` in your prompts. |
| 🔄 **Refresh Attachments** | Re-read attached files from disk without re-uploading. |
| 📊 **Context Management** | Fine-grained control over which messages are sent to the LLM. |
| 💾 **Import/Export** | Save and load entire conversations as JSON files. |
| 🎨 **Custom Avatars** | Upload custom avatars for yourself and each AI provider. |
| ⚡ **No Backend** | 100% client-side; your data never touches a third-party server. |
| 🌙 **Dark Theme** | Beautiful dark UI with syntax highlighting for code blocks. |

### Provider-Specific Features

| Provider | Models | Special Controls |
| :--- | :--- | :--- |
| **OpenAI** | GPT-4, GPT-4 Turbo, GPT-4o, o1, etc. | Reasoning Effort, Verbosity (GPT-5+), Temperature (GPT-4) |
| **Google** | Gemini Pro, Flash, Flash-Lite | Temperature, Code Execution, Google Search |
| **Anthropic** | Claude Opus, Sonnet, Haiku | Temperature, Web Search, Computer Use Tools |
| **xAI** | Grok | Temperature |

---

## Screenshots

<!-- Add screenshots of your application here -->
<!--
![Main Chat Interface](screenshots/chat.png)
![Context Settings Sidebar](screenshots/settings.png)
![API Key Modal](screenshots/api-key.png)
-->

*Screenshots coming soon. Feel free to contribute!*

---

## Getting Started

### Prerequisites

- A modern web browser (Chrome, Firefox, Edge, Safari)
- An API key from at least one supported provider:
  - [OpenAI API Key](https://platform.openai.com/api-keys)
  - [Google AI Studio Key](https://aistudio.google.com/app/apikey)
  - [Anthropic API Key](https://console.anthropic.com/settings/keys)
  - [xAI API Key](https://console.x.ai/)

### Installation

#### Option 1: Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/CypherLLM.git
cd CypherLLM
```

#### Option 2: Download Directly

Download `index.html` and place it in any folder.

### Running the App

While you *can* open the file directly in a browser (`file:///...`), it is **highly recommended** to use a local static server to avoid potential CORS and `localStorage` issues.

**Using Python:**
```bash
python -m http.server 8000
# Open http://localhost:8000
```

**Using Node.js:**
```bash
npx serve .
# Open http://localhost:3000
```

**Using VS Code:**
Install the [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) extension and click "Go Live."

---

## Configuration

### Setting Up API Keys

1. Select a **Provider** from the dropdown in the header.
2. Click the **🔑 key icon**.
3. Paste your API key into the modal.
4. Click **Save**.
   - The app validates the key with a minimal API call.
   - A green dot indicates a valid key; yellow means stored but unvalidated; red means no key.

### Customizing Models

The app includes a default list of models (some may be placeholders for future releases). To customize:

1. Open `index.html` in a text editor.
2. Find the `MODEL_LISTS` constant (~line 1130):

```javascript
const MODEL_LISTS = {
    openai: ["gpt-4o", "gpt-4-turbo", "gpt-3.5-turbo"],
    google: ["gemini-1.5-pro", "gemini-1.5-flash"],
    anthropic: ["claude-3-5-sonnet-20240620", "claude-3-opus-20240229", "claude-3-haiku-20240307"],
    xai: ["grok-beta"],
};
```

3. Update with your preferred model IDs.
4. Save and refresh the browser.

### Adjusting Defaults

You can also customize default values for:

| Constant | Default | Description |
| :--- | :--- | :--- |
| `PAGE_SIZE` | `10` | Message pairs per page |
| `HISTORY_LIMIT` | `12` | Max pairs sent as context (0 = unlimited) |

---

## Using the App

### Basic Chat

1. Type your message in the input box.
2. Press **Enter** to send (or click **Send**).
3. Watch the "Thinking..." indicator with a live timer.
4. The response appears and is saved automatically.

### Managing Context

Each message pair has controls:

| Control | Description |
| :--- | :--- |
| **☑ Include in context** | When checked, this pair is eligible to be sent to the LLM. |
| **📌 Pin to context** | Always include this pair, regardless of history limit. |
| **Retry prompt** | Re-send the same user message as a new request. |
| **Delete pair** | Permanently remove this exchange. |
| **Collapse/Expand** | Minimize the pair to save screen space. |
| **Copy response** | Copy the assistant's response to clipboard. |

### Context Settings Sidebar

Click **⚙ Context** to open the sidebar:

- **System Prompt:** Edit the instruction sent with every request.
- **Pinned Pairs:** View and manage always-included pairs.
- **Active Pairs:** See which recent pairs fall within your context limit.

### Custom Avatars

- **User Avatar:** Click the "P" circle next to your messages → upload an image.
- **Assistant Avatar:** Click the provider logo next to responses → upload an image (per-provider).

### Attachments

1. Click **📄** to attach text files.
2. Files appear as pills above the input.
3. Reference them in prompts: *"Look at [FILE 1] and..."*
4. Click **📄 ↻** to refresh file contents from disk.

### Import/Export

| Button | Action |
| :--- | :--- |
| **Save** | Export conversation to a `.json` file. |
| **Load** | Import a previously exported conversation. |
| **New** | Start a fresh chat (keeps API keys and settings). |

---

## Keyboard Shortcuts

| Key Combo | Action |
| :--- | :--- |
| `Enter` | Send message |
| `Shift + Enter` | Insert new line |
| `Escape` | Close modals |

---

## Browser Compatibility

| Browser | Supported | Notes |
| :--- | :---: | :--- |
| Chrome 90+ | ✅ | Recommended |
| Firefox 90+ | ✅ | Full support |
| Edge 90+ | ✅ | Full support |
| Safari 15+ | ✅ | Full support |
| Opera 76+ | ✅ | Full support |
| Internet Explorer | ❌ | Not supported |

> **Note:** The File System Access API (used for "Save As" dialog) is only available in Chromium-based browsers. Other browsers fall back to a traditional download.

---

## Troubleshooting

### Common Issues

**❌ "Network Error" or API Connection Failed**

- Ensure you're running via `http://localhost`, not `file://`.
- Check that your API key is valid and has sufficient credits.
- Verify your internet connection.

**❌ Model Not Found (404)**

- The model ID in `MODEL_LISTS` may be outdated or a placeholder.
- Update to a valid model ID (see [Customizing Models](#customizing-models)).

**❌ CORS Errors**

- Run the app via a local server, not directly from the file system.
- Some providers (like Anthropic) require the `anthropic-dangerous-direct-browser-access` header, which is already included.

**❌ localStorage Quota Exceeded**

- Very long conversations with many attachments can exceed browser storage limits.
- Export your conversation and start a new chat.

### Reset Everything

To completely reset the app:

1. Open browser Developer Tools (`F12`).
2. Go to **Application** → **Local Storage**.
3. Delete all entries starting with `chat_clone_`.

---

## FAQ

**Q: Is my data sent to any server besides the LLM provider?**

A: No. CypherLLM is 100% client-side. Your data only goes to the LLM provider you select (OpenAI, Google, Anthropic, or xAI).

**Q: Can I use this offline?**

A: The UI loads offline if cached, but LLM requests require an internet connection.

**Q: How do I add a new provider?**

A: Adding a new provider requires modifying the JavaScript. You'll need to:
1. Add the provider to `MODEL_LISTS`.
2. Add API handling logic in the `sendMessage()` function.
3. Add storage keys for the API key.

**Q: Why are some model names unfamiliar (e.g., gpt-5.1)?**

A: The default model list includes placeholder IDs for potential future models. Update `MODEL_LISTS` with currently available model IDs.

**Q: Can multiple people use this simultaneously?**

A: Each browser/profile has its own `localStorage`, so each user would have a separate instance. There's no shared state or collaboration feature.

---

## Contributing

Contributions are welcome! Here's how you can help:

1. **Fork** the repository.
2. **Create** a feature branch: `git checkout -b feature/amazing-feature`
3. **Commit** your changes: `git commit -m 'Add amazing feature'`
4. **Push** to the branch: `git push origin feature/amazing-feature`
5. **Open** a Pull Request.

### Ideas for Contributions

- [ ] Add more LLM providers (Mistral, Cohere, etc.)
- [ ] Implement conversation search
- [ ] Add message editing
- [ ] Create a "themes" system
- [ ] Add token counting/estimation
- [ ] Implement streaming responses
- [ ] Add keyboard navigation for messages
- [ ] Create browser extension version

---

## Tech Stack

| Technology | Purpose |
| :--- | :--- |
| **HTML5 / CSS3 / ES6+** | Core application (single file, no build) |
| [marked.js](https://github.com/markedjs/marked) | Markdown parsing |
| [highlight.js](https://highlightjs.org/) | Syntax highlighting (GitHub Dark theme) |

No frameworks. No build tools. No dependencies to install. Just one HTML file.

---

## Acknowledgments

- [OpenAI](https://openai.com/) for the GPT API
- [Google](https://ai.google.dev/) for the Gemini API
- [Anthropic](https://www.anthropic.com/) for the Claude API
- [xAI](https://x.ai/) for the Grok API
- [marked.js](https://github.com/markedjs/marked) for Markdown rendering
- [highlight.js](https://highlightjs.org/) for code highlighting
- The open-source community for inspiration

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

<p align="center">
  Made with ❤️ for the AI community
</p>
```
