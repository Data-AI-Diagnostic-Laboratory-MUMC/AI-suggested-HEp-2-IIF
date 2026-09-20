# Artificial intelligence-suggested HEp-2 IIF interpretation with human review: implications for autoantibody prediction and laboratory test utilization

This repository contains the analysis code used to reproduce the analyses reported in this study.

## Input data

The notebook expects the final merged analytic dataset at:

```text
../data/merged_data.csv
```

CSV, Excel, and Parquet input are supported by the loading function if `DATA_PATH` is changed accordingly.

The input dataset must contain the variables below. The names are the analysis column names used directly by the notebook.

### Required variables

| Variable | Description |
|---|---|
| `AC_1_P_AI` | AI-suggested Homogeneous probability (%) |
| `AC_2_P_AI` | AI-suggested Dense fine speckled probability (%) |
| `AC_3_P_AI` | AI-suggested Centromere probability (%) |
| `SPECKLED_P_AI` | AI-suggested Nuclear speckled probability (%) |
| `DOTS_P_AI` | AI-suggested Nuclear dot probability (%) |
| `NUCLEOLAERE_P_AI` | AI-suggested Nucleolar probability (%) |
| `CYTO_P_AI` | AI-suggested Cytoplasmic probability (%) |
| `NEG_P_AI` | AI-suggested Negative probability (%) |
| `AC_1_T_AI` | AI-suggested Homogeneous titer |
| `AC_3_T_AI` | AI-suggested Centromere titer |
| `SPECKLED_T_AI` | AI-suggested Nuclear speckled titer |
| `DOTS_T_AI` | AI-suggested Nuclear dot titer |
| `NUCLEOLAERE_T_AI` | AI-suggested Nucleolar titer |
| `NUC__AC_1_M` | Human-reviewed Homogeneous titer |
| `NUC__AC_3_M` | Human-reviewed Centromere titer |
| `NUC__AC_2_4_5_29_M` | Human-reviewed Nuclear speckled titer |
| `NUC__AC_6_7_M` | Human-reviewed Nuclear dot titer |
| `NUC__AC_8_9_10_M` | Human-reviewed Nucleolar titer |
| `NUC__AC_11_12_M` | Human-reviewed Nuclear envelope titer |
| `NUC__AC_13_14_M` | Human-reviewed Nuclear pleomorphic titer |
| `CYT_M` | Human-reviewed Cytoplasmic titer |
| `MIT_M` | Human-reviewed Mitotic titer |
| `NEG_M` | Human-reviewed Negative titer (100) |
| `dsDNA` | LIA band intensity value for anti-dsDNA |
| `HI` | LIA band intensity value for anti-Histone|
| `NUC` | LIA band intensity value for anti-Nucleosome |
| `DFS70` | LIA band intensity value for anti-DFS70 |
| `CB` | LIA band intensity value for anti-CENP-B |
| `CA` | LIA band intensity value for anti-CENP-A |
| `SSA` | LIA band intensity value for anti-TROVE2/Ro60|
| `Ro-52` | LIA band intensity value for anti-TRIM21/Ro52 |
| `SSB` | LIA band intensity value for anti-SSB/La |
| `Ku` | LIA band intensity value for anti-Ku |
| `Mi-2b` | LIA band intensity value for anti-Mi-2β |
| `Mi-2a` | LIA band intensity value for anti-Mi-2α |
| `Sm` | LIA band intensity value for anti-Sm|
| `RNP/Sm` | LIA band intensity value for anti-RNP/Sm |
| `RP155` | LIA band intensity value for anti-RP155 |
| `RP11` | LIA band intensity value for anti-RP11 |
| `Sp100` | LIA band intensity value for anti-Sp100|
| `PML` | LIA band intensity value for anti-PML|
| `PM75` | LIA band intensity value for anti-PM/Scl-75|
| `PM100` | LIA band intensity value for anti-PM/Scl-100 |
| `Scl-70` | LIA band intensity value for anti-Scl-70 |
| `gp210` | LIA band intensity value for anti-gp210 |
| `PCNA` | LIA band intensity value for anti-PCNA|

## Software requirements

The notebook uses Python with:

```text
numpy
pandas
matplotlib
seaborn
scipy
scikit-learn
statsmodels
```

A recent Python 3 environment is recommended.

## Running the analysis

Set `DATA_PATH` in the setup section if the merged dataset is stored elsewhere, then restart the kernel and run the notebook from top to bottom. The notebook is designed to generate the manuscript analysis objects and figures interactively.

## Data availability

The data supporting the findings of this study are available from the corresponding author upon reasonable request. The analysis code is publicly available in this GitHub repository.

## Repository scope

This repository contains the analysis code used to generate the main and supplementary results reported in the study. The analyses begin with the final merged analytic dataset and do not include upstream laboratory-data extraction, ANA-IIF/LIA data cleaning, deduplication, linkage, or construction of the final analytic cohort.
