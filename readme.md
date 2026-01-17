---
title: "Chasing Billions: The Global Unicorn Landscape"
author: "Himangshu Chetia"
date: "2024-06-10"
output: html_document
---

### Strategic Analysis of $1B+ Private Startups

## The Business Problem
A Venture Capital (VC) firm wants to identify "efficient" unicorns (reaching $1B in <5 years) outside Silicon Valley to find underserved, high-growth markets.

## Analytical Pipeline (Tech Stack)
* **Excel:** Data entry, validation, and complex string manipulation to convert string values like `$8B` into integer values.
* **SQL:** Structured querying and aggregation of the 1000+ company dataset.
* **R:** Converting data from wide to long format, statistical analysis and R Markdown reporting.
* **Tableau:** [Link to Dashboard] Interactive visualization of investor networks.

## Key Performance Indicators (KPIs)
1. **Speed to Unicorn:** Years from foundation to $1B+
2. **Capital Efficiency Ratio:** Valuation $\div$ Total Funding.
3. **Elite Investors:** Investors with stakes in the top 10% most efficient startups.
4. **Market Saturation:** Density of unicorns per city/industry.

## Data Integrity & Cleaning
* **Currency Normalization:** Converted mixed-string funding `($B/$M)` into integers for calculation.
* **Investor Parsing:** Created a "long" version of the data (where one company has multiple rows, one for each investor) using R & the `tidyverse()` package.
* **Spatial Correction:** Imputed missing city data for Singapore, Hong Kong and Bahamas entities.
* **Outlier Handling:** Addressed data entry errors (e.g., founded dates listed after join dates).

## Limitations & Assumptions
* **Survival Bias:** Data excludes companies that have already exited via IPO or Acquisition.
* **Founding Date Assumption:** Companies are assumed to be founded on Jan 1st of their founding year for time-series calculations.

## Data Source
* **Dataset:** Unicorn Companies Global Valuations
* **Platform:** Kaggle
* **Author:** Adil Shamim
* **Description:** This dataset provides a comprehensive list of "Unicorn" companies (private companies valued at over $1 billion). It includes key metrics such as current valuation, total funding raised, industry sector, headquarters location (City, Country, Continent), the year the company was founded, and the names of primary investors.
* **Citation:** Shamim, A. (2024). Startup growth and investment data [Data set]. Kaggle. https://www.kaggle.com/datasets/adilshamim8/startup-growth-and-investment-data

## Executive Summary (The "TL;DR")
* **The Trend:** [Insert your top finding here, e.g., "Fintech in Southeast Asia is scaling 20% faster than in Europe."]
* **The Opportunity:** Identified 3 underserved cities where "Capital Efficiency" is higher than Silicon Valley.
* **The Action:** Recommended a diversification strategy into [Industry] within [Region].