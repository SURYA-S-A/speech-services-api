# Speech Services API

A Python-based speech services API that provides:

- **STT (Speech-to-Text)** using [Vosk/Whisper]
- **TTS (Text-to-Speech)** using [Piper]
- **VAD (Voice Activity Detection)** using [Silero VAD]
- **Unified WebSocket API** for real-time audio streaming (STT + TTS + VAD combined)

---

## How I Used It

- Each service (STT, TTS, VAD) is implemented as a **provider class** with a common base interface.
- A **dispatcher** is used to initialize the correct service based on environment variables (`.env`).
- Models (Vosk, Piper, Silero) are downloaded separately and loaded once per process for efficiency.
- Real-time communication happens via WebSocket (`unified_ws.py`), while TTS is also available via HTTP.
- Designed to be **modular**, so adding a new engine (e.g., Whisper, Coqui TTS, WebRTC VAD) only requires creating a new provider and registering it.

---
