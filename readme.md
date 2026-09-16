<div align="center">
  <img src="assets/logo.jpg" alt="JARVIS AI" width="200"/>
  <h1>JARVIS System</h1>
  <p><b>The Ultimate Cross-Platform Personal AI Assistant</b></p>
  <p>Engineered by Abhijeet</p>
</div>

---

A real-time voice-activated AI assistant designed to see, understand, and control your computer environment across any operating system (Windows, macOS, Linux). Powered by the Gemini Live API for native audio streaming, JARVIS delivers an unparalleled, ultra-low latency conversational experience with complete digital autonomy.

---

## Overview

JARVIS is built as a hands-free, scalable, and hyper-tactical AI agent. Operating with an optimized local wake-word engine, JARVIS remains dormant to conserve system resources until explicitly summoned. When activated, it seamlessly interfaces with the Gemini 3.1 Flash Live engine to execute complex multi-step workflows, perform local file system operations, and provide immediate auditory feedback.

The system is designed with modularity in mind. Every capability is encapsulated as an independent skill (either bundled or drop-in), enabling rapid extension of the assistant without altering the core loop.

---

## Technical Stack

- **Core Intelligence:** Google Gemini 3.1 Flash Live API
- **Audio Processing:** PyAudio, sounddevice, native OS audio APIs (DirectSound, WASAPI)
- **Wake Word Engine:** openwakeword (local, offline inference)
- **UI & Visualization:** PyQt6 (Reactive HUD, Waveform Generation)
- **Browser Automation:** Playwright
- **Cross-Platform Compatibility:** Python 3.11/3.12 (Windows, macOS, Linux)

---

## System Architecture & Workflow

JARVIS employs a multi-threaded architecture to decouple audio ingestion, UI rendering, and AI inference.

1. **Wake Word Subsystem:** A dedicated lightweight thread continuously monitors the microphone buffer using an offline model. Audio is never streamed to the cloud during this phase.
2. **Audio Streaming & NLP:** Upon detecting the wake word, the system establishes a bidirectional WebSockets stream with the Gemini Live API. Speech-to-Text and Text-to-Speech are handled natively by the model, ensuring minimal latency.
3. **Action Dispatcher (Tool Calling):** When JARVIS determines an action is required, the model issues a structured tool call. The `action_loader.py` engine resolves this call against a dynamically discovered registry of Python modules located in the `actions/` and `plugins/` directories.
4. **Execution & Confirmation:** Highly privileged operations (e.g., system shutdown, irreversible file operations) trigger a UI-level confirmation gate, bypassing the LLM to prevent autonomous hallucination errors. Reversible actions are executed immediately and pushed to a global Undo stack.
5. **Memory Management:** Context is compressed via a sliding window. Persistent data (user preferences, project contexts) is stored locally in `memory/long_term.json` and recalled on demand via vector-like semantic matching.

---

## Capabilities

- **Local Wake Word Detection:** Fully offline detection. Auto-sleeps after 2 minutes of silence.
- **Dynamic Tool Dispatching:** Modular architecture where actions self-describe their parameters.
- **Autonomous File System Control:** Read, write, move, and organize files locally.
- **System Telemetry & Control:** Monitor CPU, RAM, GPU, and temperature. Control volume, brightness, power state, and networking.
- **Browser & Web Automation:** Perform web research, navigate URLs, and extract data autonomously.
- **Visual Awareness:** Real-time screen capture and webcam parsing injected into the AI context.
- **Proactive Intelligence:** Context-aware background monitoring and morning briefings based on historical memory.
- **Persistent Memory & Undo:** Remembers long-term context indefinitely. Reverses destructive actions (e.g., moving files) via voice command.

---

## Installation & Setup

### Requirements

- OS: Windows 10/11, macOS, or Linux
- Python: 3.11 or 3.12
- Hardware: Functional Microphone and Speakers
- API: A free Google Gemini API Key

### Quick Start

1. **Clone the repository:**
   ```bash
   git clone https://github.com/Abhi666-max/JARVIS-System.git
   cd JARVIS-System
   ```

2. **Install dependencies:**
   The `setup.py` script automatically detects your OS and installs only the required dependencies.
   ```bash
   python setup.py
   ```

3. **Launch the system:**
   ```bash
   python main.py
   ```
   *Note: On the first launch, the system will prompt you for your Gemini API key.*

### Directory Structure

```text
JARVIS-System/
├── actions/                  # Core bundled skills (System control, web search, file management)
├── assets/                   # Static assets (Logos, icons)
├── config/                   # Configuration files (API keys, UI settings)
├── core/                     # System engines (Prompt logic, LLM client, Audio I/O, Plugin Loader)
├── dashboard/                # Remote web interface for mobile control
├── memory/                   # Persistent local storage (Identity, long-term memory)
├── plugins/                  # User-created drop-in extensions
├── main.py                   # Application entry point and core loop
├── ui.py                     # PyQt6 Graphical User Interface
└── setup.py                  # OS-aware dependency installer
```

---

## License

Personal and non-commercial use only.
Licensed under **[Creative Commons BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/)**.

---

## Connect with the Creator

Engineered by Abhijeet.
Star the repository to support the development of JARVIS.

- **GitHub:** [abhi666-max](https://github.com/abhi666-max)
- **LinkedIn:** [Abhijeet Kangane](https://www.linkedin.com/in/abhijeet-kangane/)
- **X (Twitter):** [abhijeet_037](https://x.com/abhijeet_037)
- **Instagram:** [abhijeet.037](https://www.instagram.com/abhijeet.037/)
