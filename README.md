# Speech Services API

A Python-based speech services API that provides:

- **STT (Speech-to-Text)** using [Vosk]/[Whisper]
- **TTS (Text-to-Speech)** using [Piper]
- **VAD (Voice Activity Detection)** using [Silero VAD]
- **Unified WebSocket API** for real-time audio streaming (STT + TTS + VAD combined)

---

## Features

- Real-time **speech recognition and synthesis**
- Voice activity detection to detect speech start/stop
- Modular design: easily swap engines or add new providers
- Low-latency audio streaming via WebSocket
- HTTP TTS API for text-to-audio conversion

---

## Architecture

Frontend (AudioWorkletProcessor)
- captures audio → Float32 PCM frames
- converts to bytes → streams over WebSocket

Backend (Unified WS)
- receives audio chunks (bytes)
- VAD detects speech
- STT converts speech to text
- TTS converts text to audio for playback

---

## How I Used It

- Each service (STT, TTS, VAD) is implemented as a **provider class** with a common base interface.
- A **dispatcher** is used to initialize the correct service based on environment variables (`.env`).
- Models (Vosk, Whisper, Piper, Silero) are downloaded separately and loaded once per process for efficiency.
- Real-time communication happens via WebSocket (`unified_ws.py`), while TTS is also available via HTTP.
- Designed to be **modular**, so adding a new engine (e.g., Whisper, Coqui TTS, WebRTC VAD) only requires creating a new provider and registering it.

---