# Mesh-Based Crater Rim Detection & Depth Estimation on Ryugu — Data Package

This repository contains the input meshes and output products used for crater rim detection and depth estimation on asteroid **(162173) Ryugu**.

## Contents

### 1) JSON files (4)

#### `apbt_v2_results.json`
Per-crater **APBT v2** outputs.  
Each crater (e.g., `crater_1.vtk`) maps to a list of runs (one run per seed set). Typical fields include:
- `seed_points` (vertex ids)
- key parameters (`FACTOR_RADIUS`, `ANGLE_SIGMA`, `POINTS_CIRCLE`, `RAY_LENGTH`, etc.)
- diameter outputs (`Diameter_max`, sometimes `Diameter_ew`, `Diameter_ns`)
- depth outputs (`Depth_med`, `Depth_p40`, `Depth_p60`, `Err_minus`, `Err_plus`)
- reference levels (`Rim_level`, `Floor_level`)
- internal diagnostics (e.g., `Frac_neighbors`)

#### `circle_results.json`
Per-crater **CIRCLE** outputs, stored the same way (multiple runs per crater, one per seed set). Typical fields include:
- `seed_points`, `POINTS_CIRCLE`, `RAY_LENGTH`, `inverse`
- `Diameter_max`
- `Depth_med`, `Depth_p40`, `Depth_p60`, `Err_minus`, `Err_plus`
- `Rim_level`, `Floor_level`
- `Frac_neighbors`

#### `crater_seeds.json`
Lists the **seed sets** used per crater.  
Structure: each crater file maps to a list of seed-point arrays, e.g.
- `"crater_1.vtk": [[...],[...],[...]]`

#### `craters_manipulation.json`
Per-crater preprocessing configuration used to compute the rim signal (curvature) and stabilize the mesh fields. Typical fields include:
- `Mesh_inverse`
- Taubin smoothing settings (`type`, `n_iter`, `pass_band`)
- pooling settings (`number_rings`, `pool_method`)
- chosen curvature signal (`abs_k1` or `abs_k2`)

---

### 2) Crater ROI meshes (VTK)
Folder: **`77_craters/`**

Contains the **77 crater regions of interest** as **VTK** files (triangular mesh patches), one file per crater:
- `crater_1.vtk` … `crater_77.vtk`

These ROI meshes are the direct inputs used for rim detection and depth estimation.

---

### 3) Ryugu global mesh with crater scalar labels (ZIP)
File: **`ryugu_with_77_craters.vtk.zip

This archive contains a **Ryugu global shape model mesh** where the **77 craters are encoded as scalar data** on the mesh (e.g., a scalar array such as `crater_id` or `crater_index`).  
This enables visualization of crater locations directly on the full-body model (e.g., in ParaView or PyVista).
