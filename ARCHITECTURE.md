# 🏛️ JARVIS 3.0 — Architecture Deep Dive

Designed & Engineered by **Praveen Suthar**  
Repository: [https://github.com/Praveen-Suthar-08/JARVIS-3.0-Assistant.git](https://github.com/Praveen-Suthar-08/JARVIS-3.0-Assistant.git)

---

## 📌 Executive Summary

**JARVIS 3.0 (Mark LV)** is built upon a high-performance, non-blocking asynchronous architecture designed for sub-second real-time voice intelligence and deep local operating system control.

---

## 🧠 1. The 9-Model Failover Ladder Engine

To achieve continuous resilience against API rate limits, timeouts, and regional cloud outages, JARVIS routes all LLM calls through a prioritized 9-model ladder:

```
[ Incoming User Intent ]
          │
          ▼
┌──────────────────┐
│  Gemini 2.5 Live │ ── (Primary: Sub-300ms Audio Stream)
└─────────┬────────┘
          │ (Timeout / Quota Reached / 503 Outage)
          ▼
┌──────────────────┐
│  Gemini 2.0 Live │ ── (Fallback 1)
└─────────┬────────┘
          │
          ▼
┌──────────────────┐
│  Gemini 1.5 Pro  │ ── (Fallback 2: Deep Context & Complex Logic)
└─────────┬────────┘
          │
          ▼
    [ ... Rungs 4 through 9 ... ]
```

### Key Capabilities:
- **Measured Response Order:** Models are prioritized dynamically based on latency metrics.
- **Quarantine Cooldown:** Failed endpoints are quarantined for 15 minutes before retry to eliminate redundant network retries.

---

## 👄 2. Real-Time Lip-Sync & Holographic Renderer

The PySide6 HUD renders a 3D facial mesh without heavy external GPU engines:

1. **Audio Formant Extraction:** Speech synthesis outputs are sampled at ~50 Hz.
2. **Viseme Mapping:** Spectral formants and Unicode phonemes map directly to viseme mouth targets (closures, spreads, rounds).
3. **Software Geometry Deform:** Facial mesh vertices deform in real-time in the HUD viewport with ambient lighting.

---

## ⚡ 3. System Action Execution & Skill Matrix

```
┌────────────────────────────────────────────────────────┐
│                     ACTION LOADER                      │
│             (Auto-Discovery Skill Engine)              │
└──────────────────────────┬─────────────────────────────┘
                           │
       ┌───────────────────┼───────────────────┐
       ▼                   ▼                   ▼
┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│  Desktop OS  │    │  Media HUD   │    │ Vector Memory│
│  Control     │    │  (yt-dlp)    │    │ Lookup       │
└──────────────┘    └──────────────┘    └──────────────┘
```

- **Self-Describing Plugins:** Plugins declare a `TOOL` schema dictionary and `execute()` handler.
- **Safety Safeguard Engine:** Potentially destructive operations (e.g. system shutdown, disk wiping) require mandatory user UI confirmation.

---

## 🤝 Author & License

Developed by **Praveen Suthar** — Released under the MIT License.
