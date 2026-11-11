# China's Solar PV Export Markets, 2022–2025

**ENVIRON 712L | Team zwz | ZhengWangZhouLi**

This project examines how economic conditions, solar resources, existing PV deployment and regional time trends relate to the destination patterns of China's solar PV exports.

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

AI was used to help identify relevant datasets and assist with writing and troubleshooting the analysis code. Data sources were verified against the original providers, and code outputs were checked for consistency with the underlying data.
