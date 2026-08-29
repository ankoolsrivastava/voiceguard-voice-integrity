# Contributing to VoiceGuard

Thank you for contributing to VoiceGuard.

VoiceGuard is a six-member collaborative engineering project focused on
multilingual real-time voice integrity assessment and acoustic spoof
detection for Hindi and Marathi speech.

The repository follows a controlled contribution workflow to protect
dataset integrity, reproducibility, model evaluation, and project history.

---

## 1. Core Development Principle

Every contribution must preserve:

- data integrity
- provenance and traceability
- reproducibility
- speaker-disjoint evaluation
- split integrity
- realistic robustness
- Hindi/Marathi language scope
- scientific validity

Do not add fabricated, placeholder, demo, or synthetic project data
unless it is explicitly part of a documented experimental procedure.

---

## 2. Main Branch

`main` is the stable project branch.

Do not push experimental or unfinished work directly to `main`.

Changes should normally be developed on a separate branch and submitted
through a Pull Request.

---

## 3. Branch Naming

Use descriptive branch names.

Examples:

```text
feature/<short-description>
fix/<short-description>
docs/<short-description>
experiment/<short-description>
data/<short-description>
qc/<short-description>
refactor/<short-description>
