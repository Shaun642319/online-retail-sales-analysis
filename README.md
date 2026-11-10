# Online Retail Sales & Customer Analysis

**Python · pandas · Matplotlib · Exploratory Data Analysis · Business Insights**

An end-to-end exploratory analysis of **541,909 transaction-line records** from a UK-based online retailer, covering **1 December 2010 to 9 December 2011**. The project investigates sales trends, product performance, customer purchase behaviour, international markets, repeat purchasing and invoice timing.

> **Project notebook:** [Open the complete analysis](retail_analysis_.ipynb) — includes code, visualizations, data-quality investigations and a business recommendations section.

## Business questions

1. How did monthly merchandise sales change over time?
2. Which products generated the most units sold and net revenue?
3. Which customers generated the most revenue, and how did order frequency relate to average order value?
4. Which countries contributed the most merchandise revenue?
5. How common were repeat purchases, and how was purchase frequency distributed?
6. On which weekdays and at what hours was the most revenue recorded?

## Key findings

| Metric | Result |
|---|---:|
| Gross merchandise sales | **£10,666,684.54** |
| Recorded cancellation value | **£896,812.49** |
| Net merchandise sales | **£9,769,872.05** |
| UK share of net merchandise revenue | **84.03%** |
| Share of identifiable net customer revenue from top 10 customers | **16.60%** |
| Gross average order value, identifiable customers | **£476.10** |
| Customers making more than one purchase | **2,830 of 4,335 (65.28%)** |
| Mean / median purchases per customer | **4.25 / 2** |
| Top product by net units | **WORLD WAR 2 GLIDERS ASSTD DESIGNS** (53,847 units) |
| Top product by net revenue | **REGENCY CAKESTAND 3 TIER** (£164,762.19) |

**Further observations:** November 2011 was the strongest *full* month in the data. Thursday generated the highest cumulative weekday merchandise revenue; noon was the highest-revenue invoice hour. The correlation between purchase frequency and gross AOV among customers with AOV below £5,000 was **r = 0.12**, indicating a very weak positive linear relationship in that filtered population.

**Interpretation:** The retailer was highly reliant on UK sales. The most frequently purchased products were not necessarily the greatest revenue contributors. Repeat purchasing was common, but a relatively small group of very frequent buyers pulled the mean above the median. These patterns suggest avenues for further investigation, not causal conclusions or verified profit opportunities.

## Data and methodology

**Source:** [UCI Machine Learning Repository — Online Retail](https://archive.ics.uci.edu/dataset/352/online+retail).

The source contains invoice line items (multiple rows can belong to one order), and covers product codes, quantity, invoice timestamps, unit price, customer IDs and country.

Main steps:

- Calculated line value as `Quantity × UnitPrice`.
- Separated positive-price merchandise sales from recorded cancellation invoices (whose invoice numbers begin with `C`).
- Reconciled all **541,909 rows** into 530,104 positive-sales rows, 9,288 cancellation rows and 2,517 excluded non-merchandise/zero-price rows.
- Isolated **£22,124.12 in bad-debt accounting adjustments**, keeping these separate from merchandise revenue. The recorded total including those adjustments is **£9,747,747.93**.
- Investigated **5,268 exact duplicate rows**; retained them because the dataset lacks unique invoice-line identifiers. Removing exact duplicates would change the original recorded value by **£21,740.98** (approximately 0.22% of merchandise net sales). The notebook also includes a merchandise-only duplicate sensitivity check.
- Aggregated sales by month, product, customer and country, then analyzed repeat ordering and invoice timing.
- Created Matplotlib bar charts, scatter plots and purchase-frequency histograms.

**Definitions matter:** The customer AOV shown here is **gross purchase AOV before cancellations**, whereas net merchandise sales incorporate recorded cancellations. Customer metrics are limited to records with identifiable customers. The repeat-purchase rate is not a cohort-based retention rate.

## Tools

- Python
- pandas
- Matplotlib
- Jupyter Notebook / Google Colab
- openpyxl (Excel reader used by pandas)

## Run the project

1. Download the dataset from the [UCI source](https://archive.ics.uci.edu/dataset/352/online+retail).
2. Rename the Excel workbook to **`Online_Retail.xlsx`** and place it in the same working directory as `retail_analysis.ipynb` (or upload it to the Colab session).
3. Install the Python packages if running locally:

   ```bash
   pip install -r requirements.txt
   ```

4. Open `retail_analysis.ipynb` in Jupyter or Google Colab and select **Run All**.
5. Charts are shown in the notebook and saved as PNG files when their cells are run.

**Note:** The source workbook is not included in this repository. Download it separately from UCI.

## Limitations

- The source period is historical (2010–2011), and **December 2011 is incomplete**.
- Missing `CustomerID` values mean customer metrics do not cover every transaction.
- Some large positive invoices were later cancelled; gross AOV can therefore be misleading if interpreted as net retained spending.
- Invoice times do not necessarily equal online checkout times; revenue by weekday is not normalized by the count of observed calendar dates.
- Exact duplicate rows cannot be conclusively identified as genuine duplicate-entry errors without invoice-line identifiers.
- Revenue is not profit; the dataset does not establish margins, inventory costs, customer motivations or the impact of proposed actions.

## Recommendations for further investigation

- Compare high-volume products with high-revenue products and, where available, gross margins before changing stocking priorities.
- Explore customer segmentation and cohort-based retention analysis to identify where loyalty initiatives may help.
- Assess profitability, logistics and demand in the strongest non-UK markets before pursuing expansion.
- Verify invoice-timing patterns against order volumes and operations data before adjusting staffing.

## Repository contents

```text
online-retail-analysis/
├── README.md
├── retail_analysis.ipynb
├── requirements.txt
└── .gitignore
```

## Attribution

Dataset: **Online Retail**, UCI Machine Learning Repository. Analysis and visualizations were prepared as an independent Python data analytics portfolio project.
