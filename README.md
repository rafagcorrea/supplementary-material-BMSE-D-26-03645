# Supplementary material — HydroBEM

Supplementary material for the manuscript **"Development and validation of HydroBEM: A Blade Element Momentum framework with local Reynolds number for hydrokinetic turbines"** (Rafaela Gomide Corrêa and Francisco José de Souza, Federal University of Uberlândia), submitted to the *Journal of the Brazilian Society of Mechanical Sciences and Engineering* (manuscript ID BMSE-D-26-03645).

DOI: https://doi.org/[ZENODO-DOI]  <!-- fill in after the Zenodo release -->

This repository contains the **input data** of the two validation cases of the manuscript: the two-dimensional lift and drag polars, the blade chord and twist distributions, the hydrofoil geometry, the two-dimensional CFD data and the experimental data used for comparison. Together with the algorithm and numerical settings described in Section 2.2 of the manuscript, these data are what is needed to set up the calculations of the paper.

**The HydroBEM source code is not part of this repository.** It is registered with the Brazilian National Institute of Industrial Property (INPI) and is available from the corresponding author upon reasonable request.

## Contents

```
Case1/                                     First validation case (Tucker Harvey et al., 2023)
  chordandtwist.txt                        Blade chord and twist distribution (176 sections)
  Thickened hydrofoil profile.txt          Hydrofoil coordinates (thickened NACA 63-415)
  Re_90k.dat ... Re_700k.dat               Polars, -180 to 180 deg, Re = 90,000 ... 700,000
  Re_288k.dat                              Polar at the representative Reynolds number (see below)
  2D Hydrofoil Profile CFD Data/Tu*.txt    2D CFD polars at Re = 288,888 for several inflow turbulence levels
  Experimental/
    original/                              Experimental data as provided by the authors of the benchmark
    interped/                              Experimental data interpolated to the tip speed ratios simulated in the paper
Case2/                                     Second validation case (Stelzenmuller, 2013)
  chordandtwist.txt                        Blade chord and twist distribution (30 sections)
  Re_50k.dat ... Re_700k.dat               Polars, -180 to 180 deg, Re = 50,000 ... 700,000
  Re_75k.dat                               Polar at the representative Reynolds number (see below)
```

## File formats

All angles are in degrees. Lengths are in metres.

| File | Columns | Notes |
|---|---|---|
| `Case1/chordandtwist.txt` | r/R, twist angle [deg], chord [m] | Tab-separated, `#` lines are comments. r/R = 0.125 (hub) to 1.0 (tip). |
| `Case2/chordandtwist.txt` | r/R, twist angle [deg], chord [m] | Same layout. r/R = 0.14 to 1.0. |
| `Case1/Re_*.dat` (except 288k) | alpha [deg], Cl, Cd | One header line. |
| `Case1/Re_288k.dat`, `Case2/Re_*.dat` | alpha [deg], Cl, Cd, Cm | QBlade/AeroDyn-style table, no column header (the 288k file has a 2-line header). |
| `2D Hydrofoil Profile CFD Data/Tu*.txt` | AoA [deg], Cl, Cd | First line gives Re and the inflow turbulence intensity (Tu); 0 to 15 deg. |
| `Experimental/*/Low_Turbulence_Cases/integrated.txt` and `Elevated_Turbulence_Cases/integrated.txt` | case no., TSR, Err(TSR), C_T, Err(C_T), C_P, Err(C_P) | Rotor-integrated thrust and power coefficients with uncertainties. |
| `Experimental/*/*/BM_*R.txt` | case no., TSR, Err(TSR), C_BM(fw), Err, C_BM(ew), Err | Blade bending-moment coefficients (flapwise, fw, and edgewise, ew) at the radial station given in the file name. |
| `Thickened hydrofoil profile.txt` | x, y | Chord-normalised coordinates, trailing-edge thickness 0.00625 chord. |

The polar tables are the final tables supplied to the solver, already extrapolated to −180°…180° (Montgomerie method in QBlade). The XFOIL range was −5° to 15° in both cases.

## Data provenance

**Case 1 — Tucker Harvey et al. (2023)**: three-bladed, 1.6 m diameter rotor with a thickened NACA 63-415 hydrofoil, tested under low and elevated inflow turbulence. Experimental data and 2D CFD polars (SST k-ω) come from the benchmark. Polars `Re_90k.dat` ... `Re_700k.dat`: XFOIL with transition parameter N = 9, extrapolated in QBlade CE v2.0.4. 

**Case 2 — Stelzenmuller (2013)**: two-bladed 1:45 scale model of the DOE Reference Model 1 (rotor diameter 0.444 m, hub diameter 0.062 m, NACA 4415 hydrofoil), tested in a recirculating water channel. Polars: XFOIL with N = 9, extrapolated in QBlade CE v2.0.4..

**Representative Reynolds number**: `Re_288k.dat` (case 1) and `Re_75k.dat` (case 2) are the polars used with the representative Reynolds number approach. The local Reynolds number approach interpolates between the polars listed above, as described in Section 2.2 of the manuscript.

## How the data are used

For each blade element the solver reads the local chord and twist (linear interpolation along r/R), computes the local Reynolds number, interpolates linearly between the two polars that bracket it at each tabulated angle of attack, and then interpolates linearly in angle of attack. The equations, the numerical settings (tolerances, under-relaxation, iteration limit, root-finding intervals) and the flowcharts are given in the manuscript (Section 2.2, Figs. 1–2).

## References

- Tucker Harvey, S., Chen, X., Rowe, D., Mcnaughton, J., Vogel, C., Bhavsar, K., Allsop, T., Gilbert, J., Mullings, H., Stallard, T., Young, A., Benson, I., Willden, R.: Tidal turbine benchmarking project: Stage I – steady flow experiments. *Proceedings of the European Wave and Tidal Energy Conference* 15 (2023). https://doi.org/10.36688/ewtec-2023-553
- Stelzenmuller, N.: Array optimization for marine hydrokinetic turbines. Master's thesis, University of Washington, Seattle, USA (2013).

## License

 license: CC-BY-4.0 The experimental data and 2D CFD data of case 1 originate from Tucker Harvey et al. (2023) and the case 2 data from Stelzenmuller (2013); they are redistributed here for reproducibility of the manuscript, and the original sources must be cited when they are reused 

## How to cite

Please cite the manuscript and this dataset (see `CITATION.cff`).

## Contact

Rafaela Gomide Corrêa — rafaelagomide@ufu.br
Francisco José de Souza (corresponding author) — francisco.souza@ufu.br
Fluid Mechanics Laboratory, Federal University of Uberlândia, Brazil.
