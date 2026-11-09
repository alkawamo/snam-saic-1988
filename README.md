# Computational Social Science & Network Analysis of the 1988 Brazilian Constituent Assembly (SAIC Dataset)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/alkawamo/snam-saic-1988/blob/main/SAIC_1988_OpenScience_Analysis.ipynb)
[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)

This repository provides the open-science data curation pipeline, reproducible source code, and high-resolution figures accompanying the study:

> **Uncovering Grassroots Constitutional Demands through Word Co-occurrence Networks and Multi-Dimensional Sociodemographic Stratification: Evidence from 72,719 Citizen Letters to the 1988 Brazilian Constituent Assembly**

---

## 1. Overview & Historical Context

Between 1986 and 1987, during Brazil's transition from a 21-year military dictatorship to democracy, the Federal Senate's Data Processing Center (**Prodasen**) conducted a pioneering institutional experiment: the **Citizen Information Support System (SAIC – *Sistema de Apoio Informático ao Cidadão*)**. Before the widespread adoption of the commercial internet, **72,719 postal letters and forms** sent by citizens across all 26 Brazilian states and territories were transcribed into a mainframe database and classified into 24 official thematic categories.

In this study, we contrast that historical **top-down** bureaucratic taxonomy with an unsupervised **bottom-up** semantic network approach, cross-referencing emergent discourse communities with the rich sociodemographic, geographic, and political metadata recorded in each citizen's submission.

---

## 2. Repository Structure

```text
snam-saic-1988/
├── SAIC.csv                               # Curated SAIC dataset (72,719 rows x 21 columns)
├── SAIC_1988_OpenScience_Analysis.ipynb   # Reproducible Google Colab Notebook (English)
├── README.md                              # Project documentation and replication guide
└── figures/                               # High-resolution (300 DPI) figures in English
    ├── fig1_cooccurrence_network_en.png
    ├── fig2_topdown_vs_bottomup_heatmap_en.png
    ├── fig3_demographic_profiles_en.png
    ├── fig4_regional_distribution_en.png
    └── fig5_bipartite_parliamentarians_en.png
```

---

## 3. Summary of Methodology & Key Findings

1. **Historical Data Curation & Noise Auditing:**
   - Out of 72,719 historical records, **72,394 ($99.55\%$)** contain valid natural-language proposals (`TEXTO SUGESTÃO`), alongside 2 empty records and **323 spreadsheet formula corruption artifacts (`#NOME?`)** introduced when historical transcriptions starting with `-` or `=` were exported to CSV.
   - Deduplicating repeated campaigns yields **70,151 unique valid texts** used for network construction, while all **71,428 letters ($98.2\%$)** containing at least one core network term are retained for sociodemographic, geographic, and political stratification.

2. **PPMI Co-occurrence Network & Louvain Community Detection:**
   - Evaluating document frequency thresholds (`min_df` $\in \{1\%, 2\%, 3\%\}$) and Positive Pointwise Mutual Information (PPMI) percentile cutoffs ($\{85, 90, 95\}$) demonstrates that `min_df = 2.0%` combined with the **95th percentile PPMI cutoff ($\theta_{95} = 1.25$)** preserves full connectivity ($1$ connected component, $|V| = 322$ nodes, $|E| = 1,823$ edges, density $3.53\%$) while maximizing modularity (**$Q = 0.6363$**, 8 thematic communities):
     - **C1:** Economic Development & Agriculture (31 nodes)
     - **C2:** Public Administration & State Organization (33 nodes)
     - **C3:** Political & Electoral Structure (50 nodes)
     - **C4:** Educational Policy (28 nodes)
     - **C5:** Penal System & Public Security (43 nodes)
     - **C6:** Social Security & Healthcare (40 nodes)
     - **C7:** Professional Autonomy & Labor Regulation (30 nodes)
     - **C8:** Popular Appeals & Protests (67 nodes)

3. **Top-Down vs. Bottom-Up Alignment:**
   - Cross-tabulating Prodasen's 24 official catalog themes (`CATÁLOGO`) against the 8 emergent communities confirms strong thematic alignment in specialized domains (e.g., *Educational Policy* $\to 34.8\%$ in C4; *Agricultural Policy* $\to 26.6\%$ in C1; *Social Security Policy* $\to 26.1\%$ in C6; *Constituent Information Request* $\to 33.6\%$ in C8), while disambiguating broad bureaucratic catch-all categories such as *Social Organization* ($n=15,187$).

4. **Sociodemographic Stratification ($\chi^2$ and Cramér's $V$):**
   - **Gender ($\chi^2 = 3,159.7, p < 10^{-100}, V = 0.216$):** Female citizens ($n=23,047$) prioritize *C4: Educational Policy* ($21.3\%$ vs. $12.2\%$ for males) and *C6: Social Security & Healthcare* ($14.7\%$ vs. $13.3\%$), whereas male citizens ($n=44,500$) concentrate more heavily on *C2: Public Administration* ($14.0\%$) and *C3: Political & Electoral Structure* ($12.7\%$).
   - **Urban vs. Rural Divide ($\chi^2 = 1,454.4, p < 10^{-100}, V = 0.149$):** Rural residents ($n=7,394$) focus on *C1: Economic Dev. & Agriculture* ($14.0\%$ vs. $10.0\%$ urban) and *C7: Professional Autonomy/Labor* ($18.1\%$), whereas urban residents ($n=57,935$) emphasize *C5: Penal System & Public Security* ($13.3\%$ vs. $9.9\%$ rural) and *C6: Social Security & Healthcare* ($14.0\%$).
   - **Education & Income Gradients ($\chi^2 = 2,797.8$ and $\chi^2 = 5,650.6, p < 10^{-100}$):** Institutional design themes (*C2: Public Administration* and *C3: Political Structure*) rise monotonically from low-income ($\le 1$ MW: $10.7\%$ and $8.2\%$) and illiterate citizens ($10.3\%$ and $9.4\%$) to the highest income ($>20$ MW: $17.6\%$ and $16.5\%$) and postgraduate strata ($15.8\%$ and $13.9\%$). Conversely, *C8: Popular Appeals & Protests* ($15.1\%$ among illiterate vs. $8.4\%$ among postgraduates) and *C1: Agriculture/Economy* ($14.5\%$ vs. $8.3\%$) are heavily concentrated among lower-income and less-educated citizens.

5. **Macro-Regional Geography & Citizen–Parliamentarian Bipartite Network:**
   - Significant regional divergence ($\chi^2 = 5,009.6, p < 10^{-100}, V = 0.133$) and clear thematic specialization among the top targeted Constituent Assembly members (`DESTINATÁRIO`) reveal how both spontaneous civic mobilization and organized corporatist lobbying operated during the drafting of the 1988 Constitution.

---

## 4. Reproducing the Analyses

You can run the complete pipeline directly in **Google Colab** using the badge at the top of this README, or locally via Python 3.10+:

```bash
pip install pandas numpy scipy scikit-learn networkx matplotlib spacy
python -m spacy download pt_core_news_md
jupyter notebook SAIC_1988_OpenScience_Analysis.ipynb
```

## 5. License

The code and documentation in this repository are released under the **Creative Commons Attribution 4.0 International (CC BY 4.0)** and **MIT** licenses for Open Science reproducibility.
