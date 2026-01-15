# Phase 0: Project Planning & Problem Definition

*Goal: Align the technical work with the business objectives.*

* **Stakeholder Identification:** General Partners at a mid-sized VC firm looking to deploy $500M in emerging markets

* **Problem Statement:** Silicon Valley is saturated and expensive. How can we find untapped geographical hubs that produce high-value, capital-efficient startups in under 5 years?

* **KPIs:**
    * *Speed to Unicorn:* Years from foundation to $1B+
    * *Capital Efficiency Ratio:* Valuation $\div$ Total Funding.
    * *Market Saturation:* Density of unicorns per city/industry.

* **Data Dictionary:** Setting `Industry` and `Location` as primary filters, `Valuation` as the success metric.

# Phase 1: Data Engineering & Pre-processing (Excel/R)

*Goal: Perform heavy-duty aggregation and multi-dimensional filtering.*

* **Currency Normalization:** Used the following Excel formula to convert shorthand ($8B, $200M) into long-form integers:

    `IF(RIGHT(B2,1)="B", SUBSTITUTE(SUBSTITUTE(B2,"$",""),"B","")*1000000000, IF(RIGHT(B2,1)="M", SUBSTITUTE(SUBSTITUTE(B2,"$",""),"M","")*1000000, SUBSTITUTE(B2,"$","")*1))`

* **Date Standardization:** Converted all dates into the `YYYY-MM-DD` format

* **Data Integrity Check:**

    * Identified and fixed outliers in the date columns where `Year Founded` > `Date Joined` using the `DATEDIF` function.

    * Imputed missing values (like the Singapore,Hong Kong and Bahamas city gap).

* **Data Transformation (Wide to Long):** Created another dataset containing only company and investor columns by converting the wide data into long format using the following R script:

```r
# Load the necessary libraries
library(tidyverse)
library(readr)

# Read the data
df <- read_csv("dataset_long_temp.csv")

# Convert from wide to long
df_long <- df %>%
separate_rows(investors, sep = ",") %>%
mutate(investors = str_trim(investors))

# View result
view(df_long)

# Save the file
readr::write_csv(df_long, "dataset_long.csv")
```

* **Final Export:** Generated two cleaned `.csv` files to be used in all subsequent tools.

# Phase 2: Database Management & SQL Analysis

*Goal: Establish the baseline metrics.*

* **Schema Design:** Imported the cleaned data into MySQL with appropriate data types.

* **The "Efficiency" Query:** Performed the following SQL query to filter the companies that reached Unicorn status within 5 years:
```sql
SELECT company, years_to_unicorn
FROM (
	SELECT
        company,
        YEAR(date_joined) - YEAR(year_founded) AS years_to_unicorn
	FROM dataset
	GROUP BY company, years_to_unicorn
    ) AS yu
WHERE years_to_unicorn <= 5
ORDER BY years_to_unicorn;
```

* **Geographic Grouping:** Performed the following query to find the `Average Valuation` per startup per country:
```sql
SELECT
	country,
    avg(valuation) AS average_valuation
FROM dataset
GROUP BY country
ORDER BY average_valuation DESC;
```

* **Investor Counting:** Wrote the following query to identify which specific investors appear most frequently in the "Top 10%" of the most efficient startups:

```sql
WITH enriched AS (
    SELECT
        company,
        investors,
        YEAR(date_joined) - YEAR(year_founded) AS years_to_unicorn
    FROM dataset_long
    WHERE YEAR(date_joined) - YEAR(year_founded) <= 5
),
ranked AS (
    SELECT
        company,
        investors,
        years_to_unicorn,
        NTILE(10) OVER (ORDER BY years_to_unicorn) AS decile
    FROM enriched
)

SELECT
    investors,
    COUNT(*) AS companies_invested
FROM ranked
WHERE decile = 1
GROUP BY investors
ORDER BY companies_invested DESC;
```

* **Top valued industries:** Identified industries with the highest company valuations.

```sql
SELECT
    industry,
    SUM(valuation) AS total_valuation
FROM dataset
GROUP BY industry;
```

# Phase 3: Statistical Discovery & Advanced EDA (R)

*Goal: Find correlations and distributions that simple charts might miss.*

*The analyses and results for this phase are fully documented in the accompanying R Markdown file named "phase_3_statistical_discovery.Rmd".*

# Phase 4: Visual Storytelling & BI (Tableau)

