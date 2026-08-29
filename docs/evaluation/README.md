# Evaluation Documentation

VoiceGuard evaluation is intended to measure BONAFIDE vs SPOOF detection under both clean and realistic conditions.

## Planned Evaluation Dimensions

- overall performance
- Hindi
- Marathi
- clean conditions
- robustness conditions
- unseen speakers
- different spoof types
- realistic recording/channel conditions

## Planned Metrics

Where appropriate:

- accuracy
- precision
- recall
- F1
- ROC-AUC / PR-AUC
- EER
- confusion matrix
- false acceptance of spoof
- false rejection of bonafide
- calibration/confidence

## Evaluation Integrity

The held-out test set must remain untouched for fair model comparison. Speaker and source leakage must be checked before final evaluation.

No final performance numbers are reported until the corresponding experiments have actually been executed and validated.
