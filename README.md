# Occupational Technology Skill Shares (OTSS), Germany 2012–2023

This repository provides the data underlying the paper **"AI-Powered Skill Classification: Mapping Technology Intensity in the German Labor Market"** by Genz, Gregory, and Lehmer (2026), published open access in **Fiscal Studies**.

📄 **Paper:** https://onlinelibrary.wiley.com/doi/10.1111/1475-5890.70020

The dataset contains occupation-level measures of technology intensity for the German labor market, distinguishing between **manual**, **digital**, and **frontier** technologies. These measures are referred to as **Occupational Technology Skill Shares (OTSS)**.


## Explore the data interactively

An interactive dashboard for exploring OTSS by occupation, technology type, and time is available here:

👉 **Dashboard:** https://otss-data.github.io/otss-dashboard/

The dashboard allows users to:
- compare OTSS across occupations and years (2012 vs. 2023)
- switch between employment-weighted and unweighted views
- analyze the distribution of manual, digital, and frontier technologies
- explore relationships with occupational employment growth
- download occupation-level data or export results

**Use the dashboard for interactive exploration and the repository for data access, documentation, and replication.**


## Data description

This repository contains two datasets:

**OTSS_2012_2023_occ3digit.dta** — OTSS at the **3-digit** occupational level (140 observations).

**OTSS_2012_2023_occ5digit.dta** — OTSS at the **5-digit** occupational level (1,297 observations).

Both files report OTSS values constructed from expert-based occupational skill data (BERUFENET) combined with an AI-powered skill classification pipeline. Each observation corresponds to a German occupation (KldB 2010). Technology skill shares are computed separately for **2012** and **2023**.

The OTSS measure captures the **share of skills within an occupation** that are classified as:

- **Manual technologies** (non-IT-supported or manually controlled)
- **Digital technologies** (IT-supported or indirectly controlled)
- **Frontier technologies** (IT-integrated technologies or self-controlled)

Skill classification is based on a supervised machine-learning model that combines:

- standardized, GenAI-generated skill descriptions
- structured indicators of technological content
- metadata from the BERUFENET skill taxonomy

The resulting OTSS values reflect **observed skill requirements** in occupations rather than forward-looking exposure or automation risk.


## Coverage

- **Geographic scope:** Germany
- **Time coverage:** 2012 and 2023
- **Occupational classification:** German Classification of Occupations (KldB 2010)
- **Skill source:** BERUFENET expert database (Federal Employment Agency)


## Variable description

### Occupational identifiers

- **`kldb2010_3`** *(3-digit file only)*  
  3-digit code of the German Classification of Occupations (KldB 2010).

- **`kldb2010_5`** *(5-digit file only)*  
  5-digit code of the German Classification of Occupations (KldB 2010).

- **`kldb2010_title_en`**  
  English occupation title corresponding to the KldB 2010 code.

### Employment

- **`headcount_2012`**  
  Number of employed workers in the occupation in 2012.

- **`headcount_2023`**  
  Number of employed workers in the occupation in 2023.

Employment counts are derived from German administrative employment records (IAB Employment History) and refer to **regular employment**, defined as individuals aged **16–65** in **socially insured employment** (Personengruppe 101: sozialversicherungspflichtig Beschäftigte ohne besondere Merkmale).  
For further details on sample construction and exclusions, see the accompanying paper.

### Occupational Technology Skill Shares (OTSS)

All OTSS variables are expressed as shares and sum to one within each occupation-year (up to rounding).

**2012**
- **`manual_OTSS_2012`**  
  Share of skills related to manual technologies.

- **`digital_OTSS_2012`**  
  Share of skills related to digital technologies.

- **`frontier_OTSS_2012`**  
  Share of skills related to frontier technologies.

**2023**
- **`manual_OTSS_2023`**  
  Share of skills related to manual technologies.

- **`digital_OTSS_2023`**  
  Share of skills related to digital technologies.

- **`frontier_OTSS_2023`**  
  Share of skills related to frontier technologies.

### Missing value classification *(5-digit file only)*

