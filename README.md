# KRINO Dokim - Desktop App Releases

Official release downloads for **KRINO Dokim** - AI-powered test case generation from user stories.

## Download

**[View All Releases](../../releases)**

| Platform | Requirements |
|----------|--------------|
| Windows 10/11 | [WebView2 Runtime](https://developer.microsoft.com/en-us/microsoft-edge/webview2/) (pre-installed on Windows 11) |
| macOS 10.14+ | No additional requirements |
| Linux | WebKit2GTK (`sudo apt install python3-gi gir1.2-webkit2-4.0`) |

## Installation

### Windows
1. Download `krino-dokim-vX.X.X-windows.zip`
2. Extract to any folder
3. Run `krino-dokim.exe`
4. If SmartScreen warning appears: Click "More info" → "Run anyway"

### macOS
1. Download `krino-dokim-vX.X.X-macos.zip`
2. Extract the `.app` bundle
3. Right-click → Open (first time only, to bypass Gatekeeper)

### Linux
1. Download `krino-dokim-vX.X.X-linux.tar.gz`
2. Extract: `tar -xzf krino-dokim-*.tar.gz`
3. Run: `./krino-dokim/krino-dokim`

## LLM Configuration

KRINO Dokim requires an LLM to generate test cases. Choose **one** of the following options:

### Option A: Cloud API (Recommended for Best Results)

Use your own API key from any supported provider:

| Provider | Get API Key | Models |
|----------|-------------|--------|
| **OpenAI** | [platform.openai.com/api-keys](https://platform.openai.com/api-keys) | GPT-4o, GPT-4-turbo |
| **Anthropic** | [console.anthropic.com](https://console.anthropic.com/) | Claude 3.5 Sonnet, Claude 3 Opus |
| **Google** | [aistudio.google.com/apikey](https://aistudio.google.com/apikey) | Gemini 1.5 Pro, Gemini 1.5 Flash |

**Setup:**
1. Create an account and generate an API key
2. Launch KRINO Dokim → Settings
3. Enter your API key for your chosen provider
4. Select a model from the dropdown

**Cost:** Pay-per-use based on tokens processed. Typical cost: $0.01-0.10 per user story.

---

### Option B: Local LLM (Free, Private, Offline)

Run models locally on your machine for complete privacy and no API costs.

#### Ollama (Easiest)

1. **Install Ollama:** [ollama.com/download](https://ollama.com/download)
2. **Pull a model:**
   ```bash
   ollama pull llama3.1:8b        # Good balance of speed/quality (4.7 GB)
   ollama pull llama3.1:70b       # Best quality, requires 40+ GB RAM
   ollama pull codellama:13b      # Optimized for code tasks
   ```
3. **Start Ollama:** It runs automatically after install
4. **Configure KRINO Dokim:**
   - Settings → LLM Provider → "Ollama"
   - Endpoint: `http://localhost:11434` (default)
   - Select your model from the dropdown

#### LM Studio (GUI-based)

1. **Install LM Studio:** [lmstudio.ai](https://lmstudio.ai/)
2. **Download a model:** Browse and download from the in-app model library
   - Recommended: `TheBloke/Llama-2-13B-chat-GGUF` or similar
3. **Start the server:** Click "Start Server" in LM Studio (default port: 1234)
4. **Configure KRINO Dokim:**
   - Settings → LLM Provider → "LM Studio"
   - Endpoint: `http://localhost:1234/v1`

#### Hardware Requirements for Local LLMs

| Model Size | RAM Required | GPU VRAM | Quality |
|------------|--------------|----------|---------|
| 7-8B params | 8 GB | 6 GB | Good for simple stories |
| 13B params | 16 GB | 10 GB | Better reasoning |
| 70B params | 48 GB+ | 40 GB+ | Near cloud quality |

**Note:** Local models may produce lower quality results than cloud APIs for complex user stories.

---

## Beta Program

Current releases are part of our private beta program.

**Beta Expiration:** Builds are time-limited and will prompt for upgrade when expired.

To join the beta or request access to newer versions:
**krino@krinosystems.com**

## Support

- **Issues:** krino@krinosystems.com
- **Website:** [krinosystems.com](https://krinosystems.com)

---

*Part of the [KRINO](https://krinosystems.com) product family by Krino Systems LLC.*
