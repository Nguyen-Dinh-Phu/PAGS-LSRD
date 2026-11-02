# PAGS–LSRD: Topology Optimization of a Composite Robot Arm

Research MATLAB source for **Paraxial Alignment Geometric Stability (PAGS)** combined with **Level Set–Reaction Diffusion (LS–RD)** topology optimization of an orthotropic composite robotic-arm link.

**Authors:** Le Thi Bich Nam, Dinh Phu Nguyen, Van Hanh Dang, TienDung Vu.

**Research status:** Source release for reproducibility and review. The manuscript's numerical results have **not yet been independently reproduced** using this published repository. This README does not imply journal acceptance.

## Repository structure

```text
PAGS-LSRD/
├── MAIN.m                         # Entry point and study parameters
├── FUNCTION/
│   ├── Domain.m
│   ├── ApplyBC.m
│   ├── GetMeshInfo.m
│   ├── InitializeSystem.m
│   ├── AnalyzeFEM_PAGS_FixedTheta.m
│   ├── Calculate_RC0.m
│   ├── ElementToNodalSensitivity.m
│   ├── PhiToDensity.m
│   ├── ApplyPassivePhi.m
│   ├── LVS.m
│   ├── PAGS_LSRD.m
│   ├── PAGS_Study.m
│   └── PAGS_Output.m
├── README.md
├── REPLICATION_GUIDE.md
└── .gitignore
```

## Running in MATLAB

1. Download or clone the repository, keeping the `FUNCTION/` folder intact.
2. Set the MATLAB current folder to the repository root.
3. Run:

```matlab
MAIN
```

`MAIN.m` adds the project root and `FUNCTION/` to the MATLAB path. Select `study.runMode = 'history'`, `'sweep'`, or `'all'` in `MAIN.m`.

### Default study

- Robot-arm domain: 120 × 30 (model coordinate units), background Q4 mesh: 360 × 90 elements.
- Applied total load (case 3): `F = 5000` N, downward in the current implementation.
- Orthotropic properties in `MAIN.m`: `E11 = 73.2e9` Pa, `E22 = 4.1e9` Pa, `G12 = 2.23e9` Pa, `nu12 = 0.33`.
- Volume fraction limit: 0.60; 400 iterations per optimization case.
- `history`: baseline `w = 0` and four `w = 0.4` cases at 0°, 30°, 45°, and 60°.
- `sweep`: 24 cases combining `w = 0:0.1:0.5` and angles 0°, 30°, 45°, and 60°.

## Figures and output

The source displays MATLAB figures corresponding to **Fig. 4 onward** and the topology matrix. **Fig. 3 is not generated**, and no `Results/` directory or PNG/CSV/MAT exports are created. MATLAB responses remain in the `studyResults` workspace variable.

## Numerical verification and scientific limitations

The provided source has not been executed or benchmarked here in MATLAB. Before citing its output as an independently reproduced result, verify the Q4 element local-node / global-DOF ordering, material and geometry conventions, supports and loads, sensitivities, and agreement with manuscript figures and tables. See [REPLICATION_GUIDE.md](REPLICATION_GUIDE.md).

The current implementation uses a projected/normalized density-sensitivity reaction field rather than a literal exact gradient flow in the level-set variable; this distinction matters when interpreting the governing equations.

## License and citation

A software license has not been selected; publication of source code does **not** by itself grant permission for unrestricted copying or modification. Confirm licensing with the contributors before adding a license. Cite the finalized manuscript when bibliographic details become available.
