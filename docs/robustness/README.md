# Robustness Documentation

Robustness is developed independently from the protected REAL dataset.

## Current Status

- Genuine environment source collection: **complete**
- Environment technical QC: **complete**
- Environment human acoustic QC: **complete**
- Environment source manifest: **complete**
- Room-01 RIR measurement/extraction/numerical QC: **complete**
- Room-01 controlled reverb pilot: **complete**
- Final augmentation policy: **pending**
- Full environment augmentation: **not started**

## Environment Sources

11 genuine environment recordings have been collected across fan/AC, street, road, and room conditions.

The accepted near-construction recording contains genuine construction/hammering activity plus wind/air noise. Natural secondary noise is not automatically treated as grounds for rejection.

## Room-01 RIR

The measured RIR work uses the following chain:

```text
Redmi → Bluetooth → E887 → Room → Phone microphone
```

These measurements are therefore described as effective acoustic/system impulse responses rather than mathematically isolated room-only impulse responses.

Approximate RT20:

- F16: 0.2739 s
- M14: 0.2628 s

T03 was intentionally not performed; T02 was selected.

## Reproducibility Rules

The final augmentation policy must be defined before scaling. The required sequence is:

```text
Define policy
    ↓
Implement reproducibly
    ↓
Small controlled batch
    ↓
QC
    ↓
Lineage / leakage / distribution checks
    ↓
Scale
```

No arbitrary final SNR values, counts, ratios, or split allocations are assumed before the policy is locked.

## Label Preservation

Robustness transformations never change authenticity labels.

```text
bonafide + condition → bonafide
spoof + condition    → spoof
```

Every derivative must retain `parent_file_id` and remain in the parent's split.
