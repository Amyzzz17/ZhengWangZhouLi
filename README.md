# ZhengWangZhouLi

**712L Solar Project | Group Repository**

## 1. Team Information

**Team Name:** zwz

**Team Members:**
- Amy Zheng
- Ziyan Wang
- Xuan Zhou
- Reynold Li

## 2. Research Overview

### Main Research Question

**Which destination markets, product categories, and sales periods should Chinese solar PV exporters prioritize to improve expected commercial returns?**

### Research Description

This project aims to analyze China's solar photovoltaic (PV) export patterns to identify promising international markets, evaluate product positioning opportunities, and improve export timing and commercial decision-making.

Our analysis focuses on four supporting questions:

**1. Market Selection**

Which destination markets have the largest and most sustained growth in China's solar PV exports?

**2. Product Positioning**

How does the composition of China's solar PV exports differ across destination markets and evolve over time? How do these patterns align with local PV deployment and manufacturing activity?

**3. Export Timing**

Do priority country-product markets exhibit recurring monthly export patterns that can support shipment planning?

**4. Commercial Feasibility**

Which country-product opportunities remain commercially attractive under alternative assumptions?

## 3. Intended Audience

Our research is primarily intended for:

**Chinese Solar PV Manufacturers and Exporters**
- Business development teams identifying high-potential export markets
- International sales teams optimizing product positioning and shipment timing
- Strategic planning teams evaluating market opportunities and commercial profitability

**Trade Associations and Export Advisory Organizations**
- Organizations supporting Chinese solar PV companies with international market entry and expansion strategies
- Industry advisors providing market intelligence and export recommendations

## 4. Project Objectives

Through this analysis, we aim to:

1. Identify high-growth and sustainable destination markets for China's solar PV exports.
2. Examine product-level export patterns across international markets.
3. Explore recurring monthly export trends to support shipment planning.
4. Evaluate potential commercial opportunities under different assumptions.

## 5. Data Sources and Access

This project uses the **Ember China Solar Export dataset**, based on export records from the General Administration of Customs of China (GACC). Ember supplements the customs data with reference prices and estimated export capacity.

