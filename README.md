# Chasing Billions: The Global Unicorn Landscape

Funding, Valuation, and Growth Dynamics of Billion-Dollar Startups

## Overview

This project analyzes global unicorn companies (privately valued startups worth $1B+) to identify "efficient" unicorns—those reaching $1 billion valuation in less than 5 years—outside Silicon Valley. The analysis uncovers underserved, high-growth markets for venture capital investment.

## Project Scope

The project answers key questions:

- Which startups reached unicorn status most efficiently?
- What are the capital efficiency ratios for top performers?
- Which investors have stakes in the most efficient startups?
- How saturated are different markets with unicorns?

## Key Performance Indicators

1. **Speed to Unicorn:** Years from foundation to $1B+ valuation
2. **Capital Efficiency Ratio:** Valuation divided by total funding raised
3. **Elite Investors:** Investors with stakes in top 10% most efficient startups
4. **Market Saturation:** Unicorn density per city and industry

## Tech Stack

- Excel: Data entry, validation, and string manipulation
- SQL: Structured querying and aggregation of 1000+ companies
- R: Data transformation (wide to long format) and statistical analysis
- Tableau: Interactive visualizations

## Data

- Source: Kaggle - "Unicorn Companies Global Valuations" by Adil Shamim
- Files:
  - `dataset.csv`: Original unicorn company data
  - `dataset_long.csv`: Investor-normalized format (one row per investor relationship)
  - `geocoded_unicorns.csv`: Spatially corrected data
  - `main.html`: Interactive Quarto report (rendered from main.qmd)

## Data Quality

- Currency normalized: Converted mixed-format funding values to integers
- Investor parsing: Created long-format dataset for relationship analysis
- Spatial correction: Imputed missing city data
- Outlier handling: Corrected data entry errors (e.g., founding dates after joining dates)

## Limitations

- Survival bias: Excludes companies that exited via IPO or acquisition
- Founding date assumption: Companies assumed founded on January 1st of their founding year
