![Uploading image.png…]()

# Seasonal Agriculture Performance Analysis

A complete, data-driven analytics dashboard project analyzing how agricultural
performance changes across seasons, regions, crops, and farming practices —
built as the Major Project for the **VOIS AICTE Batch 2026-2027** program.

## Overview

This project analyzes 4,000 real farm-season records to understand how
agricultural yield, resource use, environmental conditions, and economic
performance vary across India's three cropping seasons — **Kharif, Rabi, and
Zaid**. It follows a complete analytics workflow: raw data → cleaning →
analysis → KPIs → visualization → dashboard → insights → recommendations,
built entirely with Python, Jupyter, Pandas, NumPy, Matplotlib, Seaborn, and
SciPy. Every number in the notebook and dashboard is calculated directly from
the dataset — nothing is hard-coded or fabricated.

## Problem Statement

Agricultural activity is shaped by seasonal shifts in environmental
conditions, farming practices, resource availability, and market conditions,
so performance can differ considerably from one season to the next. Raw
farm-level data alone does not make these seasonal differences obvious. This
project analyzes the provided agricultural dataset to uncover meaningful
seasonal patterns, trends, relationships, and variations in agricultural
performance.

## Objectives

- Explore and understand the structure and quality of the dataset
- Clean and prepare the data so it is reliable for analysis
- Examine how yield, production, and profitability vary across seasons
- Statistically test whether observed seasonal patterns are real
- Investigate relationships between environmental/resource conditions and
  performance
- Compare performance across regions, crops, and irrigation methods
- Build a KPI-driven analytics dashboard summarizing the strongest findings
- Translate findings into evidence-based recommendations

## Technology Stack

Python 3 · Jupyter Notebook · Pandas · NumPy · Matplotlib · Seaborn · SciPy
— no other libraries or BI tools are used.

## Dataset

**`data/agriculture_dataset.csv`** — 4,000 records, 28 columns:

| Dimension | Columns |
|---|---|
| Identifiers | Farm_ID |
| Geographic | State (8), District (10) |
| Seasonal / Crop | Season (Kharif/Rabi/Zaid), Crop (8), Irrigation_Method (4) |
| Environmental | Rainfall_mm, Avg_Temperature_C, Humidity_pct, Sunlight_Hours_Day, Soil_pH, Soil_Moisture_pct |
| Resources | Nitrogen/Phosphorus/Potassium_kg_ha, Fertilizer_kg_ha, Pesticide_Litre_ha, Seed_Quality_Score, Water_Used_m3 |
| Performance | Farm_Area_Hectares, Yield_Tonnes_Ha, Production_Tonnes, Disease_Pest_Risk_pct, Water_Efficiency_t_per_1000m3 |
| Economic | Market_Price_INR_Tonne, Total_Cost_INR, Revenue_INR, Profit_INR |

**Data quality found:** 48 missing `Rainfall_mm`, 40 missing
`Soil_Moisture_pct`, 32 missing `Yield_Tonnes_Ha`; no duplicate rows or
Farm_IDs. `Yield_Tonnes_Ha` was reconstructed exactly from
`Production_Tonnes / Farm_Area_Hectares` (a relationship that holds for every
complete record); `Rainfall_mm` and `Soil_Moisture_pct` were imputed with
each row's season median, since both vary strongly by season. Extreme-looking
Yield/Production values were investigated and found to be genuine — driven
entirely by Sugarcane's realistically much higher yield per hectare — and so
were kept rather than removed. See `notebooks/…ipynb` §6–7 for the full
walkthrough.

## Analysis Performed

- **Seasonal analysis** — yield, profit, and loss-rate by season, with a
  crop-normalized Yield Index (Kharif = 100) to show the pattern is universal
- **Environmental analysis** — rainfall by season; correlation of
  environmental variables with yield
- **Resource usage analysis** — fertilizer/nutrient correlation with yield
  (overall and within-crop); water use & efficiency by irrigation method
- **Economic analysis** — revenue, cost, and profit by season and by crop
- **Regional/category analysis** — profit and yield by state and by crop
- **Statistical analysis** — one-way ANOVA (season, crop, state, irrigation),
  Welch's t-test (Kharif vs. Zaid profit, Drip vs. Flood yield), and Spearman
  correlation, all computed with SciPy and summarized in one results table

### Headline findings

- **Season is the strongest driver of performance.** Yield and profit both
  fall Kharif > Rabi > Zaid for every one of the 8 crops (log-yield ANOVA
  p < 0.001; profit ANOVA p < 0.001).
- **Zaid is loss-making on average**, with ~65% of Zaid farms unprofitable
  vs. ~42% in Kharif (Welch t-test p < 0.001).
- **Irrigation method outperforms geography as a lever**: Drip gives the
  best yield and profit; Flood uses the most water for the lowest profit and
  efficiency (ANOVA p < 0.001).
- **State-level differences are not statistically significant** for yield or
  profit (ANOVA p ≈ 0.60 / 0.56).
- **Fertilizer shows almost no relationship with yield** and a small
  negative correlation with profit; water applied is the strongest resource
  driver of yield of any input measured.

Full reasoning, every statistical test, and data-driven recommendations are
in the notebook's Key Insights, Recommendations, and Limitations sections.

## Dashboard

The notebook generates a single consolidated analytics dashboard
(`visualizations/00_final_dashboard.png`) containing:

- 6 KPI cards (farms analyzed, total production, total profit, profit
  margin, best season, best irrigation method)
- Main chart: seasonal yield & profitability trend
- Crop-wise Yield Index heatmap and Regional Performance by state
- Water usage/efficiency by irrigation and Rainfall by season
- Economic performance (revenue/cost/profit) by season
- A Key Insights panel with the six strongest, statistically-supported
  findings

13 additional individual charts from every analysis section are also saved
to `visualizations/`.

## How to Run

```bash
pip install -r requirements.txt
jupyter notebook notebooks/Seasonal_Agriculture_Performance_Analysis.ipynb
```

Run all cells (Kernel → Restart & Run All). The notebook reads
`data/agriculture_dataset.csv`, cleans it, recalculates every KPI and
statistic, regenerates every chart into `visualizations/`, and rebuilds the
final dashboard automatically — no manual steps or hard-coded values.

## Project Structure

```
Seasonal-Agriculture-Performance-Analysis/
│
├── data/
│   ├── agriculture_dataset.csv            # original raw dataset
│   └── agriculture_dataset_cleaned.csv    # output of the cleaning step
│
├── notebooks/
│   └── Seasonal_Agriculture_Performance_Analysis.ipynb
│
├── visualizations/
│   ├── 00_final_dashboard.png             # consolidated dashboard
│   └── 01–12_*.png                        # individual analysis charts
│
├── README.md
└── requirements.txt
```

## Final Output

A submission-ready Jupyter Notebook (20 sections: overview through
conclusion) and a professional, automatically-generated analytics dashboard
that together document the full pipeline from raw data to statistically
validated, evidence-based recommendations for seasonal agricultural
planning.
