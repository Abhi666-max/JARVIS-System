<div align="center">
  <img src="assets/logo.jpg" alt="JARVIS AI System Logo" width="220"/>
  <h1>JARVIS System</h1>
  <p><b>The Ultimate Cross-Platform Personal AI Assistant</b></p>
  <p>Engineered by Abhijeet</p>
</div>

---

A real-time, voice-activated artificial intelligence assistant designed to perceive, understand, and autonomously control your desktop environment. Engineered for Windows, macOS, and Linux, JARVIS leverages the ultra-low latency **Gemini 3.1 Flash Live API** to deliver seamless bidirectional audio streaming and complete digital autonomy.

---

## 1. System Overview

JARVIS is engineered to act as a hyper-tactical AI agent capable of local OS execution, proactive system monitoring, and multi-step autonomous workflows. It departs from standard turn-based LLM chat interfaces by implementing continuous, duplex audio streaming and executing local system commands in real time.

Operating under an optimized local wake-word detector, JARVIS remains dormant to conserve system resources. When summoned with **"Hey JARVIS"**, the system connects instantly, delivering immediate auditory acknowledgment before executing complex system scripts, filesystem operations, and web-crawling protocols.

---

## 2. Core Architecture & Algorithms

The system employs an asynchronous, multi-threaded architecture to decouple audio ingestion, UI rendering, and AI inference.

### 2.1 WebSockets & Full Duplex Audio
JARVIS relies on a persistent WebSocket connection to the Gemini Live API. Instead of recording a full sentence and sending it as a file, the system streams raw PCM audio chunks continuously. Speech-to-Text (STT) and Text-to-Speech (TTS) are handled server-side by the model, enabling the assistant to interrupt itself, listen while speaking, and respond with near-zero latency.

### 2.2 Dynamic Tool Dispatcher
The architecture follows a strict decoupled pattern for skills. `actions/` and `plugins/` directories act as registries. At startup, the `action_loader.py` scans these directories, extracts structured `TOOL` schemas, and builds the LLM context dynamically. When the LLM decides to execute an action, it fires a function call that the dispatcher resolves in microseconds. Adding a new skill requires zero core modification—simply drop a `.py` file into the folder.

### 2.3 Semantic Memory Engine
Context window limitations are bypassed using a sliding-window compression technique combined with a local vector-like semantic store. Persistent data, user identity, preferences, and multi-session projects are written to `memory/long_term.json`. A background search algorithm fetches relevant historical context dynamically based on the current conversational focus.

### 2.4 Autonomous Safety Gate
High-risk OS operations (e.g., system shutdown, destructive file removals, firewall modifications) are routed through a strict UI-level confirmation gate. The LLM is structurally blocked from forging a confirmation token, ensuring zero risk of catastrophic hallucination. Reversible tasks use a global LIFO Undo stack.

---

## 3. Comprehensive Feature Set

### Audio & Inference
- **Local Wake Word Detection:** Fully offline detection using `openwakeword`. Zero cloud telemetry until activated.
- **Instant Acknowledgment:** Intelligent interrupt system that provides immediate feedback before commencing high-latency tasks like deep web searches or code compilation.
- **Gemini 3.1 Flash Live:** Utilizes the absolute fastest reasoning model currently available.

### System & File Autonomy
- **Full File System Control:** Read, write, move, create, and organize local files programmatically.
- **System Telemetry:** Real-time extraction of CPU load, RAM utilization, GPU state, and thermals.
- **Hardware Integration:** Control system volume, display brightness, networking, and power states natively on Windows, macOS, and Linux.

### Vision & Web Automation
- **Real-Time Visual Processing:** Captures screen context and webcam streams, piping visual data directly into the AI's reasoning engine.
- **Headless Browser Control:** Powered by Playwright to autonomously navigate URLs, scrape data, extract prices, and conduct academic research.

