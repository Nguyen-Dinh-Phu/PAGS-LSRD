# PAGS–LSRD

**MATLAB implementation of multi-objective topology optimization for orthotropic composite robot-arm structures**, combining Level Set–Reaction Diffusion (LS–RD) with Paraxial Alignment Geometric Stability (PAGS).

**Authors:** Le Thi Bich Nam, Dinh Phu Nguyen, Van Hanh Dang, TienDung Vu.

## Project structure

```text
PAGS-LSRD/
├── MAIN.m             # Main script and input parameters
├── FUNCTION/           # FEM, PAGS, LS-RD and plotting functions
├── README.md
└── .gitignore
```

## How to run

1. Download or clone this repository.
2. Open MATLAB and set the current folder to the repository root.
3. Run:

```matlab
MAIN
```

Set `study.runMode` in `MAIN.m` to `'history'`, `'sweep'` or `'all'`.

## Default settings

- Q4 mesh: **360 × 90** elements; domain: **120 × 30 mm**
- Load: **5,000 N** (downward, case 3)
- Volume fraction: **0.60**; optimization iterations: **400**
- Fiber orientations: **0°, 30°, 45°, 60°**
- PAGS weights for sweep: **0, 0.1, 0.2, 0.3, 0.4, 0.5**
