# KRINO Dokim - Desktop App

**Professional BDD Test Case Generator**

Transform user stories into comprehensive Gherkin test cases using AI.

---

## Quick Start

### Windows

1. **Download** `krino-dokim-v1.3.0-beta-windows.zip` from [GitHub Releases](https://github.com/KrinoSystems/krino-dokim-releases/releases)
2. **Extract** to a folder (e.g., `C:\Program Files\KRINO`)
3. **IMPORTANT: Unblock files** - Right-click in the extracted folder → **"Open in Terminal"**, then run:
   ```powershell
   Get-ChildItem -Recurse | Unblock-File
   ```

   **Why?** Windows marks downloaded files with "Mark of the Web" (MOTW), blocking DLLs from loading.

   **Verify it worked:**
   ```powershell
   # Check if zone identifier exists - should return nothing
   Get-Content -Path "krino-dokim.exe" -Stream Zone.Identifier -ErrorAction SilentlyContinue
   ```
   If the command returns nothing, unblocking succeeded!

4. **Run** `krino-dokim.exe`

**First-Run Warning (Expected):**
Windows SmartScreen may show: **"Windows protected your PC"**. This is normal for unsigned indie software. Click **"More info"** → **"Run anyway"**.

**Requirements:**
- Windows 10/11
- Microsoft Edge WebView2 Runtime (usually pre-installed; [download here](https://go.microsoft.com/fwlink/p/?LinkId=2124703) if needed)

**Troubleshooting:**
- **App fails to start silently?** You likely skipped step 3. Run the unblock command above.
- **Still not working?** Check if WebView2 is installed.

---

### macOS

1. **Download** `krino-dokim-v1.3.0-beta-macos.zip` from [GitHub Releases](https://github.com/KrinoSystems/krino-dokim-releases/releases)
2. **Extract** and move `KRINO Dokim.app` to Applications folder
3. **Right-click** → **Open** (first launch only, bypasses Gatekeeper)
4. Click **Open** in the security dialog

**Requirements:**
- macOS 10.14 (Mojave) or later
- Apple Silicon (M1/M2/M3) or Intel Mac

---

### Linux

1. **Download** `krino-dokim-v1.3.0-beta-linux.tar.gz` from [GitHub Releases](https://github.com/KrinoSystems/krino-dokim-releases/releases)
2. **Extract**:
   ```bash
   tar -xzf krino-dokim-v1.3.0-beta-linux.tar.gz
   cd krino-dokim
   ```
3. **Make executable** (if needed):
   ```bash
   chmod +x krino-dokim
   ```
4. **Run**:
   ```bash
   ./krino-dokim
   ```

**Requirements:**
- Ubuntu 18.04+, Fedora 32+, or equivalent
- WebKit2GTK (required for GUI):
  ```bash
  # Ubuntu/Debian
  sudo apt install python3-gi gir1.2-webkit2-4.1 libgirepository1.0-dev

  # Fedora/RHEL
  sudo dnf install python3-gobject gtk3 webkit2gtk3

  # Arch Linux
  sudo pacman -S python-gobject gtk3 webkit2gtk
  ```

**Troubleshooting:**
- **App fails to start?** Install WebKit2GTK dependencies above and retry.
- **Permission denied?** Run `chmod +x krino-dokim` in the extracted folder.

---

## Using KRINO Dokim

### Single Story Mode

Generate test cases for one user story:

1. **Connect AI Provider:**
   - Click "Settings" (gear icon)
   - Choose provider: Ollama (local), LM Studio (local), OpenAI, Anthropic, or Google Gemini
   - Enter API key (if using cloud provider)
   - Select model

2. **Enter User Story:**
   - Paste your JIRA story or type user story text
   - Click "Generate Test Cases"

3. **Review & Export:**
   - View generated Gherkin scenarios
   - Edit if needed
   - Export to Excel, Word, or Markdown

---

### Batch Processing Mode

Process multiple stories from Excel/CSV:

1. **Prepare Input File:**
   - Excel (.xlsx, .xls) or CSV file
   - Required columns: `Story ID`, `Title`, `Description`, `Acceptance Criteria`
   - Optional: `Epic`, `Priority`, `Assignee`, `Story Points`

2. **Upload & Configure:**
   - Click "Batch Processing" tab
   - Upload your file
   - Review detected stories
   - Configure settings (model, coverage level)

3. **Process:**
   - Click "Start Processing"
   - Monitor progress in real-time
   - Stories process sequentially (prevents rate limiting)

4. **Review Results:**
   - Expand each story to see generated test cases
   - Green = Success, Red = Failed
   - Click "Modify Story" to edit and regenerate
   - Click "Rerun" to retry individual failed stories
   - Click "Rerun All Failed Stories" (appears if 2+ failures)

5. **Export:**
   - Click "Export Results"
   - Choose format: 4-Sheet Excel, Word, or Markdown
   - Download generated file

**Batch Features:**
- **Pause/Resume:** Close app anytime - reopening resumes from checkpoint
- **Rerun Failed Stories:** Fix model settings and retry only failures
- **Modify & Regenerate:** Edit story details and regenerate test cases
- **Cost Tracking:** View token usage and estimated costs per story

---

## Coverage Levels

- **Quick (3-5 scenarios):** Basic happy path + 1-2 edge cases
- **Standard (8-12 scenarios):** Comprehensive coverage (default, recommended)
- **Exhaustive (15+ scenarios):** Maximum coverage including rare edge cases

---

## AI Provider Setup

### Ollama (Local, Free)

1. Install Ollama: [https://ollama.ai](https://ollama.ai)
2. Pull a model:
   ```bash
   ollama pull qwen2.5:14b
   ```
3. In KRINO: Settings → Ollama → `http://localhost:11434` → Select model

**Recommended models:** `qwen2.5:14b`, `llama3.1:70b`, `mistral-nemo:latest`

---

### LM Studio (Local, Free)

1. Install LM Studio: [https://lmstudio.ai](https://lmstudio.ai)
2. Download a model (e.g., Qwen 2.5 14B)
3. Start local server in LM Studio
4. In KRINO: Settings → LM Studio → `http://localhost:1234` → Model auto-detects

---

### OpenAI (Cloud, Paid)

1. Get API key: [https://platform.openai.com/api-keys](https://platform.openai.com/api-keys)
2. In KRINO: Settings → OpenAI → Enter API key → Select model

**Recommended models:** `gpt-4o`, `gpt-4o-mini` (cheaper)

---

### Anthropic Claude (Cloud, Paid)

1. Get API key: [https://console.anthropic.com/settings/keys](https://console.anthropic.com/settings/keys)
2. In KRINO: Settings → Anthropic → Enter API key → Select model

**Recommended models:** `claude-3-5-sonnet-20241022`, `claude-3-5-haiku-20241022` (cheaper)

---

### Google Gemini (Cloud, Paid)

1. Get API key: [https://aistudio.google.com/apikey](https://aistudio.google.com/apikey)
2. In KRINO: Settings → Google Gemini → Enter API key → Select model

**Recommended models:** `gemini-2.0-flash-exp`, `gemini-1.5-pro`

---

## Data Privacy

- **Local providers (Ollama, LM Studio):** Data never leaves your machine
- **Cloud providers:** Data sent to provider's API (OpenAI, Anthropic, Google)
- **KRINO:** Does not store or transmit your data to KRINO servers
- **API keys:** Stored locally in app settings (never transmitted to KRINO)

---

## Troubleshooting

### General Issues

**App won't start:**
- Windows: Run the unblock command (see installation)
- macOS: Right-click → Open (first launch)
- Linux: Install WebKit2GTK dependencies

**Settings won't save:**
- Check file permissions in app folder
- Try running as administrator (Windows only)

**Slow processing:**
- Local models: Check available RAM (14B models need ~16GB)
- Cloud providers: Check internet connection
- Batch processing: Normal - processes one story at a time to prevent rate limits

---

### Batch Processing Issues

**Upload fails:**
- Verify file has required columns: `Story ID`, `Title`, `Description`, `Acceptance Criteria`
- Check file format: .xlsx, .xls, or .csv only
- Try saving file in Excel 2010+ format

**Stories fail to process:**
1. Click "Modify Story" to check for missing fields
2. Verify AI provider is working (test in Single Story mode)
3. Click "Rerun" to retry individual story
4. If 2+ failures, click "Rerun All Failed Stories"

**Export button missing:**
- At least 1 story must process successfully
- Check if batch processing is still running

**Timeout errors:**
- Increase timeout in Settings (default: 5 minutes)
- Use faster model (e.g., `gpt-4o-mini` instead of `gpt-4o`)
- Reduce coverage level (Standard → Quick)

---

### AI Provider Issues

**Ollama connection failed:**
```bash
# Check if Ollama is running
curl http://localhost:11434/api/tags
```
If no response, start Ollama: `ollama serve`

**LM Studio connection failed:**
- Verify local server is running in LM Studio
- Check port (default: 1234)
- Ensure a model is loaded

**OpenAI/Anthropic/Google API errors:**
- Verify API key is valid and active
- Check account has credits/billing enabled
- Review rate limits (wait a few minutes and retry)

---

## Beta Information

**Expiration Date:** March 6, 2026

After this date, the app will display an expiration notice. Contact [krino@krinosystems.com](mailto:krino@krinosystems.com) for upgrade options.

---

## Support

- **GitHub Issues:** [https://github.com/KrinoSystems/krino-dokim-releases/issues](https://github.com/KrinoSystems/krino-dokim-releases/issues)
- **Email:** [krino@krinosystems.com](mailto:krino@krinosystems.com)

---

## License

Proprietary License - Copyright 2025 TitanMind, licensed to Krino Systems LLC.

This is beta software provided for evaluation purposes. See full license terms at: [https://github.com/KrinoSystems/krino-dokim-releases](https://github.com/KrinoSystems/krino-dokim-releases)

---

**KRINO Dokim v1.3.0-beta** - Professional BDD Test Case Generation