### Proactive Intelligence
- **Morning Briefing Engine:** On the first boot of the day, JARVIS synchronizes the time, summarizes the previous day's context, and fetches live headlines.
- **Background Watchers:** User-configured topic monitoring running on a scheduled chron-job.
- **Session Continuity:** Network dropouts or voice changes are handled gracefully without losing the conversational context.

---

## 4. Technical Stack

- **Intelligence Layer:** Google Gemini Live API
- **Audio I/O Handling:** PyAudio, sounddevice
- **Wake Word Engine:** openwakeword, ONNX Runtime
- **Graphical Interface:** PyQt6
- **Web Automation:** Playwright
- **Configuration & State:** JSON, OS Environment Variables
- **Language Requirements:** Python 3.11 or Python 3.12

---

## 5. Complete Setup Guide

### 5.1 Prerequisites
- Operating System: Windows 10/11, macOS, or Linux.
- Python: Version 3.11 or 3.12 is strictly required (3.13+ may not support certain audio dependencies natively).
- Hardware: A functional, accessible microphone and audio output device.
- API Key: A valid Google Gemini API Key.

### 5.2 Clone and Install

Clone the repository locally:
```bash
git clone https://github.com/Abhi666-max/JARVIS-System.git
cd JARVIS-System
```

Execute the OS-aware setup script. This script automatically detects your platform and installs the precise dependencies required, circumventing cross-platform compilation errors.
```bash
python setup.py
```
*(Alternatively, power users can run `pip install -r requirements.txt`)*

### 5.3 First Boot Configuration

Launch the main loop:
```bash
python main.py
```

On the initial boot, JARVIS will present a UI setup screen. You will be prompted to:
1. Provide your **Gemini API Key**.
2. Select your exact hardware Audio Input (Microphone) and Audio Output (Speakers) from the measured hardware list.
3. Configure your assistant name ("JARVIS") and your personal identity.

### 5.4 Enabling the Wake Word
The Wake Word engine is an optional opt-in due to the heavy ONNX binary. To enable true hands-free operation:
1. Open the JARVIS Settings UI.
2. Toggle the **Wake Word** option.
3. The system will autonomously download the required local AI model.
4. From now on, simply say **"Hey JARVIS"** to initiate communication.

---

## 6. Directory Structure

```text
JARVIS-System/
├── actions/                  # Core executable skills (System control, web search, file management)
├── assets/                   # Static application assets and branding
├── config/                   # Local configuration, keys, and UI state (Generated at runtime)
├── core/                     # Internal engine logic (LLM client, Audio I/O, Tool Discovery, TTS/STT)
├── dashboard/                # Remote web interface backend for mobile pairing
├── memory/                   # Persistent local JSON storage for identity and context
├── plugins/                  # Directory for user-created drop-in Python extensions
├── main.py                   # Main asynchronous execution loop
├── ui.py                     # PyQt6 Graphical User Interface rendering engine
├── setup.py                  # Intelligent OS-aware dependency installer
└── requirements.txt          # Complete dependency manifest
```

---

## 7. Development & Customization

JARVIS is built for extreme extensibility. To create a new capability, copy `plugins/_template.py`, define your Python function, map its parameters in the `PLUGIN` dictionary, and drop it into the `plugins/` directory. JARVIS will instantly parse the function syntax, pass the schema to the LLM, and learn how to use it on the next boot.

---

## 8. License

This software is for personal and non-commercial use only.
Licensed under **[Creative Commons BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/)**.

---

## 9. Connect with the Creator

Engineered by Abhijeet.
Star the repository to support the development and evolution of the JARVIS System.

- **GitHub:** [abhi666-max](https://github.com/abhi666-max)
- **LinkedIn:** [Abhijeet Kangane](https://www.linkedin.com/in/abhijeet-kangane/)
- **X (Twitter):** [abhijeet_037](https://x.com/abhijeet_037)
- **Instagram:** [abhijeet.037](https://www.instagram.com/abhijeet.037/)
