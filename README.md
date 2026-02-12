# Occupational Technology Skill Shares (OTSS), Germany 2012–2023

This repository provides the data underlying the paper **“AI-Powered Skill Classification: Mapping Technology Intensity in the German Labor Market”** by Genz, Gregory, and Lehmer (2026), **Fiscal Studies (forthcoming)**.

The dataset contains occupation-level measures of technology intensity for the German labor market, distinguishing between **manual**, **digital**, and **frontier** technologies. These measures are referred to as **Occupational Technology Skill Shares (OTSS)**.

## Data description

The main file

**OTSS_2012_2023_occ3digit.dta**

reports OTSS values constructed from expert-based occupational skill data (BERUFENET) combined with an AI-powered skill classification pipeline.

Each observation corresponds to a German occupation (KldB 2010, 3-digit level).  
The dataset contains **140 occupational observations**, with technology skill shares computed separately for **2012** and **2023**.

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
- **`kldb2010_3`**  
  3-digit code of the German Classification of Occupations (KldB 2010).

- **`kldb2010_title_en`**  
  English occupation title corresponding to the 3-digit KldB 2010 code.

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

## Intended use

The data are intended for:

- research on technological change, AI, and digitalization in labor markets
- policy analysis related to skills, training, and workforce transformation
- replication and extension of the results in the accompanying paper

Users can link OTSS to employment, wage, or establishment data at the occupational level to study the labor-market implications of digital and frontier technologies.

## Citation

If you use this data, please cite:

> Genz, S., Gregory, T., & Lehmer, F. (2026). *AI-Powered Skill Classification: Mapping Technology Intensity in the German Labor Market*. Fiscal Studies, forthcoming.
