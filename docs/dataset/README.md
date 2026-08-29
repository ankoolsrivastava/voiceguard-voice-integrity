# Dataset Documentation

VoiceGuard Dataset V1 is organized into three pillars:

- **REAL** — protected bonafide speech foundation.
- **SPOOF** — synthetic/cloned/replayed spoof data, pending receipt and audit.
- **ROBUSTNESS** — controlled environmental/acoustic derivatives with strict parent lineage.

## REAL Status

Current verified REAL statistics:

- Metadata rows: 4,613
- Usable audio: 4,568
- Duration exclusions: 45
- Hindi usable: 3,165
- Marathi usable: 1,403
- Speakers: 424
- Train: 3,180
- Validation: 718
- Test: 715

Audio standard:

- WAV
- PCM 16-bit
- 16,000 Hz
- mono

The REAL audio, metadata, labels, parent mapping, and splits are protected.

## Scope

Dataset V1 contains Hindi and Marathi only. Indian English is deferred and must not be added unless the project lead explicitly changes the scope.

## Labels

Authenticity labels are:

- `bonafide`
- `spoof`

Noise, reverberation, replay, device, and other acoustic factors are conditions, not authenticity labels.

## Lineage

Derived samples must retain `parent_file_id` and preserve the parent's language, label, and split.

Final Dataset V1 is not locked until the required data integration, global audit, leakage checks, and validation are complete.
