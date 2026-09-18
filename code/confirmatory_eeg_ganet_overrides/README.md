# Modified EEG-GANet source used in the confirmatory experiments

## Upstream source

Repository:

`https://github.com/xicheng105/EEG-GANet.git`

Pinned upstream commit:

`6c555030498338b349c74ddc723bf52716a0fa89`

The files in this directory are modified experiment-specific versions derived
from the upstream EEG-GANet implementation.

## Common modified files

The following files were byte-identical across subjects A01-A08:

- `common/GANs.py`
- `common/github_PreProcess.py`
- `common/github_PreTraining.py`

Their SHA-256 hashes are recorded in `source_manifest.json`.

## Subject-specific fine-tuning files

`github_FineTuning.py` differed for every subject.

The exact versions are therefore preserved under:

- `subject_finetuning/A01/`
- `subject_finetuning/A02/`
- `subject_finetuning/A03/`
- `subject_finetuning/A04/`
- `subject_finetuning/A05/`
- `subject_finetuning/A06/`
- `subject_finetuning/A07/`
- `subject_finetuning/A08/`

## Excluded material

Generated datasets, model checkpoints, GAN outputs, pretraining outputs,
Python caches, and historical backup scripts are intentionally not included
in this source bundle.

The complete experimental model definitions and confirmatory workflow are
preserved separately under `notebooks/confirmatory/`.

## Provenance note

This directory contains modifications to upstream EEG-GANet code. It should
not be described as an entirely original implementation. The upstream project
and its authors must be cited according to the applicable license and paper.
