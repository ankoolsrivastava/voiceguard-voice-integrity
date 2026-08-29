# Architecture

## Current Direction

VoiceGuard is designed as a voice-integrity analysis system whose final authenticity decision is **BONAFIDE vs SPOOF**.

The current custom-model direction is:

```text
Audio
  ↓
Preprocessing
  ↓
Log-Mel representation
  ↓
CNN
  ↓
BiGRU
  ↓
Attention
  ↓
BONAFIDE / SPOOF
```

The broader system direction is:

```text
Audio input
    ↓
Preprocessing
    ↓
Representation / features
    ↓
Spoof-detection model
    ↓
Calibrated probability / decision
    ↓
BONAFIDE or SPOOF
```

A later pretrained anti-spoof model comparison is planned as an empirical experiment. No model is assumed to be superior before measurement.

## Deployment Direction

The eventual system is intended to expose voice-integrity analysis through an integration-ready API. API implementation is planned and must not be represented as production-ready until it has actually been implemented and validated.
