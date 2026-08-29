# Dataset Handling and Provenance

VoiceGuard separates reproducible repository artifacts from protected or potentially sensitive audio.

## Repository Boundary

The repository should contain code, documentation, appropriate metadata, QC reports, and reproducibility material that can be safely redistributed.

Protected/raw recordings and other large or restricted data must remain outside version control unless their provenance, licensing, privacy, and redistribution status have been explicitly reviewed.

## REAL Dataset

The REAL pillar is the protected bonafide foundation of Dataset V1.

Do not:

- rename REAL files
- delete REAL files
- reconvert REAL files
- modify REAL metadata
- change REAL labels
- change REAL splits

## Robustness Data

Robustness is developed independently from the REAL dataset.

Original environment recordings and measured RIR files must remain untouched. Derived data must remain separate from source data and must retain parent lineage.

## Provenance Requirements

Record provenance that is actually known, including source, generator/transformation, generator version where available, condition, environment, device, and other applicable metadata.

Do not infer or fabricate unavailable recording metadata. Use `NA` where the schema permits and the information is genuinely unavailable.

## Licensing and Redistribution

Before publishing any external dataset material, verify that its license permits the intended redistribution. A dataset being publicly downloadable does not by itself establish that its contents may be redistributed inside this repository.

## Sensitive Information

Do not publish private recordings, sensitive speaker information, credentials, API keys, `.env` files, or temporary listening/QC artifacts.

## Audit Before Integration

New data must be audited before entering Dataset V1. At minimum, review files, labels, languages, speakers, provenance, audio properties, duplicates, metadata completeness, speaker leakage, and split leakage as applicable to the source.
