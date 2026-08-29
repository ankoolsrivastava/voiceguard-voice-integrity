# VoiceGuard

## Multilingual Real-Time Voice Integrity Assessment and Acoustic Spoof Detection Framework

VoiceGuard is an AI-powered voice-integrity project designed to determine whether speech is **BONAFIDE** or **SPOOF** under realistic recording and acoustic conditions.

The project focuses on **Hindi and Marathi** speech and is being developed as a reproducible, six-member collaborative engineering system with a planned integration-ready API for downstream applications.

> **Project principle:** Voice authenticity should be evaluated under realistic conditions—not only on clean laboratory audio.

---

## Problem

Modern speech systems can be exposed to synthetic, cloned, replayed, or otherwise manipulated speech. A detector that performs only on clean, controlled recordings may not remain reliable when the same speech passes through real microphones, rooms, devices, replay channels, or environmental noise.

VoiceGuard therefore treats acoustic and recording conditions as an explicit robustness dimension while keeping the authenticity decision separate:

```text
                         Voice Input
                              │
                              ▼
                    Audio Preprocessing
                              │
                              ▼
                    Feature Representation
                              │
                              ▼
                    Voice Spoof Detector
                              │
                    ┌─────────┴─────────┐
                    ▼                   ▼
                BONAFIDE             SPOOF
```

The eventual system is intended to expose this capability through an API so that external applications—such as banking, fintech, enterprise, or other voice-enabled systems—can integrate voice-integrity analysis into their own workflows.

**The API is a planned system component; production API claims are not made until the underlying model and service are actually implemented and validated.**

---

## Current Scope

| Area | Current scope/status |
|---|---|
| Target languages | **Hindi, Marathi** |
| Indian English | **Deferred / excluded from Dataset V1** |
| Prediction target | **BONAFIDE vs SPOOF** |
| Synthetic / TTS speech | In scope |
| Voice cloning | In scope |
| Replay speech | In scope |
| Environmental robustness | In scope |
| Realistic room/channel effects | In scope |
| Real dataset | **Complete and protected** |
| Robustness source collection | **Complete** |
| Room-01 RIR work | **Complete** |
| Final robustness augmentation policy | **Pending** |
| Full robustness generation | **Not started** |
| SPOOF data | **Pending receipt/audit** |
| Final Dataset V1 lock | **Not ready** |
| Final binary model training | **Not started** |
| Production API | **Planned** |

No model-performance numbers are reported here until the corresponding experiments have actually been run.

---

## Dataset Architecture

VoiceGuard Dataset V1 is organized around three pillars:

```text
                         DATASET V1
                             │
          ┌──────────────────┼──────────────────┐
          │                  │                  │
          ▼                  ▼                  ▼
        REAL               SPOOF           ROBUSTNESS
      bonafide             spoof        derived conditions
          │                  │                  │
          └──────────────────┼──────────────────┘
                             ▼
                   Global audit + leakage checks
                             │
                             ▼
                       Dataset V1 Lock
```

### REAL

The REAL pillar is the protected bonafide foundation.

Current verified state:

- Metadata rows: **4,613**
- Usable audio: **4,568**
- Duration exclusions: **45**
- Hindi usable: **3,165**
- Marathi usable: **1,403**
- Speakers: **424**
- Train: **3,180**
- Validation: **718**
- Test: **715**

The processed REAL audio standard is:

- WAV
- PCM 16-bit
- 16,000 Hz
- mono

The REAL audio, metadata, labels, parent mapping, and splits are protected and must not be modified casually.

### SPOOF

The SPOOF pillar is owned by the spoof-data track and is **pending receipt**.

When received, it must be audited before integration for:

- files and labels
- languages
- speakers
- spoof type
- generator/source
- generator version where available
- duplicates
- audio format and duration
- metadata completeness
- speaker leakage
- split leakage
- provenance

No substitute or fabricated spoof data is used to make the repository appear complete.

### ROBUSTNESS

Robustness is developed independently from the protected REAL dataset.

The purpose is to evaluate how authenticity detection behaves when speech encounters realistic conditions such as environmental noise, reverberation, channel/device effects, and replay-related conditions where feasible.

A robustness transformation **never changes the authenticity label**:

```text
REAL + noise      → bonafide
REAL + reverb     → bonafide
REAL + replay     → bonafide

SPOOF + noise     → spoof
SPOOF + reverb    → spoof
SPOOF + replay    → spoof
```

