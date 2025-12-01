Recipe: Adding a New LLM Provider to CypherLLM

## Pre-Integration: Validate Provider Information

**ALWAYS use WebSearch to verify:**
- Official API documentation URL
- Correct model names (exact spelling and format)
- API endpoint URL
- API authentication method
- Whether the API is OpenAI-compatible
- Temperature range supported
- Console/dashboard URL

## Complete Integration Checklist (20 Steps)

### 1. Provider Dropdown
Location: `<select id="provider-select">`
```html
<option value="providername">Provider Name</option>
```

### 2. Model Lists
Location: `const MODEL_LISTS = {`
```javascript
providername: ["model-1", "model-2"],
```

### 3. API Key Storage Constants (2 constants)
```javascript
const APIKEY_PROVIDERNAME_STORAGE_KEY = "chat_clone_providername_api_key";
const APIKEY_PROVIDERNAME_VALID_KEY = "chat_clone_providername_key_valid";
```

### 4. Avatar Storage Constant
```javascript
const ASSISTANT_AVATAR_PROVIDERNAME_KEY = "chat_clone_avatar_providername";
```

### 5. API Keys Object
```javascript
apiKeys = { ..., providername: "" }
```

### 6. Load API Keys Function
```javascript
const xKey = localStorage.getItem(APIKEY_PROVIDERNAME_STORAGE_KEY);
if (xKey) apiKeys.providername = xKey;
```

### 7. Avatar CSS
```css
.avatar.assistant.providername {
    background: #colorcode;
    color: #ffffff;
}
```

### 8 & 9. Avatar Storage Keys (2 locations)
Both loadAssistantAvatars() and saveAssistantAvatar()
```javascript
providername: ASSISTANT_AVATAR_PROVIDERNAME_KEY,
```

### 10. API Integration
Add full else-if block in sendMessage() function with OpenAI-compatible format

### 11. API Links
```javascript
providername: "https://console.provider.com/",
```

### 12. Temperature Control Logic
Add to showTemperature condition

### 13. Temperature Limits (if needed)
Only if provider uses non-standard range

### 14 & 15. Validation Functions (2 locations)
Both validateApiKey() and validateApiKeySilent()
```javascript
case "providername":
    endpoint = "https://api.provider.com/v1/models";
    headers = { Authorization: `Bearer ${key}` };
    break;
```

### 16 & 17. API Key Storage Keys (2 locations)
Modal save and clear handlers

### 18. Validation Keys (4 locations!)
1. Modal open handler
2. Modal save handler
3. Clear button handler
4. validateAllKeys() function

### 19. Provider Names (3 locations!)
1. Avatar upload handler
2. Modal open handler
3. validateAllKeys() function

### 20. Providers Array
Add to validateAllKeys() providers array

## Total: ~27 locations to update

## Common Mistakes
- Wrong model names (verify with WebSearch!)
- Missing `-latest` suffixes
- Forgetting duplicate locations (4 validationKeys, 3 providerNames, 2 storageKeys)
- Wrong API endpoint
- Wrong authentication method

---

This recipe should be used as a system prompt when adding new providers to ensure nothing is missed!
