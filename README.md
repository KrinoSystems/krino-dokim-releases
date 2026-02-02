# KRINO Dokim

**AI-Powered BDD Test Case Generator**

[![Version](https://img.shields.io/badge/version-1.3.0--beta-blue.svg)](https://github.com/KrinoSystems/krino-dokim/releases)
[![Python](https://img.shields.io/badge/python-3.10+-green.svg)](https://python.org)
[![License](https://img.shields.io/badge/license-Proprietary-red.svg)](LICENSE)

KRINO Dokim transforms JIRA user stories into comprehensive BDD-style test cases using AI. Supports both local LLMs (Ollama, LM Studio) and cloud providers (OpenAI, Anthropic, Google Gemini) with Bring Your Own Key (BYOK) integration.

**Part of the KRINO Suite by [Krino Systems LLC](https://krinosystems.com)**

> **🚀 Current Release: v1.3.0-beta (Desktop App Edition)**
> Desktop app with auto-updates, PyArmor protection, and enhanced security.
> Status: Pre-beta testing - Full release end of Q1 2026

---

## What's New in v1.3.0-beta (Desktop App Edition)

### Desktop Application Features
- **Cross-Platform Desktop App** - Native apps for Windows, macOS, and Linux using PyWebView
- **Auto-Update Mechanism** - Automatic detection and installation of updates from GitHub Releases
- **Single Instance Enforcement** - Prevents multiple instances from running
- **Window State Persistence** - Remembers window size between sessions
- **Platform-Specific Optimizations** - EdgeWebView2 (Windows), WebKit (macOS), GTK/WebKit (Linux)
- **Crash Logging** - File-based crash reporting for debugging
- **Beta Expiration System** - Time-limited beta with warning period
- **Build System** - PyInstaller-based builds for all three platforms

### Improvements from v1.2.0

### Cloud BYOK Integration (Phase 3) - Fully Validated

- **OpenAI Support** - GPT-4o, GPT-4.1, o1/o3 reasoning models, GPT-3.5 Turbo
- **Anthropic Support** - Claude 3.5 Sonnet, Claude 3 Opus, Claude 3 Haiku
- **Google Gemini Support** - Gemini 2.0/2.5/3 Flash and Pro, Gemma 3 models
- **Dynamic Model Fetching** - Real-time model discovery via provider APIs
- **Free Model Labeling** - UI highlights free/experimental models with visual tags
- **Model Family Inference** - Automatic pricing for new model variants
- **Budget Tracking** - Set spending limits, monitor costs in real-time
- **Cost Per Story** - Track token usage and costs for each generation
- **Monthly Pricing Updates** - `scripts/update_pricing.py` validates pricing coverage

### Architecture Improvements

- **Modular Codebase** - Restructured from monolithic `app.py` to clean `app/` package
- **Comprehensive Test Suite** - 450+ pytest tests across 16 test files
- **Dev Tooling** - Black, Ruff, isort, Bandit, pre-commit hooks
- **Enhanced Retry Logic** - Exponential backoff with `Retry-After` header support

---

## Features

### Single Story Mode
- Generate test cases for individual JIRA stories
- **Coverage levels**: Quick (3-5 tests), Standard (8-12 tests), Exhaustive (15+ tests)
- Live streaming output with token-by-token generation
- Connection testing with latency display
- Copy-to-clipboard functionality
- Export to 5 formats (Excel, JSON, JSON-Xray, CSV, TestRail)

### Batch Processing Mode
- Process multiple stories from Excel (.xlsx, .xls) or CSV (.csv) files
- Auto-detect CSV delimiters (comma, tab, semicolon)
- Real-time progress tracking with live accordion
- Pause/Resume batch processing
- Per-story rerun for failed stories
- Dynamic metrics grid with live updates
- **Actionable error messages** with suggestions for resolution

### Cloud BYOK (v1.2) - Production Ready
- Bring Your Own API Key - keys stay in your browser session only
- Dynamic model selection from provider APIs with real-time discovery
- **Free model indicators** - Models with zero pricing highlighted in green
- **Model family inference** - New model variants automatically inherit base pricing
- Real-time budget dashboard with color-coded progress
- Cost warnings at 75%, 90%, and 100% thresholds
- Pre-flight budget validation before each request
- **Integration tests** - Validated with real API keys across all providers

### Local LLM Support
- **Ollama** - llama3.1, qwen2.5, mistral, and more
- **LM Studio** - Any compatible GGUF model
- Zero cloud costs, complete privacy

---

## Quick Start

### Prerequisites

- Python 3.10+
- Git
- Local LLM (Ollama or LM Studio) OR cloud API key

### Installation

```bash
# Clone the repository
git clone https://github.com/KrinoSystems/krino-dokim.git
cd krino-dokim

# Create virtual environment
python -m venv .venv

# Activate (Windows)
.venv\Scripts\activate

# Activate (macOS/Linux)
source .venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Run the application
python main.py
```

### Access the Application

```
http://localhost:8000
```

### API Documentation

- **Swagger UI:** http://localhost:8000/docs
- **ReDoc:** http://localhost:8000/redoc

---

## Configuration

### Environment Variables

Create a `.env` file (use `.env.example` as template):

```bash
# Local LLM Configuration
OLLAMA_BASE_URL=http://localhost:11434
LM_STUDIO_BASE_URL=http://localhost:1234/v1

# Application Settings
UPLOAD_FOLDER=uploads
MAX_UPLOAD_SIZE_MB=10
```

### Cloud Provider Setup (BYOK)

API keys are entered in the browser and stored in session memory only - never persisted.

| Provider | Get API Key | Models Available |
|----------|-------------|------------------|
| OpenAI | [platform.openai.com/api-keys](https://platform.openai.com/api-keys) | GPT-4o, GPT-4.1, o1/o3 reasoning, GPT-3.5 Turbo |
| Anthropic | [console.anthropic.com](https://console.anthropic.com) | Claude 3.5 Sonnet, Claude 3 Opus, Claude 3 Haiku |
| Google Gemini | [aistudio.google.com](https://aistudio.google.com) | Gemini 2.0/2.5/3 Flash, Gemini Pro, Gemma 3 |

**Note:** Models are fetched dynamically from provider APIs. Free models (e.g., `gemini-exp-1206`) are highlighted in green. New model variants automatically inherit pricing from their base model family.

### Local LLM Setup

**Option 1: Ollama (Recommended)**
```bash
# Install from https://ollama.ai
ollama pull llama3.1:8b
ollama list  # Verify installation
```

**Option 2: LM Studio**
1. Download from [lmstudio.ai](https://lmstudio.ai)
2. Load a model (e.g., Llama 3.1, Mistral, Qwen)
3. Start the local server

---

## Usage

### Single Story Workflow

1. Select **Provider Type**: Local LLM or Cloud BYOK
2. Choose provider and model
3. Enter story details (Summary, User Story, Acceptance Criteria)
4. Click **Generate Test Cases**
5. View results, copy, or export

### Batch Processing Workflow

1. Prepare Excel (.xlsx, .xls) or CSV (.csv) file with columns:
   - `Issue ID` (required)
   - `Summary` or `Title` (required)
   - `Acceptance Criteria` (required)
   - `As a`, `I want to`, `So that` (optional)
   - CSV files support auto-detection of delimiters (comma, tab, semicolon)
2. Upload file (drag & drop or browse)
3. Configure LLM settings
4. Click **Generate Test Cases for Batch**
5. Monitor progress, pause/resume as needed
6. Export results in preferred format

### Budget Management (Cloud BYOK)

1. Enter your API key
2. Set budget limit (optional, in USD)
3. Monitor the budget dashboard:
   - **Green**: < 75% used
   - **Yellow**: 75-90% used
   - **Red**: > 90% used
4. Processing stops automatically at budget limit

---

## Project Structure

```
krino-dokim/
├── main.py                     # Application entry point (graceful shutdown)
├── app/
│   ├── api/
│   │   ├── routes.py          # HTTP endpoints
│   │   ├── task_state.py      # Global task state management
│   │   ├── websocket.py       # WebSocket manager
│   │   └── checkpoint.py      # Crash recovery checkpoints
│   ├── clients/
│   │   ├── base.py            # Abstract LLM client
│   │   ├── ollama.py          # Ollama integration
│   │   ├── lmstudio.py        # LM Studio integration
│   │   ├── openai_client.py   # OpenAI integration
│   │   ├── anthropic_client.py # Anthropic integration
│   │   └── gemini_client.py   # Google Gemini integration
│   ├── models/
│   │   ├── enums.py           # Coverage level enums
│   │   ├── requests.py        # Request validation (Pydantic)
│   │   ├── responses.py       # Response models
│   │   ├── metrics.py         # Cost/usage metrics
│   │   └── validators.py      # Input validators
│   ├── pricing/
│   │   ├── __init__.py        # Pricing database
│   │   ├── budget.py          # Budget tracker (thread-safe)
│   │   └── token_pricing.py   # Token cost calculation with model family inference
│   ├── processors/
│   │   └── qa_task.py         # Test case generation logic
│   └── utils/
│       ├── api_keys.py        # API key validation & sanitization
│       ├── error_registry.py  # 10-dimension error message framework
│       ├── logging.py         # Structured JSON logging with trace IDs
│       ├── model_cache.py     # Model list caching (30-min TTL)
│       ├── path_validation.py # Path traversal protection
│       ├── rate_limit.py      # API rate limiting
│       └── retry.py           # Exponential backoff with Retry-After
├── static/
│   ├── script.js              # Main entry point (ES module)
│   ├── style.css              # Dark theme styling
│   └── modules/               # ES Modules (modular frontend)
│       ├── state.js           # Centralized state management
│       ├── notifications.js   # Toast notification system
│       ├── ui-helpers.js      # Spinner, timer, ETA utilities
│       ├── api.js             # API calls (models, budget, tasks)
│       ├── export.js          # Export (JSON, Excel, CSV, TestRail, Xray)
│       ├── websocket.js       # WebSocket connection manager
│       ├── batch-ui.js        # Batch accordion and metrics
│       └── error-handler.js   # Error display with suggestions
├── templates/
│   └── index.html             # Main UI template
├── tests/                     # Pytest test suite (450+ tests)
│   ├── conftest.py            # Fixtures and configuration
│   └── ...                    # 16 test files with unit & integration tests
├── .github/workflows/         # CI/CD pipelines
│   └── ci.yml                 # Lint, mypy strict, security, tests
├── docs/                      # Documentation
├── requirements.txt           # Production dependencies
├── pyproject.toml            # Project config (Black, Ruff, mypy strict)
├── pytest.ini                # Test configuration
└── .pre-commit-config.yaml   # Git hooks (Black, Ruff, Bandit, pip-audit)
```

---

## Tech Stack

### Backend
- **FastAPI** - Modern async web framework
- **Uvicorn** - ASGI server
- **Pydantic** - Data validation
- **httpx** - Async HTTP client
- **pandas** - Excel processing
- **openpyxl** - Excel file manipulation

### Frontend
- **HTML5/CSS3** - Dark theme UI
- **Vanilla JavaScript (ES6+)** - No framework dependencies
- **WebSockets** - Real-time streaming

### LLM Integrations
- **Local**: Ollama, LM Studio
- **Cloud**: OpenAI, Anthropic, Google Gemini

### Development Tools
- **pytest** - Testing framework (450+ tests)
- **mypy** - Static type checking (strict mode, blocking in CI)
- **Black** - Code formatting (120-char lines)
- **Ruff** - Fast linting
- **isort** - Import sorting
- **Bandit** - Security scanning
- **pip-audit** - Dependency vulnerability scanning
- **pre-commit** - Git hooks

---

## Development

### Setup Development Environment

```bash
# Install all dependencies (including dev)
pip install -r requirements.txt

# Install pre-commit hooks
pre-commit install

# Run code formatting
black app/ tests/
isort app/ tests/

# Run linting
ruff check app/ tests/

# Run type checking (strict mode)
mypy app/

# Run security scan
bandit -r app/

# Run dependency audit
pip-audit
```

### Running Tests

```bash
# Run all tests
pytest

# Run with coverage
pytest --cov=app --cov-report=html

# Run specific test file
pytest tests/test_pricing.py -v

# Run only unit tests
pytest -m unit
```

### Code Style

This project follows:
- **Black** formatting (120-char line length)
- **isort** import sorting (Black-compatible)
- **Google-style docstrings**
- **Type hints** throughout

---

## API Endpoints

### Task Processing

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/tasks/single` | Generate test cases for single story |
| POST | `/api/tasks/single/rerun` | Rerun single story from batch results |
| POST | `/api/tasks/batch` | Process batch of stories from Excel |
| POST | `/api/tasks/{task_id}/cancel` | Cancel running task |
| POST | `/api/tasks/{task_id}/pause` | Pause batch task |
| POST | `/api/tasks/{task_id}/resume` | Resume paused task |
| GET | `/api/tasks/{task_id}/status` | Get task status |

### File Operations

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/files/upload` | Upload Excel/CSV file |
| GET | `/api/files/preview` | Preview file content |
| GET | `/api/files/validate` | Validate file structure |
| GET | `/api/files/coverage` | Check coverage in file |

### Export

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/exports/download` | Download file |
| POST | `/api/exports/json` | Export as JSON |
| POST | `/api/exports/excel` | Export as Excel |
| POST | `/api/exports/csv` | Export as CSV |
| POST | `/api/exports/xray` | Export as JSON-Xray (Jira) |
| POST | `/api/exports/testrail` | Export as TestRail format |

### Models & Budget

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/models/{provider}` | Get available models for provider |
| POST | `/api/cloud-models` | Get cloud provider models (includes free/preview labels) |
| GET | `/api/providers/{provider}/status` | Check provider connection |
| GET | `/api/budget/status` | Get current budget usage |
| POST | `/api/budget/reset/{provider}` | Reset provider budget |
| POST | `/api/budget/limit/{provider}` | Update budget limit |

### Checkpoints (Crash Recovery)

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/checkpoints` | List all checkpoints |
| GET | `/api/checkpoints/{task_id}` | Get specific checkpoint |
| DELETE | `/api/checkpoints/{task_id}` | Delete checkpoint |
| POST | `/api/checkpoints/{task_id}/resume` | Resume from checkpoint |

### Other

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/health` | Health check endpoint |
| WS | `/ws/logs` | WebSocket for real-time logs |

### Export Formats

- **Excel (.xlsx)** - 4 sheets: Summary, Test Cases, Errors, Cost Breakdown
- **JSON** - Structured JSON with all fields
- **JSON-Xray** - JIRA Xray compatible format
- **CSV** - Flat structure, one test per row
- **TestRail** - TestRail bulk import format

---

## Security

### API Key Handling
- Keys stored in browser session memory only
- Never persisted to localStorage or server
- **Automatic sanitization** - keys redacted from error logs
- Cleared on page refresh

### Input Validation
- Pydantic models validate all requests
- **Path traversal protection** - canonical path resolution with allowed directory checks
- SQL injection protection (no database)
- XSS prevention via template escaping

### Budget Protection
- Pre-flight budget checks before API calls
- **Thread-safe** atomic usage updates with reservations
- Automatic stop at budget limit

---

## Troubleshooting

### "Failed to connect to Ollama"
```bash
# Check Ollama is running
ollama list
curl http://localhost:11434/api/tags
```

### "No models available"
```bash
# Pull a model
ollama pull llama3.1:8b
```

### "Invalid API key" (Cloud)
- Verify key at provider's console
- Check key has required permissions
- Ensure no extra whitespace when pasting

### "Budget exceeded"
- Increase budget limit in UI
- Reset budget (refresh page)
- Switch to local LLM (free)

---

## Version History

| Version | Date | Highlights |
|---------|------|------------|
| 1.2.0 | Jan 2026 | Cloud BYOK (OpenAI, Anthropic, Gemini), budget tracking, modular architecture |
| 1.1.0 | Dec 2025 | Pause/resume, retry logic, ETA calculation, export formats |
| 1.0.0 | Dec 2025 | Initial release, local LLM support, batch processing |

See [CHANGELOG.md](CHANGELOG.md) for detailed release notes.

---

## Roadmap

### v1.3 - Desktop App (Current Release - End Q1 2026)
- Cross-platform desktop application (Windows, macOS, Linux) using PyWebView
- Platform-native renderers: EdgeWebView2 (Windows), WebKit (macOS), GTK/WebKit (Linux)
- Auto-update mechanism via GitHub Releases
- Single-instance enforcement, window state persistence
- PyArmor code protection (Windows builds)
- Beta expiration with warning period
- **Target:** 100+ active desktop users across all platforms

### v1.5 - Jira Companion (Planned - Q3 2026)
**Codebase version: v1.4.x**
- Atlassian Marketplace Forge app
- In-Jira test case generation (one-click from issues)
- Comment/attachment write-back to Jira
- Per-user LLM configuration (BYOK or local)
- Freemium model (5 free generations/month, Pro tier unlimited)
- **Target:** 100+ monthly active users, bridge to V2

### v2.0 - Governance Integrator (Planned - Q4 2026)
- Deep JIRA OAuth2 integration
- Automated story fetching with triple-gate governance
- Test case write-back and audit logging
- RAG-based compliance guardrails
- Enterprise B2B contracts
- **Target:** 10 enterprise customers

### v3.0 - Adaptive Core (Planned - Q1 2027+)
- Autonomous scheduling (nightly runs)
- Stateful processing with change detection
- Adaptive re-run logic for requirement updates
- Custom fine-tuned models per customer
- **Target:** 10-20 regulated enterprise customers

---

## Desktop App Installation

### Windows

**Download & Run:**
1. Download `krino-dokim-v1.3.0-beta-windows.zip` from [GitHub Releases](https://github.com/KrinoSystems/krino-dokim/releases)
2. Extract to a folder (e.g., `C:\Program Files\KRINO`)
3. **IMPORTANT: Unblock files** - Right-click in the extracted folder → **"Open in Terminal"**, then run:
   ```powershell
   Get-ChildItem -Recurse | Unblock-File
   ```
   *Why?* Windows marks downloaded files with "Mark of the Web" (MOTW), blocking DLLs from loading. This command removes the security block.

   **Verify it worked:** The command completes silently with no output. To confirm files are unblocked, check any DLL file properties:
   ```powershell
   # Check if zone identifier (MOTW marker) exists - should return nothing
   Get-Content -Path "krino-dokim.exe" -Stream Zone.Identifier -ErrorAction SilentlyContinue
   ```
   If the command returns nothing, unblocking succeeded!

4. Run `krino-dokim.exe`

**First-Run Warning (Expected):**
Windows SmartScreen may show: **"Windows protected your PC"**. This is normal for unsigned indie software. Click **"More info"** → **"Run anyway"**.

**Requirements:**
- Windows 10/11
- Microsoft Edge WebView2 Runtime (usually pre-installed; [download here](https://go.microsoft.com/fwlink/p/?LinkId=2124703) if needed)

**Troubleshooting:**
- **App fails to start silently?** You likely skipped step 3. Open PowerShell in the extracted folder and run `Get-ChildItem -Recurse | Unblock-File`

### macOS

**Download & Run:**
1. Download `krino-dokim-v1.3.0-beta-macos.zip` from [GitHub Releases](https://github.com/KrinoSystems/krino-dokim/releases)
2. Extract and move `KRINO Dokim.app` to Applications folder
3. Right-click → **Open** (first launch only, bypasses Gatekeeper)
4. Click **Open** in the security dialog

**Requirements:**
- macOS 10.14 (Mojave) or later
- Apple Silicon (M1/M2/M3) or Intel Mac

### Linux

**Download & Run:**
1. Download `krino-dokim-v1.3.0-beta-linux.tar.gz` from [GitHub Releases](https://github.com/KrinoSystems/krino-dokim/releases)
2. Extract to a folder:
   ```bash
   tar -xzf krino-dokim-v1.3.0-beta-linux.tar.gz
   cd krino-dokim
   ```
3. Make executable (if needed):
   ```bash
   chmod +x krino-dokim
   ```
4. Run:
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
- **App fails to start?** Install WebKit2GTK dependencies above and retry
- **Permission denied?** Run `chmod +x krino-dokim` in the extracted folder

---

## License

Proprietary License - Copyright 2025 TitanMind, licensed to Krino Systems LLC.

See [LICENSE](LICENSE) for details.

---

## Support

- **Issues**: [GitHub Issues](https://github.com/KrinoSystems/krino-dokim/issues)
- **Email**: support@krinosystems.com
- **Documentation**: [docs/](docs/)

---

## Acknowledgments

- Built with [FastAPI](https://fastapi.tiangolo.com/)
- Powered by [Ollama](https://ollama.ai), [LM Studio](https://lmstudio.ai), [OpenAI](https://openai.com), [Anthropic](https://anthropic.com), and [Google AI](https://ai.google)
- Real-time updates via WebSockets

---

**KRINO Dokim v1.3.0** - Professional BDD Test Case Generation (Desktop App Edition)