A derivative also remains in the same split as its parent.

---

## Robustness Work Completed So Far

The robustness track currently includes genuine environment-source collection and Room-01 acoustic measurement work.

### Environment recordings

**11 genuine environment recordings** have been collected and technically/human-QC approved.

The collected conditions include:

- fan / AC
- street
- road
- room

The accepted near-construction recording contains genuine construction/hammering activity together with wind/air noise. Natural secondary noise is not automatically treated as a reason for rejection.

### Room-01 RIR

Room-01 measured acoustic/system impulse-response work is complete.

The measurement chain was:

```text
Redmi → Bluetooth → E887 → Room → Phone microphone
```

Accordingly, the measurements are described as **effective acoustic/system impulse responses**, not as mathematically isolated room-only impulse responses.

Measured files include F16 and M14 T02 RIR recordings. Approximate RT20 values were:

- F16: 0.2739 s
- M14: 0.2628 s

T03 was intentionally not performed; T02 was selected.

### Reverb pilot

A controlled 8-file Room-01 reverb pilot has been generated from four REAL parents using the two measured RIRs.

This is a **pipeline pilot**, not the final robustness training dataset.

The pilot outputs were verified as:

- WAV
- PCM 16-bit
- 16,000 Hz
- mono
- duration-matched to parent clips

The final augmentation policy remains pending and must be defined, implemented reproducibly, tested on a controlled batch, QC'd, and validated before scaling.

---

## Model Direction

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

The project has already established the model/training infrastructure far enough to validate the REAL-data path, including preprocessing, Log-Mel feature extraction, model forward/backward execution, configuration, reproducibility, and training/evaluation scaffolding.

Final binary training is intentionally waiting for the genuine SPOOF pillar.

A later comparison against an appropriate pretrained anti-spoof model is planned as an empirical experiment. The repository will not assume beforehand which approach is superior.

---

## Evaluation Direction

Evaluation will eventually consider:

- overall performance
- Hindi
- Marathi
- clean conditions
- robustness conditions
- unseen speakers
- different spoof types
- realistic recording/channel conditions

Planned metrics include, where appropriate:

- Accuracy
- Precision
- Recall
- F1
- ROC-AUC / PR-AUC
- EER
- Confusion matrix
- False acceptance of spoof
- False rejection of bonafide
- Calibration/confidence

The held-out test set must remain untouched for fair final comparison.

---

## Repository Structure

The repository separates application code, reproducibility assets, documentation, evaluation material, and controlled metadata.

```text
voiceguard-voice-integrity/
│
├── README.md
├── CONTRIBUTING.md
├── .gitignore
│
├── docs/
│   ├── architecture/
│   ├── dataset/
│   ├── robustness/
│   ├── evaluation/
│   └── api/
│
├── src/
│   └── voiceguard/
│
├── scripts/
├── tests/
├── reports/
│
├── dataset_v1/
│   └── metadata/
│
└── robustness/
    ├── metadata/
    ├── reports/
    └── scripts/
```

Directories are populated only as the corresponding real project artifacts are migrated and verified. Raw/protected audio is intentionally excluded from version control.

---

## Metadata and Lineage

The master data schema includes fields such as:

```text
file_id
parent_file_id
speaker_id
language
language_name
split
label
source
source_dataset
original_filename
original_source_path
processed_audio_path
generator
generator_version
condition
environment
device
distance_m
transcript
text_id
duration_sec
sample_rate
channels
quality_status
notes
```

Core languages:

```text
HI
MR
```

Authenticity labels:

```text
bonafide
spoof
```

Every derived robustness sample must retain a valid `parent_file_id`, preserve its parent's language and split, and preserve its authenticity label.

---

## Quality Control

Final robustness data must be checked for:

- file existence
- audio readability
- WAV format
- 16,000 Hz
- mono
- 16-bit PCM
- positive duration
- correct metadata
- unique file ID
- unique processed path
- valid language
- valid label
- valid parent relationship
- split consistency
- duplicate IDs/paths
- missing parents
- invalid labels/languages

Final QC reporting is expected to cover sample counts, language, labels, conditions, splits, exclusions, audio failures, metadata failures, duplicates, parent relationships, and overall PASS/FAIL status.

---

## Reproducibility

VoiceGuard prioritizes reproducibility over raw file count.

The project uses:

