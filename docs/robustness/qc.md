# Robustness Quality Control

Every final robustness sample must be validated before it is accepted into the dataset.

## Audio Checks

Verify:

- file exists
- audio is readable
- WAV format
- PCM 16-bit
- 16,000 Hz
- mono
- positive duration

## Metadata Checks

Verify:

- unique `file_id`
- unique processed path
- valid `HI` or `MR` language
- valid `bonafide` or `spoof` label
- valid parent relationship
- parent language preserved
- parent authenticity label preserved
- parent split preserved
- provenance is documented where available

## Leakage Checks

Check for:

- duplicate IDs
- duplicate paths
- missing parents
- invalid parent references
- speaker leakage
- source/near-duplicate leakage across train, validation, and test

A derivative remains in the same split as its parent.

## Condition and Label Separation

Noise, reverberation, replay, room conditions, device effects, and similar factors are conditions. They do not change authenticity labels.

```text
bonafide + condition -> bonafide
spoof + condition    -> spoof
```

## Reporting

Final robustness QC reporting should include:

- total samples
- Hindi / Marathi counts
- bonafide / spoof counts
- condition counts
- train / validation / test counts
- usable / excluded samples
- missing audio
- invalid WAVs
- invalid sample rates
- invalid channels
- invalid durations
- duplicate IDs
- duplicate paths
- missing parents
- invalid labels
- invalid languages
- final PASS / FAIL

## Scaling Rule

Do not optimize for file count. Follow the controlled sequence:

```text
Define policy
    -> implement reproducibly
    -> small controlled batch
    -> QC
    -> lineage / leakage / distribution checks
    -> scale
```

The final augmentation policy must be explicitly defined before full-scale generation. No arbitrary SNR values, counts, ratios, or split allocations are assumed by this document.
