# Replication and verification guide

This document describes the **available MATLAB implementation**, not a confirmed verification outcome.

## Requirements

- MATLAB with support for the plotting functions used in `PAGS_Output.m` (including `tiledlayout` and `MarkerIndices`).
- Source tree preserved with `MAIN.m` at root and helper functions under `FUNCTION/`.

## Execution

```matlab
cd('path/to/PAGS-LSRD')
MAIN
```

Change `study.runMode` in `MAIN.m` to `history`, `sweep`, or `all`. The full-resolution default uses a 360 × 90 Q4 background mesh, with 400 iterations per case.

The `history` mode generates the baseline and four orientation-dependent responses; `sweep` evaluates 24 weight/orientation combinations. Neither mode writes result files or generates Fig. 3. Figures are displayed in MATLAB and the numeric result struct is returned to `studyResults` in the workspace.

## Model and input checks

1. Confirm `MAIN.m` finds every helper function under `FUNCTION/` using `which ApplyBC -all`, `which PAGS_Study -all`, and `which PAGS_LSRD -all`.
2. Confirm applied total vertical force, supports, hole geometry, and passive zones for boundary-condition case `'3'`.
3. Test Q4 local-node and global DOF ordering through an affine displacement patch test and rigid-body zero-strain test.
4. Check that the FE material stiffness and model dimensions use a consistent unit system.
5. Verify compliance and CG–RC sensitivities with central finite differences at more than one orientation.
6. Check that the element-to-node sensitivity projection and reaction–diffusion update correspond to the **implemented numerical method**, not an assumed exact gradient in `phi`.

## Manuscript replication

- Re-run the `history` mode, then the `sweep` mode at the original mesh resolution.
- Record MATLAB release, machine configuration, commit SHA, stopping conditions, and any divergence or singular stiffness errors.
- Compare compliance, volume fraction, CG–RC distance, objectives and final topologies with the manuscript at equal settings.
- Keep a clear distinction between stored iteration metrics (before updates) and the final post-update metrics.
- Do not describe numerical validation as PASS until the corresponding MATLAB tests have been run.

## Current publication scope

This repository intentionally retains the authors' existing calculation methods; the organization-only commit that placed files in `FUNCTION/` does not amend scientific algorithms or regenerate manuscript figures. The code is supplied for inspection and subsequent reproducibility evaluation.