- controlled preprocessing
- centralized configuration
- reproducibility/seed controls
- explicit dataset lineage
- deterministic or controlled generation where applicable
- validation before scaling
- documented QC
- speaker/split leakage checks

The operating principle is:

> **Quality + traceability + realistic robustness + reproducibility + Hindi/Marathi coverage + no data leakage**

A smaller, validated dataset is preferable to a larger undocumented or incorrectly labelled dataset.

---

## Data Safety

The repository must not contain, unless explicitly reviewed and permitted:

- private/raw personal recordings
- sensitive speaker information
- credentials or API keys
- `.env` files
- local virtual environments
- temporary QC listening copies
- unnecessary large audio collections
- model checkpoints without an intentional reason
- datasets whose licenses do not permit redistribution

The `.gitignore` provides baseline protection, but every contributor is responsible for reviewing files before committing them.

---

## API / System Integration

The long-term deployment direction is an integration-ready service that can be consumed by external applications.

Conceptually:

```text
External Application
        │
        │ audio / voice input
        ▼
   VoiceGuard API
        │
        ▼
 Voice Integrity Engine
        │
        ▼
 BONAFIDE / SPOOF
```

Potential consumers include banking, fintech, enterprise, and other systems that require voice-integrity analysis.

The API layer is **planned**. Endpoint names, authentication, rate limits, deployment architecture, and production guarantees will be documented only after the corresponding implementation exists.

---

## Team

VoiceGuard is a six-member collaborative project.

| Member | Responsibility | GitHub identity |
|---|---|---|
| Project Lead | REAL data, dataset architecture, validation, later ML/training/backend | @ankoolsrivastava |
| Friend 1 | SPOOF data | Pending |
| Friend 2 | ROBUSTNESS data | Pending |
| Member 4 | Pending | Pending |
| Member 5 | Pending | Pending |
| Member 6 | Pending | Pending |

Names and GitHub usernames are added only when supplied by the project team.

---

## Collaboration Workflow

`main` is the stable branch.

Contributors should normally work through feature branches and Pull Requests:

```text
feature/* / fix/* / docs/* / data/* / qc/*
                         │
                         ▼
                    Pull Request
                         │
                         ▼
                      Review
                         │
                         ▼
                    merge → main
```

See [`CONTRIBUTING.md`](CONTRIBUTING.md) for the contribution and dataset-integrity rules.

---

## Project Status

### Complete / Verified

- REAL dataset foundation
- REAL data QC and split validation
- REAL preprocessing and feature extraction foundation
- Custom CNN + BiGRU + Attention model implementation foundation
- REAL-data forward/backward pipeline verification
- Environment-source collection
- Environment technical QC
- Environment human acoustic QC
- Room-01 RIR measurement/extraction/numerical QC
- Room-01 controlled reverb pilot

### In Progress / Pending

- Final robustness augmentation policy
- Full environment augmentation
- Friend 1 SPOOF data receipt and audit
- REAL + SPOOF + ROBUSTNESS integration
- Global dataset audit
- Dataset V1 lock
- Final binary model training
- Final evaluation
- Production API implementation

### Explicitly Not Claimed

This repository does not currently claim final binary model accuracy, EER, production readiness, or API performance.

---

## Limitations

Current limitations include:

- final SPOOF data is pending
- final robustness augmentation policy is not yet locked
- final Dataset V1 is not yet locked
- final binary model training has not started
- production API is planned rather than completed
- classroom/office conditions must not be fabricated; genuine recordings must be collected and evaluated before inclusion

---

## Future Work

1. Receive and audit the SPOOF pillar.
2. Lock and implement the robustness augmentation policy.
3. Generate and QC controlled robustness data.
4. Integrate REAL, SPOOF, and ROBUSTNESS while preserving lineage and splits.
5. Perform global leakage and distribution audits.
6. Lock Dataset V1.
7. Train the final binary detector.
8. Evaluate clean and robustness conditions.
9. Compare the custom architecture with an appropriate pretrained anti-spoof model.
10. Develop and validate the integration-ready API.
11. Test end-to-end deployment under realistic recording/channel conditions.

---

## Scientific and Engineering Principle

VoiceGuard is intentionally developed as a **real, reproducible, scientifically defensible engineering project**.

Every repository claim should correspond to something that is:

- actually implemented,
- actually measured,
- actually collected,
- actually validated,
- or explicitly marked as planned/pending.

**No fake data. No fake results. No hidden leakage.**
