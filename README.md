# AI-assisted HEp-2 IIF interpretation and autoantibody analysis

This repository contains the analysis code used to reproduce the manuscript analyses of AI-assisted HEp-2 indirect immunofluorescence (IIF) interpretation and disease-specific autoantibody results.

The public notebook starts from the **final merged analytic dataset**. Raw ANA-IIF and line immunoassay (LIA) exports, patient-level identifiers, data cleaning, deduplication, and record linkage are intentionally outside the scope of this repository. No patient-level dataset is distributed with the repository.

## Analysis workflow

The notebook follows the order of the manuscript Results:

1. **HEp-2 IIF pattern and autoantibody characteristics** — descriptive distributions used for Table 1.
2. **Impact of human review on HEp-2 IIF interpretations** — AI-to-human pattern reassignment and titer changes (Figure 2).
3. **Associations between HEp-2 IIF interpretations and disease-specific autoantibodies** — pattern–autoantibody associations and reclassification analyses (Figure 3 and Supplementary Table S2).
4. **Diagnostic performance of AI probabilities for autoantibody identification** — probability distributions, median/IQR comparisons, diagnostic performance, and ROC analyses (Figure 4, Table 2, and Supplementary Table S3).
5. **ROC analysis for anti-DFS70 identification** — dense fine speckled (AC-2) AI probability versus anti-DFS70 positivity (Figure 5A).

## Analysis conventions

Autoantibody positivity is defined as **LIA band intensity ≥26 (≥2+)**. AI pattern positivity is defined using the manufacturer-defined **probability threshold ≥50%**. For binary AI-pattern analyses, unavailable/below-reporting-threshold probability values are treated as pattern not suggested. Continuous probability analyses use cases with an available probability score.

