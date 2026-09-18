# Structured and Interaction-Aware P300 Decoding

This repository contains code and reproducibility material for a confirmatory
study of structured, Bayesian-informed, and interaction-aware P300 character decoding.

## Research questions

### Primary comparison

**GLASS-gated DBNet vs. Structured DBNet**

Primary endpoint: `Acc@4`.

### Secondary comparison

**Interaction DBNet vs. Structured DBNet**

The Interaction DBNet augments Structured DBNet with pairwise EEG-channel
features based on Fisher-z transformed Pearson correlations.

## Dataset and evaluation

Subjects: `A01-A08`

- 35 characters per subject
- 10 sequences per character
- 2 half-sequences per sequence
- 6 stimuli per half-sequence
- 8 EEG channels
- 128 samples per processed epoch

Channels: `Fz, Cz, Pz, Oz, P3, P4, PO7, PO8`

A frozen seven-fold outer protocol was used.

The independent statistical unit is the **subject** (`n = 8`).
Folds and seeds are not treated as independent statistical samples.

Neural-network seeds: `1, 2, 3`.

## Models

1. Pure GLASS
2. Binary DBNet with temperature `T = 1`
3. Structured DBNet
4. GLASS-gated DBNet
5. Interaction DBNet

### Frozen parameter counts

| Model | Parameters |
|---|---:|
| Structured DBNet | 3,961 |
| GLASS-gated DBNet | 4,986 |
| Interaction DBNet | 3,989 |
| Binary DBNet | 4,090 |

## Final A01-A08 results

| Model | NLL | Half-sequence accuracy | Acc@1 | Acc@4 | Acc@10 |
|---|---:|---:|---:|---:|---:|
| Pure GLASS | 1.1001 | 61.71% | 33.21% | 74.64% | 93.57% |
| Binary DBNet T=1 | 0.9863 | 68.68% | 41.79% | 83.93% | 96.79% |
| Structured DBNet | 0.9063 | 68.45% | 41.43% | 85.71% | 96.79% |
| GLASS-gated DBNet | 0.9198 | 68.09% | 40.36% | 85.36% | 97.50% |
| Interaction DBNet | 0.9076 | 68.71% | 42.50% | 86.43% | 96.79% |

## Confirmatory statistical results

### Primary: GLASS-gated minus Structured at Acc@4

- Mean difference: **-0.357 percentage points**
- Wins / ties / losses: **0 / 7 / 1**
- Exact paired sign-flip p-value: **1.000**
- 95% subject-bootstrap CI: **[-1.071, 0.000] pp**

The predefined primary hypothesis was **not supported**.

### Secondary: Interaction minus Structured at Acc@4

- Mean difference: **+0.714 percentage points**
- Wins / ties / losses: **2 / 5 / 1**
- Exact paired sign-flip p-value: **0.750**
- 95% subject-bootstrap CI: **[-0.714, +2.500] pp**

Interaction DBNet achieved a slightly higher observed mean Acc@4, but the
subject-level analysis did not provide evidence of a reliable improvement.

## Repository structure

```text
GLASS_GANet/
  integration/
    glass_tf220.py

code/
  confirmatory_eeg_ganet_overrides/
    README.md
    source_manifest.json
    common/
      GANs.py
      github_PreProcess.py
      github_PreTraining.py
    subject_finetuning/
      A01/ ... A08/

notebooks/
  confirmatory/
    01_structured_interaction_validation.ipynb
    02_confirmatory_model_training_evaluation.ipynb
    03_A07_A08_unattended_confirmatory_training.ipynb
    04_confirmatory_recovery_persistence.ipynb
```

Notebook outputs were removed before publication while preserving source code.

## EEG-GANet provenance

Upstream repository:

https://github.com/xicheng105/EEG-GANet

Pinned upstream commit:

`6c555030498338b349c74ddc723bf52716a0fa89`

Experiment-specific modified files are preserved under:

`code/confirmatory_eeg_ganet_overrides/`

Exact SHA-256 hashes are recorded in `source_manifest.json`.

The modified upstream code should not be interpreted as an entirely original implementation.

## GLASS provenance

Upstream repository:

https://github.com/BangyaoZhao/GLASS

Pinned commit:

`db32c2abd9211dec225a7f39a33963f8a0b21d7f`

The confirmatory protocol used the official GLASS prediction and character
evaluation logic.

## Pairwise interaction features

For eight channels:

`C(8,2) = 28`

For each channel pair:

1. Pearson correlation is calculated over the processed epoch.
2. Correlation is clipped before Fisher transformation.
3. Fisher-z transformation is applied.
4. The resulting 28 features are passed through the interaction branch.

## Reproducibility controls

- frozen seven-fold protocol
- frozen preprocessing
- frozen model definitions
- three predefined neural-network seeds
- checkpoint verification before outer-test access
- probability-level seed ensembling
- subject-level statistical inference
- folds and seeds are not treated as independent samples
- no post-outer temperature or model tuning

The completed confirmatory experiment should therefore be considered frozen.

## Data and trained models

Raw EEG data, processed arrays, trained checkpoints, generated GAN samples,
and large result files are intentionally excluded from this repository.

## Interpretation

Adding frozen GLASS evidence through a single nonnegative residual gate did
not improve the predefined early-sequence endpoint.

Pairwise Interaction DBNet produced a small numerical Acc@4 improvement,
but this difference was not statistically supported at the subject level.

These findings motivate follow-up work on temporal and higher-order EEG
interaction representations rather than additional tuning of the completed
confirmatory models.

## Initial cleaned confirmatory-code release

`ac569142bd1b96f1a62645e344f8fbc2ee3ff853`

## Status

```text
Subjects evaluated:      8/8
Confirmatory folds:      complete
Primary endpoint:        Acc@4
Inferential unit:        subject
Post-outer tuning:       none
Confirmatory analysis:   complete
```
