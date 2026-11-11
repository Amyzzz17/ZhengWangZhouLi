# China's Solar PV Export Markets, 2022–2025

**ENVIRON 712L | Team zwz | ZhengWangZhouLi**

This project examines how economic conditions, solar resources, existing PV deployment and regional time trends relate to the destination patterns of China's solar PV exports.

**Start here:** [Read the full analytical report](Docs/Analytical_Report_712L.pdf). The PDF brings together the group's exploratory figures, four supporting research questions, regression results, summary tables, diagnostic checks and interpretation. It is the project-level report; the notebooks and section-level outputs provide supporting analysis.

## 1. Team

**Team name:** zwz

- Amy Zheng
- Ziyan Wang
- Xuan Zhou
- Reynold Li

## 2. Research Question and Audience

**Central research question**

What economic, environmental, and market-development characteristics are associated with the destination patterns of China's solar PV exports, and how did regional export-capacity trends change from 2022 to 2025?

**Intended audience**

The project informs Chinese solar PV manufacturers and exporters, energy-market analysts, policymakers, trade associations and export advisors interested in understanding destination markets and regional export patterns. Its findings support further market research and descriptive comparisons. The available data do not estimate firm-level profits or establish causal effects.

## 3. Supporting Research Questions and Methods

| Research question | Analysis |
|---|---|
| **RQ1: Population and GDP.** Are GDP and population associated with export capacity, and do the relationships differ between countries and regions? | Four simple OLS comparisons using country and regional averages over matched years in 2022–2025, with logarithmic transformations. The reported samples contain 197 countries and seven regions. |
| **RQ2: Solar radiation.** Do countries with greater solar resource availability receive more Chinese panels? | Country-year regression of log annual panel-export capacity on annual irradiation, adjusting for population, real GDP per capita, prior-year installed PV, region and year. Inference is clustered by destination. The main sample contains 526 observations from 151 destinations. |
| **RQ3: Prior-year installed capacity.** Is existing PV deployment associated with subsequent Chinese panel imports? | Match 2021–2024 year-end installed PV capacity to 2022–2025 panel exports. Estimate a region- and year-adjusted ln(1+x) model with destination-clustered inference. The report covers 549 matched destination-years from 160 destinations. |
| **RQ4: Regional growth trends.** How do monthly export-capacity trends differ across destination regions? | Estimate region-specific intercepts and time slopes with calendar-month effects over 48 months and seven regions. Use Driscoll–Kraay inference, a joint equal-slopes test, Holm-adjusted pairwise comparisons and lag-sensitivity checks. |

The preliminary overview describes geographic distribution, product composition and monthly export patterns before the question-specific analyses.

## 4. Data Sources and Scope

