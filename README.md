# Chasing Billions: The Global Unicorn Landscape

Funding, Valuation, and Growth Dynamics of Billion-Dollar Startups

## Overview

This project analyzes global unicorn companies (privately valued startups worth $1B+) to identify "efficient" unicorns, which have reached $1B+ valuation in less than 5 years. The analysis uncovers underserved, high-growth markets for venture capital investment.

## Key Insights

- **Capital does not buy speed:** Virtually zero correlation (-0.03) between total funding and time to unicorn status—a well-targeted $300M Series can be as effective as $600M.
- **AI startups are fastest:** AI companies reach unicorn status 1 year faster than Fintech (5 vs. 6 years median).
- **Geographic opportunity exists:** China dominates AI valuation ($214B vs. US $135B), while India and Southeast Asia offer lower competition with similar growth timelines.
- **Investor concentration:** A "super-cluster" of co-investors (Tiger Global, SoftBank, Sequoia China, Tencent) controls high-valuation outcomes.

For the full technical analysis and methodology, see the [Quarto report](https://himangshuchetia-hc17.github.io/the-global-unicorn-landscape/main.html).

## Dashboard

View the interactive dashboard on [Tableau Public](https://public.tableau.com/views/TheGlobalUnicornLandscape/Dashboard?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link).

## Project Files

| File | Description |
|------|-------------|
| `main.qmd` | Quarto source for the technical report |
| `main.html` | Rendered interactive report |
| `dataset.csv` | Original unicorn company data |
| `dataset_long.csv` | Investor-normalized format (one row per investor) |
| `geocoded_unicorns.csv` | Data with latitude/longitude coordinates |

## Tech Stack

- Excel
- SQL
- R (tidyverse, ggplot2, igraph)
- Quarto
- Tableau

## How to Reproduce

1. Clone this repository
2. Install R and required packages:
   ```r
   install.packages(c("tidyverse", "scales", "knitr", "viridis", 
                      "maps", "treemapify", "ggraph", "igraph", "networkD3"))
   ```
3. Render the Quarto report:
   ```bash
   quarto render main.qmd
   ```

## Data Source

- **Dataset:** Unicorn Companies Global Valuations
- **Platform:** Kaggle
- **Author:** Adil Shamim

## Limitations

- Survival bias: Excludes companies that exited via IPO or acquisition
- Founding date assumption: Companies assumed founded on January 1st of their founding year