- **`missings`**  
  Categorical variable classifying the reason for missing OTSS values. See the [Missing Values](#missing-values-in-the-5-digit-file) section below for details.


## Missing values in the 5-digit file

The 3-digit file contains complete OTSS information for all 140 occupations. At the more granular 5-digit level, a subset of the 1,297 occupations contains missing values in `manual_OTSS_2012`, `digital_OTSS_2012`, `frontier_OTSS_2012`, `manual_OTSS_2023`, `digital_OTSS_2023`, and `frontier_OTSS_2023`. This section explains how missing values are identified, categorized, and what institutional factors drive them.

### Summary

| Category | Count | Share |
|---|---|---|
| Complete information (2012 & 2023) | 1,179 | 90.36% |
| Missing in both years | 68 | 5.24% |
| Missing in 2012 only | 45 | 3.47% |
| Missing in 2023 only | 5 | 0.39% |
| Small headcount in both years | 4 | 0.31% |
| Small headcount in 2012 | 2 | 0.15% |
| Missing in 2012 and small headcount in 2023 | 1 | 0.08% |
| **Total** | **1,297** | **100%** |

### Reasons for missing values

Missings arise from institutional features of the KldB 2010 classification system and changes over time, as well as the information contained in BERUFENET. We distinguish three main mechanisms.

#### (1) Invalid status

Some occupations are not valid endpoints in BERUFENET and therefore do not receive skill descriptions by definition. Valid endpoints are marked with status `E` in `alleBerufe.txt`, available at [arbeitsagentur.de](https://www.arbeitsagentur.de/institutionen/dkz-downloadportal).

Reasons why occupations are not valid endpoints include:
- Occupation codes used only for administrative reporting (e.g. employer notifications) but not described in BERUFENET
- Inactive occupation codes
- Old occupation codes about to be archived

> **Impact:** OTSS missing in **both years** for **68 occupations**.

#### (2) Time variation in occupational classification

**(a) Occupations without BERUFENET description in 2012:**
- Occupation codes used only for administrative reporting but not described in BERUFENET
- Occupation codes that did not yet exist in 2012 and were only added by 2023

> **Impact:** OTSS missing in **2012** for **45 occupations**.

**(b) Occupations without BERUFENET description in 2023:**
- Occupation codes used only for administrative reporting but not described in BERUFENET
- Occupation codes deleted by 2023 because they are old or inactive

> **Impact:** OTSS missing in **2023** for **5 occupations**.

#### (3) Small employment numbers

Due to the statistical confidentiality rules of the Federal Employment Agency, all cells with fewer than 3 employees in a given year have been anonymized.

> **Impact:**
> - Both years: **4 occupations**
> - 2012 only: **2 occupations**
> - 2023 only: **1 occupation** *(note: this occupation also had no BERUFENET description in 2012)*

### Classification of missing values

Each observation in the 5-digit file is assigned to one of the following categories in the variable `missings`:

| Value | Description |
|---|---|
| `complete_information` | Occupation with OTSS in both 2012 and 2023 |
| `invalid_status_both` | Occupation without OTSS in 2012 and 2023 due to invalid status |
| `no_description_2012` | Occupation without OTSS in 2012 due to missing BERUFENET description |
| `no_description_2023` | Occupation without OTSS in 2023 due to missing BERUFENET description |
| `headcount_small_both` | Anonymized due to small employment numbers in 2012 and 2023 |
| `headcount_small_2012` | Anonymized due to small employment numbers in 2012 |
| `no_description_2012_headcount_2023` | No OTSS in 2012; anonymized due to small employment numbers in 2023 |


## Intended use

The data are intended for:

- research on technological change, AI, and digitalization in labor markets
- policy analysis related to skills, training, and workforce transformation
- replication and extension of the results in the accompanying paper

Users can link OTSS to employment, wage, or establishment data at the occupational level to study the labor-market implications of digital and frontier technologies.


## Citation

If you use this data, please cite:

> Genz, S., Gregory, T., & Lehmer, F. (2026). *AI-Powered Skill Classification: Mapping Technology Intensity in the German Labor Market*. Fiscal Studies. https://doi.org/10.1111/1475-5890.70020


## License

This dataset is licensed under the [Creative Commons Attribution 4.0 International License (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/). See `LICENCE.txt` for the full license text.