| Data | Source | Use |
|---|---|---|
| Solar PV exports | [Ember China Solar Exports](https://ember-energy.org/data/china-solar-exports-data/), based on China customs records | Monthly export value, product categories and estimated capacity for 2022–2025. |
| Population | [World Bank: Population, total](https://data.worldbank.org/indicator/SP.POP.TOTL) | Population comparisons in RQ1 and a control variable in RQ2. |
| GDP | [World Bank: GDP, current US$](https://data.worldbank.org/indicator/NY.GDP.MKTP.CD) | Total nominal GDP in RQ1. |
| Real GDP per capita | [World Bank: GDP per capita, constant prices](https://data.worldbank.org/indicator/NY.GDP.PCAP.KD) | A separate income control in RQ2; the saved field is `real_gdp_pc_2015_usd`. |
| Solar radiation | [NASA POWER](https://power.larc.nasa.gov/docs/services/aws/) | Actual annual irradiation for 2022–2025, aggregated into country-level area-weighted averages in kWh/m²/year. |
| Installed solar PV capacity | [IRENASTAT](https://pxweb.irena.org/pxweb/en/IRENASTAT/) | Previous-year market development, with 2021–2024 capacity matched to 2022–2025 exports. |

**Product scope and units**

- RQ1 and several exploratory figures combine Panels, Cells and Wafers. Their totals represent summed product-stage capacity equivalents, which can include related upstream and downstream trade.
- RQ2, RQ3 and the RQ4 regional time-trend model analyze **Panels only**.
- Monthly source capacity is in MW. Figures may show GW-equivalent exports; individual regressions use their stated log transformations and units.
- Installed PV capacity is a cumulative stock. Export capacity measures a trade flow. These quantities are interpreted separately.
- Country/economy records are used for destination aggregation so that supplied regional and global totals are not counted again.
- Missing observations are not automatically replaced with zero. Each analysis reports its own matching and sample rules.

The observation unit varies across analyses: country or regional averages in RQ1, destination-years in RQ2–RQ3, and region-months in RQ4. The results therefore do not all use the same sample or denominator.

## 5. Repository Guide

```text
Docs/             Full report, section-level HTML and team charter
Scripts/          Exploratory and statistical-analysis notebooks
data/Raw/         Saved source-data snapshots
data/Processed/   Cleaned and matched analysis inputs
Results/          Saved figures
README.md         Project overview and reproduction instructions
```

Some RQ1 summary CSV files and figures are also saved at the repository root.

### Analysis files

| Component | Notebook or report location |
|---|---|
| Full project report | [Docs/Analytical_Report_712L.pdf](Docs/Analytical_Report_712L.pdf) |
| RQ1: Population and GDP | [Scripts/Q1_GDP_pop.ipynb](Scripts/Q1_GDP_pop.ipynb) |
| RQ2: Solar radiation | [Scripts/Solar_Radiation_Country_Year_Regression.ipynb](Scripts/Solar_Radiation_Country_Year_Regression.ipynb) |
| RQ3: Prior-year installed capacity | Section 3.4 of the [full project report](Docs/Analytical_Report_712L.pdf) |
| RQ4: Regional time trends / Part 4 | [Scripts/Model4_All_Region_Trend_Regression.ipynb](Scripts/Model4_All_Region_Trend_Regression.ipynb) |
| Preliminary geographic overview | [Scripts/Figure1.ipynb](Scripts/Figure1.ipynb) |
| Preliminary regional export value | [Scripts/Figure_2_Regional_Export_Value.ipynb](Scripts/Figure_2_Regional_Export_Value.ipynb) |
| Preliminary regional export capacity | [Scripts/Figure_3_Regional_Export_Capacity.ipynb](Scripts/Figure_3_Regional_Export_Capacity.ipynb) |
| Preliminary high/low destination comparison | [Scripts/Figure4_high_low_countries.ipynb](Scripts/Figure4_high_low_countries.ipynb) |

The exploratory notebook named `Figure4_high_low_countries.ipynb` is a country comparison; **Part 4 of the analytical report** is the regional time-trend analysis in `Model4_All_Region_Trend_Regression.ipynb`.

### Selected saved outputs

- [Population and GDP comparisons](solar_four_regressions_2022_2025.png)
- [RQ1 regression summary](solar_regression_results_2022_2025.csv)
- [Solar-radiation HTML report](Docs/Solar_Radiation_Country_Year_Regression.html)
- [Monthly panel capacity by region](Results/region_monthly_panel_capacity.png)
- [Regional trend estimates and confidence intervals](Results/region_slope_comparison.png)

Download HTML files and open them in a browser to view the rendered reports. GitHub may display their source rather than the rendered page.

## 6. Reproducing and Updating the Analysis

### Open the project

Clone or pull this repository and open the repository folder in VS Code. Use the saved data snapshots in the repository for the reported study period.

Install the common analysis and HTML-export packages in the Python environment selected for the notebook:

```bash
python3 -m pip install pandas numpy matplotlib scipy statsmodels nbconvert ipykernel
```

### Run an analysis

1. Open the notebook corresponding to the research question in the table above.
2. Select its Python environment and follow the input configuration provided in that notebook.
3. Run the cells in order, review the figures and tables, and save the executed notebook with its outputs.

**RQ1 inputs:** `data/solarexport_data.csv`, `data/Raw/global_Pop.csv` and `data/Raw/global_GDP.csv`.

**RQ2 inputs:** the analysis starts directly from the following saved processed files:

- `data/Processed/panels_processed.csv`
- `data/Processed/solar_radiation_country_year.csv`
- `data/Processed/solar_radiation_country_year_2022_2025.csv`

For RQ2, the last file supplies country mapping and market controls. Its previous radiation values, combined-product outcome and sample flag are not used. The notebook rebuilds the Panels-only outcome and sample. Rerunning NASA data preparation is not required for this workflow.

**RQ3 methods, results and checks:** see Section 3.4 of the full project report.

**RQ4 input:** `data/Raw/mart_solar_exports_full_release_monthly.csv`. The notebook selects country-level Panels records and aggregates them to region-months. Generated coefficient, comparison and diagnostic tables are written to the notebook's configured `OUT_DIR`, which defaults to `Model4_All_Regions_Results` under the working directory.

### Regenerate an HTML report

After running and saving the relevant notebook, use **Export → HTML** in VS Code. To export a report with code inputs hidden, run the corresponding command from the repository root:

```bash
python3 -m nbconvert --to html --no-input --embed-images Scripts/Q1_GDP_pop.ipynb --output-dir Docs
python3 -m nbconvert --to html --no-input --embed-images Scripts/Solar_Radiation_Country_Year_Regression.ipynb --output-dir Docs
python3 -m nbconvert --to html --no-input --embed-images Scripts/Model4_All_Region_Trend_Regression.ipynb --output-dir Docs
```

These commands export saved notebook content and outputs. The full project PDF is an assembled report; update its source document and re-export it when the analysis changes. Save updated notebooks, reports and relevant outputs in the repository.

## 7. Main Findings in the Current Report

1. **Established PV markets tend to receive more subsequent exports.** Previous-year installed capacity is positively associated with next-year Chinese panel exports in the reported region- and year-adjusted analysis.
2. **Solar resource availability alone may not fully explain import patterns.** The main adjusted irradiation estimate is positive, but the evidence is sensitive to the sample and model specification.
3. **Regional export scale and trend growth differ.** Asia, the Middle East and Africa have strong positive estimated monthly trends, while Europe has the largest cumulative panel-export capacity over the study period. Overall regional trends differ, but not every pairwise comparison is statistically significant.

These are descriptive findings. Refer to the full report for estimates, confidence intervals, sample definitions and interpretation.

## 8. Robustness Checks and Limitations

The report examines geographic aggregation in RQ1; complete-series and country-effects comparisons in RQ2; coverage, re-export-hub and data-source sensitivities in RQ3; and residual dependence, lag choices and multiple-comparison correction in RQ4.

Important limitations are:

- Ember estimates panel-export capacity using trade value and monthly reference prices. Value and estimated capacity are not independent measures.
- Recorded first destinations may be re-export hubs, rather than final installation markets.
- Combined Panels, Cells and Wafers totals can overlap across production stages and are not unique installed capacity or final demand.
- Matching, missing values and coverage rules produce different samples across research questions.
- National-average irradiation can mask local variation, and the regional time model has only 48 months per region.
- Statistical associations and fitted trends do not establish causation or predict firm-level profits.

## 9. AI Use Statement

AI was used to help identify relevant datasets and assist with writing and troubleshooting the analysis code, particularly for **Part 4: the multi-region time-trend regression**. Data sources were verified against the original providers, and code outputs were checked for consistency with the underlying data.

## 10. Earlier Project Documentation

The earlier README is retained below to preserve the project's initial questions, data dictionary, cleaning notes and historical workflows. The current report and instructions above describe the present analytical draft. Historical sample counts and product scopes refer to the stages in which they were recorded.

<details>
<summary>Earlier README and preparation notes</summary>

# ZhengWangZhouLi

**712L Solar Project | Group Repository**

**Solar-radiation analytical draft:** [Open the HTML report file](Docs/Solar_Radiation_Country_Year_Regression.html). Download it and open it in a web browser to read the rendered report. Instructions for reproducing this section from processed data are in **Section 13**.

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

Additional sources used in the country-year solar-radiation analysis are:

- **Solar radiation:** [NASA POWER](https://power.larc.nasa.gov/docs/services/aws/), annual solar radiation for 2022–2025, aggregated into country-level area-weighted averages.
- **Population and real GDP per capita:** World Bank ([population](https://data.worldbank.org/indicator/SP.POP.TOTL), [real GDP per capita](https://data.worldbank.org/indicator/NY.GDP.PCAP.KD)).
- **Previous-year installed solar PV capacity:** [IRENA](https://www.irena.org/Publications/2026/Mar/Renewable-capacity-statistics-2026), with 2021–2024 capacity matched to 2022–2025 exports.

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

## 12. Figure 3 analytical-report contribution

The following additional Figure 3 report files are local drafts. These notes are retained for project history; this section is separate from the processed-data solar-radiation workflow in Section 13.

Open `Docs/Figure_3_Analytical_Report.html` in a browser. It contains Figure 3, two main findings, the annual summary, the existing complete-coverage check, and two peer-review questions. This Figure 3 section covers Panels, Cells and Wafers in 2022–2025.

To reproduce it, run `Scripts/Figure_3_Analytical_Report.ipynb` with the existing Figure 3 CSV files in `data/Processed/`. Save the executed notebook and render from the repository root with:

```bash
jupyter nbconvert --to html --no-input Scripts/Figure_3_Analytical_Report.ipynb --output-dir Docs
```

## 13. Country-year solar-radiation regression

**Supporting question:** Is annual solar irradiation associated with solar-panel imports from China?

**Scope:** Panels only, 2022–2025. Each observation represents one destination country/economy in one year.

**Report:** `Docs/Solar_Radiation_Country_Year_Regression.html`. Download and open this file in a web browser. It contains the research question and hypotheses, four annual scatterplot panels, a regression table, two main findings, and robustness and residual checks.

### Required processed inputs

| File | Purpose |
|---|---|
| `data/Processed/panels_processed.csv` | Monthly Panels-only exports, aggregated to country-year capacity in the notebook. |
| `data/Processed/solar_radiation_country_year.csv` | NASA POWER annual country-level solar irradiation. |
| `data/Processed/solar_radiation_country_year_2022_2025.csv` | Existing country mapping, population, real GDP per capita and previous-year installed PV capacity. |

The existing matched file has 866 destination-years. Its previous combined-product outcome, radiation values and sample flags are not used in the revised analysis. Panels-only annual aggregation and coverage rules are recomputed in the regression notebook. The main model uses 526 observations from 151 countries/economies; the complete 48-month Panels comparison uses 433 observations from 109 destinations. Population, real GDP per capita and prior-year PV capacity come from the existing matching workbook.

### Reproduce the analysis

The default workflow starts from the three processed CSV files above. Raw-data downloads and the preparation notebook are not required to run the regression.

1. Clone or pull this repository and open its root folder in VS Code.
2. Install the analysis and export packages in the Python environment selected for the notebook:

   ```bash
   python3 -m pip install pandas numpy matplotlib statsmodels nbconvert ipykernel
   ```

3. Open `Scripts/Solar_Radiation_Country_Year_Regression.ipynb`, select that Python environment, and choose **Run All**. The notebook can run from the repository root or `Scripts/`.
4. Save the executed notebook, including its figures, table and findings.
5. From the repository root, export the report:

   ```bash
   python3 -m nbconvert --to html --no-input --embed-images Scripts/Solar_Radiation_Country_Year_Regression.ipynb --output-dir Docs
   ```

6. Open the updated `Docs/Solar_Radiation_Country_Year_Regression.html` in a browser. Commit the saved notebook and regenerated HTML when updating the analysis.

### AI use and checks

AI assisted with drafting Python code and report text. Checks included country-year keys, units, annual export aggregation, sample counts, regression results, robustness comparisons and successful execution of the analysis. The report contains the fuller AI-use statement and limitations.

