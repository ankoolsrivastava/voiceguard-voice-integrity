# Security and Data Handling

VoiceGuard works with speech recordings and machine-learning artifacts that may contain sensitive information. Security and data provenance are part of the engineering requirements.

## Do Not Commit

Do not commit:

- private or raw personal recordings
- sensitive speaker information
- credentials, API keys, or secrets
- `.env` files
- local virtual environments
- temporary QC listening copies
- unnecessary large audio collections
- model checkpoints unless intentionally approved
- datasets whose license does not permit redistribution

Audio files are ignored by default in `.gitignore`.

## Dataset Integrity

The protected REAL dataset must not be renamed, deleted, reconverted, relabelled, or repartitioned through ordinary repository work.

Robustness derivatives must preserve parent-file lineage, language, authenticity label, and split.

## Reporting a Security/Data Issue

Do not publish sensitive data or credentials in a GitHub issue. Contact the project lead privately with enough information to reproduce or assess the issue without exposing protected material.
