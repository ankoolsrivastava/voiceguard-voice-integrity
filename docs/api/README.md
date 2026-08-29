# API Documentation

VoiceGuard is intended to become an integration-ready voice-integrity service that external applications can consume.

## Intended Flow

```text
External application
        │
        │ voice/audio input
        ▼
   VoiceGuard API
        │
        ▼
 Voice Integrity Engine
        │
        ▼
 BONAFIDE / SPOOF
```

Potential consumers include banking, fintech, enterprise, and other voice-enabled systems.

## Current Status

The API layer is **planned**. The underlying binary model is not yet final because the SPOOF pillar is pending. Therefore production endpoints, authentication, rate limits, latency, deployment guarantees, and performance claims are intentionally not documented as implemented capabilities.

When the API is implemented, this section will document its request/response contract, authentication, validation, error handling, model versioning, deployment, and integration examples.