- [Dataset page](https://ember-energy.org/data/china-solar-exports-data/)
- [Download the CSV](https://files.ember-energy.org/public-downloads/customs/outputs/mart_solar_exports_full_release_monthly.csv)

The dataset is updated monthly. To support reproducibility, the notebook preserves the uploaded CSV snapshot in `data/Raw/mart_solar_exports_full_release_monthly.csv`. 

## 6. Analysis Scope and Unit of Observation

The preliminary analysis uses the following filters:

- **Product:** `Commodity type == "Panels"`
- **Period:** January 2022 through December 2025
- **Geographic level:** `Area type == "Country or economy"`

Each row in the processed country-level dataset represents **China’s solar panel exports to one destination country or economy during one reporting month**.

Regional and global aggregate rows are excluded to prevent double counting. The analysis starts in 2022 because the customs classification separately identifies assembled photovoltaic modules and panels from that year onward.

The selected sample contains **8810 observations, 228 destinations, and 48 distinct reporting months**.

## 7. Data Dictionary

Definitions follow Ember’s methodology where documented. Geographic labels and date encoding describe the supplied CSV.

| Variable | Unit | Definition |
|---|---|---|
| `Area` | None | Recorded first destination country or economy. This may differ from the final consumption destination. |
| `Date` | YYYY-MM-DD | Reporting month, encoded as the first day of that month. |
| `Area type` | None | Geographic classification of the record. This analysis retains only `Country or economy`. |
| `Region` | None | Regional classification supplied for the destination. |
| `Commodity code` | HS code | Customs product classification. Panels use code `85414300` during the selected period. |
| `Commodity type` | None | Solar product category. This stage retains `Panels`. |
| `Amount (items)` | Items | Export quantity reported in the customs data. |
| `Amount (kg)` | Kilograms | Export weight reported in the customs data. |
| `Amount (USD)` | US dollars | Export value reported in the customs data. This measures trade value, not profit. |
| `Commodity price` | USD/W for panels | Monthly average reference price used by Ember, based on InfoLink prices and product-type weights. It is not a destination-specific transaction price. |
| `Price unit` | None | Unit associated with `Commodity price`; `USD/W` for the selected panel records. |
| `Capacity (MW)` | Megawatts | Ember’s estimated monthly export capacity. For panels, capacity is calculated using export value and the monthly reference price, with conversion from watts to megawatts. |
| `Cumulative capacity (MW)` | Megawatts | Cumulative capacity supplied in the source file. The cited methodology does not specify its exact accumulation convention. It is retained for provenance but is not used in aggregation. |
| `year` | Calendar year | Year extracted from `Date`. |
| `month` | Month number, 1–12 | Month extracted from `Date`. |
| `value_growth_pct` | Percent | Annual export-value growth: `(current annual value / previous annual value - 1) * 100`. |
| `capacity_growth_pct` | Percent | Annual estimated-capacity growth: `(current annual capacity / previous annual capacity - 1) * 100`. |

The growth-rate variables appear in the annual summary. Their values for 2022 are missing by design because 2022 is the baseline year.

## 8. Import and Cleaning Workflow

The analysis is implemented in `Solar_A2_ENVIRON712_ZhengWangZhouLi.ipynb` using Python, pandas, NumPy, and Matplotlib.

To reproduce the analysis:

1. Open the notebook in Google Colab.
2. Run the first code cell and upload the Ember CSV.
3. Run the remaining cells in order.
4. Review the audit results, exploratory figures, and annual growth table.
5. Run the saving and download cells to obtain the processed datasets.

The workflow:

- Preserves the original uploaded CSV.
- Converts the reporting date to a datetime variable.
- Selects Panels, 2022–2025, and country/economy records.
- Checks missing values, duplicates, numeric plausibility, and monthly coverage.
- Creates year and month variables.
- Aggregates export value and estimated capacity by month and year.
- Calculates annual growth rates separately for value and capacity.
- Saves the processed datasets to `data/Processed/`.

No external datasets are joined in this stage as we are still looking for it. Unmatched join keys and before/after join counts are therefore not applicable. The notebook reports row counts before and after filtering.

## 9. Data Quality Findings and Cleaning Decisions

For the uploaded snapshot:

- The original dataset contains **31,624 rows and 13 columns**.
- The selected sample contains **8,810 rows**.
- The selected sample has **no missing cells**, **no exact duplicate rows**, and **no duplicate destination-month-product keys**.
- No negative values were found in the checked numeric fields.
- **160 records have zero estimated monthly capacity despite positive export value**. Rounding of small shipments is a plausible explanation, but it has not been independently verified. These records are retained.
- **111 destinations have observations in all 48 months**.
- Relative to the 228 observed destinations × 48 months, **2,134 destination-month combinations are absent**.

Absent records are not automatically treated as zero exports. They may reflect no recorded trade or a reporting issue. No missing-value imputation, automatic duplicate removal, or size-based outlier deletion is performed.

The notebook contains the audit code, detailed outputs, and explanatory assessment.

## 10. Processed Datasets and Preliminary Analysis

The notebook saves three files:

| File | Unit of observation | Contents |
|---|---|---|
| `data/Processed/panels_processed.csv` | One destination-month-panel record | Filtered country-level data with year and month variables. |
| `data/Processed/monthly_exports.csv` | One reporting month | Export value and estimated capacity summed across available country/economy records. |
| `data/Processed/annual_exports.csv` | One calendar year | Annual export value, estimated capacity, and their annual growth rates. |

The preliminary exploratory analysis includes:

- Descriptive statistics for country-month export records.
- Monthly export-value trends in billion USD.
- Monthly estimated export-capacity trends in GW.
- Annual export totals and growth rates.

In this snapshot, annual panel export value falls from approximately **USD 42.35 billion in 2022 to USD 23.69 billion in 2025**, while estimated capacity rises from **155.76 GW to 248.37 GW**. These patterns motivate examining both monetary value and physical scale when evaluating markets.

## 11. Limitations

- **Estimated capacity:** Panel capacity is derived from export value and monthly reference prices. Value and capacity are mechanically related and should not be interpreted as independent measurements.
- **Incomplete monthly coverage:** Country-level growth comparisons require attention to missing destination-month records and comparable coverage.
- **Commercial interpretation:** Export value is not profit. The dataset does not contain manufacturing costs, freight, tariffs, contract-level prices, or attainable firm sales volumes.
- **Product scope:** This stage analyzes Panels only. We chose panels as it is the dominant product type in the dataset. 
- **Seasonality:** Four years provide only four observations for each calendar month. Monthly fluctuations alone do not establish stable shipment-timing patterns.
- **Data revisions:** Results may change when Ember updates or revises the source dataset.