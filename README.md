# Bader Charge 3D Analyzer

A browser-based 3D analyzer for `POSCAR` and `ACF.dat` files that visualizes Bader charge transfer with an interactive Three.js view.

This single-page tool is designed for quick inspection of VASP Bader charge analysis results. It lets you load atomic coordinates and Bader charges, generate a color-mapped 3D structure, box-select atoms, and summarize local charge transfer directly in the browser.

## Online Demo

After GitHub Pages is enabled, the site can be visited here:

```text
https://sanguangnian6699.github.io/bader-charge-3d-analyzer/
```

## Features

- Upload `POSCAR` and `ACF.dat`
- Parse VASP 5 style element and atom-count information from `POSCAR`
- Parse Bader charge data from common `ACF.dat` output
- Auto-fill default VASP PBE valence electron counts for many elements
- Allow manual correction of valence values for special POTCAR variants
- Compute charge transfer as:

```text
deltaQ = valence electrons - Bader charge
```

- Render atoms in 3D with a charge-based heatmap
- Use blue/red color mapping to distinguish positive and negative charge transfer
- Adjust:
  - atom display radius
  - background color
  - transparent background export
  - light direction and intensity
  - ambient light intensity
- Switch camera view along X / Y / Z
- Support manual drag rotation and auto rotation
- Constrain rotation around X / Y / Z axes
- Use `Shift + drag` to box-select atoms in the viewport
- Summarize selected atom count and total charge transfer
- Export high-resolution PNG images

## Usage

### Option 1: Open directly

Open [`index.html`](./index.html) in a modern browser such as Chrome, Edge, or Firefox.

### Option 2: Run a local static server

```bash
python -m http.server 8000
```

Then visit:

```text
http://localhost:8000
```

### Option 3: Use GitHub Pages

1. Open the repository on GitHub
2. Go to `Settings`
3. Open `Pages`
4. Under `Build and deployment`, choose `Deploy from a branch`
5. Select branch `main`
6. Select folder `/ (root)`
7. Save and wait for deployment

## Input Files

Required files:

```text
POSCAR
ACF.dat
```

Notes:

- `POSCAR` should be VASP 5 style and include an element-symbol line
- `ACF.dat` should be a common Bader analysis output with atom coordinates and charge values
- The number of atoms in `POSCAR` must match the number of parsed entries in `ACF.dat`

## Charge Interpretation

The tool uses:

```text
deltaQ = valence - Bader charge
```

In this convention:

- positive `deltaQ` means the atom has lost electron density
- negative `deltaQ` means the atom has gained electron density

Please interpret results together with the actual Bader workflow and the POTCAR used in your calculation.

## Tech Stack

- HTML
- JavaScript
- Three.js
- OrbitControls

This project is a pure frontend application and does not require a backend server.

## Typical Use Cases

- Bader charge result inspection
- local charge-transfer visualization
- materials science teaching demos
- catalyst active-site comparison
- paper figure drafting
- quick sanity checks for charge redistribution

## Known Limitations

This tool is intended for lightweight visualization and interactive inspection, not as a replacement for a full analysis workflow.

1. `POSCAR` parsing expects a VASP 5 style file with an explicit element-symbol line.
2. `ACF.dat` parsing assumes a common Bader output layout and may not support every variant.
3. Default valence electron values are approximate VASP PBE defaults and should be checked for `_sv`, `_pv`, or other special POTCARs.
4. Charge interpretation depends on the consistency between your `POSCAR`, `ACF.dat`, and chosen valence reference.
5. The 3D view is atom-based and does not display bonding, charge-density isosurfaces, or volumetric data.
6. Very large structures may reduce browser performance.

## Future Ideas

- support for more Bader output variants
- export of selected atom indices and summed charge
- configurable color maps
- element labels and hover tooltips
- optional bond rendering
- snapshot of current analysis settings

## License

This project is released under the [MIT License](./LICENSE).

## Author

Created by [sanguangnian6699](https://github.com/sanguangnian6699)

If this project helps you, feel free to star the repository, fork it, or open an issue.