Autoantibody-positive case counts are calculated at the **case level**: a case with multiple positive autoantibodies is counted once when reporting the number of autoantibody-positive cases. Counts of individual autoantibodies are antibody-level and therefore are not mutually exclusive.

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
| `NUC__AC_1_M` | Human-reviewed Homogeneous result; positive values indicate the reviewed pattern/titer as encoded in the merged dataset |
| `NUC__AC_3_M` | Human-reviewed Centromere result; positive values indicate the reviewed pattern/titer as encoded in the merged dataset |
| `NUC__AC_2_4_5_29_M` | Human-reviewed Nuclear speckled result; positive values indicate the reviewed pattern/titer as encoded in the merged dataset |
| `NUC__AC_6_7_M` | Human-reviewed Nuclear dot result; positive values indicate the reviewed pattern/titer as encoded in the merged dataset |
| `NUC__AC_8_9_10_M` | Human-reviewed Nucleolar result; positive values indicate the reviewed pattern/titer as encoded in the merged dataset |
| `NUC__AC_11_12_M` | Human-reviewed Nuclear envelope result; positive values indicate the reviewed pattern/titer as encoded in the merged dataset |
| `NUC__AC_13_14_M` | Human-reviewed Nuclear pleomorphic result; positive values indicate the reviewed pattern/titer as encoded in the merged dataset |
| `CYT_M` | Human-reviewed Cytoplasmic result; positive values indicate the reviewed pattern/titer as encoded in the merged dataset |
| `MIT_M` | Human-reviewed Mitotic result; positive values indicate the reviewed pattern/titer as encoded in the merged dataset |
| `NEG_M` | Human-reviewed Negative result; positive values indicate the reviewed pattern/titer as encoded in the merged dataset |
| `dsDNA` | Line immunoassay band/intensity value for anti-dsDNA; ≥26 is treated as ≥2+ positive |
| `HI` | Line immunoassay band/intensity value for anti-Histone; ≥26 is treated as ≥2+ positive |
| `NUC` | Line immunoassay band/intensity value for anti-Nucleosome; ≥26 is treated as ≥2+ positive |
| `DFS70` | Line immunoassay band/intensity value for anti-DFS70/LEDGF; ≥26 is treated as ≥2+ positive |
| `CB` | Line immunoassay band/intensity value for anti-CENP-B; ≥26 is treated as ≥2+ positive |
| `CA` | Line immunoassay band/intensity value for anti-CENP-A; ≥26 is treated as ≥2+ positive |
| `SSA` | Line immunoassay band/intensity value for anti-TROVE2/Ro60; ≥26 is treated as ≥2+ positive |
| `Ro-52` | Line immunoassay band/intensity value for anti-TRIM21/Ro52; ≥26 is treated as ≥2+ positive |
| `SSB` | Line immunoassay band/intensity value for anti-SSB/La; ≥26 is treated as ≥2+ positive |
| `Ku` | Line immunoassay band/intensity value for anti-Ku; ≥26 is treated as ≥2+ positive |
| `Mi-2b` | Line immunoassay band/intensity value for anti-Mi-2β; ≥26 is treated as ≥2+ positive |
| `Mi-2a` | Line immunoassay band/intensity value for anti-Mi-2α; ≥26 is treated as ≥2+ positive |
| `Sm` | Line immunoassay band/intensity value for anti-Sm; ≥26 is treated as ≥2+ positive |
| `RNP/Sm` | Line immunoassay band/intensity value for anti-RNP/Sm; ≥26 is treated as ≥2+ positive |
| `RP155` | Line immunoassay band/intensity value for anti-RP155; ≥26 is treated as ≥2+ positive |
| `RP11` | Line immunoassay band/intensity value for anti-RP11; ≥26 is treated as ≥2+ positive |
| `Sp100` | Line immunoassay band/intensity value for anti-Sp100; ≥26 is treated as ≥2+ positive |
| `PML` | Line immunoassay band/intensity value for anti-PML; ≥26 is treated as ≥2+ positive |
| `PM75` | Line immunoassay band/intensity value for anti-PM/Scl-75; ≥26 is treated as ≥2+ positive |
| `PM100` | Line immunoassay band/intensity value for anti-PM/Scl-100; ≥26 is treated as ≥2+ positive |
| `Scl-70` | Line immunoassay band/intensity value for anti-Scl-70; ≥26 is treated as ≥2+ positive |
| `gp210` | Line immunoassay band/intensity value for anti-gp210; ≥26 is treated as ≥2+ positive |
| `PCNA` | Line immunoassay band/intensity value for anti-PCNA; ≥26 is treated as ≥2+ positive |

### Notes on the variable schema

The AI probability variables (`*_P_AI`) are expressed on a 0–100 probability scale. AI titer variables (`*_T_AI`) are required only for the directly comparable nuclear-pattern pairs used in Figure 2B.

Human-reviewed nuclear-pattern columns retain the reviewed result/titer encoding used in the final merged analytic dataset; values greater than zero are interpreted as presence of that pattern. `CYT_M` and `MIT_M` represent human-reviewed cytoplasmic and mitotic interpretations, respectively, and `NEG_M` represents the human-reviewed negative interpretation.

The abbreviated LIA column names above are retained because they are the variable names in the analytic dataset. Their corresponding reported autoantibodies are provided in the table.

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

Set `DATA_PATH` in the setup section if the merged dataset is stored elsewhere, then restart the kernel and run the notebook from top to bottom. The notebook is designed to generate the manuscript analysis objects and figures interactively; it does not require figure or Excel export code.

## Data availability and privacy

The analytic dataset is not included in this public repository because it is derived from clinical laboratory records. The variable schema above is provided to document the structure required to reproduce the analysis code without distributing patient-level data.

The repository code should therefore be interpreted as a reproducible description of the statistical analysis workflow rather than as a public release of the study dataset.

## Repository scope

This repository covers analyses beginning with the final merged dataset. It does **not** reproduce upstream laboratory-data extraction, ANA-IIF/LIA cleaning, deduplication, linkage, or construction of the final analytic cohort.
