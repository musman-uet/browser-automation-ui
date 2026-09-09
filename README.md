<p align="center">
  <img src="./assets/web-ui.png" alt="Browser Agent Web UI" width="900" />
</p>

<h1 align="center">Browser Agent Web UI</h1>

<p align="center">
  A clean Gradio interface for running AI-powered browser agents with multiple LLM providers, configurable browser sessions, and deep-research workflows.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.11%2B-blue" alt="Python 3.11+" />
  <img src="https://img.shields.io/badge/Interface-Gradio-orange" alt="Gradio" />
  <img src="https://img.shields.io/badge/Maintainer-Usman-success" alt="Maintainer Usman" />
</p>

---

## Overview

Browser Agent Web UI provides a browser-based control panel for AI agents built around the `browser-use` ecosystem. Instead of configuring and running every browser task from the command line, you can manage agents, browser options, model providers, saved configurations, and research tasks through a single web interface.

This repository is maintained by **Usman** and builds on the open-source work of the [`browser-use`](https://github.com/browser-use/browser-use) project and its community contributors.

## Key Features

- **Simple Web Interface** — Run browser-agent tasks from a Gradio-based UI.
- **Multiple AI Providers** — Supports OpenAI, Azure OpenAI, Anthropic, Google, DeepSeek, Mistral, Ollama, Alibaba, Moonshot, IBM, Grok, SiliconFlow, ModelScope, and other configured providers.
- **Custom Browser Support** — Connect an existing local browser profile when required.
- **Persistent Sessions** — Keep the browser open between tasks to preserve session state.
- **Deep Research Agent** — Includes a dedicated workflow for research-oriented browser tasks.
- **Config Management** — Load and save commonly used agent/browser settings from the UI.
- **Docker Support** — Run the project in a containerized environment with browser/VNC support.
- **Configurable UI** — Choose the server IP, port, and available interface theme from the command line.

## Project Structure

```text
web-ui/
├── assets/                  # Images and UI assets
├── src/
│   ├── agent/               # Browser-use and deep-research agents
│   ├── browser/             # Custom browser/context handling
│   ├── controller/          # Agent controller logic
│   ├── utils/               # Configuration, LLM and helper utilities
│   └── webui/               # Gradio interface and UI components
├── tests/                   # Project tests
├── .env.example             # Environment variable template
├── docker-compose.yml       # Docker Compose configuration
├── Dockerfile               # Container image definition
├── requirements.txt         # Python dependencies
└── webui.py                 # Application entry point
```

## Getting Started

## Demo Videos

Explore the main features and workflow of the application through these screen recordings:

- 🎥 [Project Demo 1](ProjectDemo/ProjectDemo1.mp4)
- 🎥 [Project Demo 2](ProjectDemo/ProjectDemo2.mp4)
- 🎥 [Project Demo 3](ProjectDemo/ProjectDemo3.mp4)

### Requirements

For a local installation, make sure you have:

- Python **3.11 or later**
- Git
- A supported LLM API key, or a local Ollama installation
- Playwright browser dependencies

Using [`uv`](https://docs.astral.sh/uv/) is recommended for creating and managing the Python environment.

### 1. Clone the Repository

```bash
git clone https://github.com/usman/web-ui.git
cd web-ui
```

> If your GitHub username or repository name is different, replace the URL above with your actual repository URL.

### 2. Create a Virtual Environment

Using `uv`:

```bash
uv venv --python 3.11
```

Activate it on Windows Command Prompt:

```cmd
.venv\Scripts\activate
```

Activate it on Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

Activate it on macOS/Linux:

```bash
source .venv/bin/activate
```

### 3. Install Dependencies

```bash
uv pip install -r requirements.txt
```

Install Playwright browsers:

```bash
playwright install --with-deps
```

To install Chromium only:

```bash
playwright install chromium --with-deps
```

### 4. Configure Environment Variables

Create your local `.env` file from the provided template.

Windows Command Prompt:

```cmd
copy .env.example .env
```

PowerShell, macOS, or Linux:

```bash
cp .env.example .env
```

Open `.env` and add the API key(s) for the provider you want to use. For example:

```env
OPENAI_API_KEY=
ANTHROPIC_API_KEY=
GOOGLE_API_KEY=
DEEPSEEK_API_KEY=
MISTRAL_API_KEY=

DEFAULT_LLM=openai
KEEP_BROWSER_OPEN=true
USE_OWN_BROWSER=false
```

Only configure the providers you actually plan to use.

### 5. Start the Web UI

```bash
python webui.py --ip 127.0.0.1 --port 7788
```

Then open:

```text
http://127.0.0.1:7788
```

The application also accepts a UI theme option:

```bash
python webui.py --ip 127.0.0.1 --port 7788 --theme Ocean
```

## Using Your Own Chrome Browser

The application can connect to your existing Chrome installation and profile.

Example for Windows:

```env
BROWSER_PATH="C:\Program Files\Google\Chrome\Application\chrome.exe"
BROWSER_USER_DATA="C:\Users\YourUsername\AppData\Local\Google\Chrome\User Data"
USE_OWN_BROWSER=true
KEEP_BROWSER_OPEN=true
```

Example for macOS:

```env
BROWSER_PATH="/Applications/Google Chrome.app/Contents/MacOS/Google Chrome"
BROWSER_USER_DATA="/Users/YourUsername/Library/Application Support/Google/Chrome"
USE_OWN_BROWSER=true
```

Before starting an agent with an existing Chrome profile, close other Chrome windows that may already be using the same profile. You can then enable **Use Own Browser** from the Browser Settings section of the UI.

## Docker Setup

If you prefer Docker, create your `.env` file first and then run:

```bash
docker compose up --build
```

For ARM64 systems such as Apple Silicon:

```bash
TARGETPLATFORM=linux/arm64 docker compose up --build
```

After startup:

- **Web UI:** `http://localhost:7788`
- **VNC browser view:** `http://localhost:6080/vnc.html`

The default VNC password is defined in `.env`:

```env
VNC_PASSWORD=youvncpassword
```

Change it before using the project in a shared or exposed environment.

## Supported Configuration

The `.env.example` file includes settings for:

- LLM provider endpoints and API keys
- Default LLM selection
- Browser executable and user-data paths
- Browser debugging host/port
- Persistent browser sessions
- Browser CDP connection
- Screen resolution
- Logging level
- Anonymous telemetry
- VNC password

Do not commit your real `.env` file or API keys to GitHub.

## Running Tests

Tests are included for the agent, controller, LLM API integration, and Playwright setup.

```bash
pytest tests/
```

Some tests may require browser dependencies or valid provider configuration.

## Security

Keep all API credentials in environment variables and never hard-code secrets into source files. If you publish a fork of this project, review `.env`, logs, browser profiles, screenshots, and generated files before committing them.

For repository-specific security information, see [`SECURITY.md`](./SECURITY.md).

## Acknowledgements

This project builds on the open-source [`browser-use`](https://github.com/browser-use/browser-use) ecosystem. Credit also belongs to the upstream maintainers and community contributors whose work made the original Web UI implementation possible, including [WarmShao](https://github.com/warmshao).

Maintained in this repository by **Usman**.

## License

This repository retains the original open-source license and copyright notices. See [`LICENSE`](./LICENSE) for the applicable terms.
