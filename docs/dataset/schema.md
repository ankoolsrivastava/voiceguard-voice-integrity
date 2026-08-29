# Dataset Metadata Schema

VoiceGuard uses metadata to preserve dataset identity, provenance, lineage, split integrity, and quality information.

## Core Fields

The master schema includes:

| Field | Purpose |
|---|---|
| `file_id` | Unique identifier for the sample |
| `parent_file_id` | Parent source identifier for derived samples |
| `speaker_id` | Speaker identifier where available and permitted |
| `language` | Core language code (`HI` or `MR`) |
| `language_name` | Human-readable language name |
| `split` | Dataset split (`train`, `validation`, or `test`) |
| `label` | Authenticity label (`bonafide` or `spoof`) |
| `source` | Source/provenance category |
| `source_dataset` | Dataset/source collection identifier |
| `original_filename` | Original source filename |
| `original_source_path` | Original source location where appropriate |
| `processed_audio_path` | Path to the processed/derived sample |
| `generator` | Generator or transformation used, where applicable |
| `generator_version` | Generator/transformation version, where available |
| `condition` | Applied recording/acoustic condition |
| `environment` | Environment category, where applicable |
| `device` | Recording/playback device, where known |
| `distance_m` | Source/device distance in metres, where known |
| `transcript` | Associated speech text, where available |
| `text_id` | Text identifier, where available |
| `duration_sec` | Audio duration in seconds |
| `sample_rate` | Audio sample rate |
| `channels` | Number of audio channels |
| `quality_status` | QC status |
| `notes` | Additional provenance/QC information |

## Allowed Core Values

Languages:

```text
HI
MR
```

Authenticity labels:

```text
bonafide
spoof
```

## Label Preservation

Acoustic or recording conditions do not define authenticity labels.

Examples:

```text
bonafide + noise   -> bonafide
bonafide + reverb  -> bonafide
spoof + noise      -> spoof
spoof + reverb     -> spoof
```

## Lineage Rule

Every derived robustness sample must retain `parent_file_id` and preserve the parent's language, authenticity label, and split.

## Missing Information

Metadata must never be fabricated. When a field is genuinely unavailable and the schema permits an unavailable value, use `NA` rather than inventing a value.

## Data Integrity

Changes to protected REAL metadata require explicit project-level review. Dataset V1 is not considered locked until integration, global audit, leakage checks, and validation are complete.
