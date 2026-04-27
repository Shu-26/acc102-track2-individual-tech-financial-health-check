# ACC102 track2 Technology Sector Financial Health Check

A Python data product that helps everyday investors compare the financial performance of U.S. technology companies against their industry peers.

## 1. Problem & User

Ordinary investors often read financial statements without knowing whether a company's profitability, efficiency, leverage, or valuation is strong or weak relative to similar firms.  
This project is designed for **retail investors without advanced accounting knowledge**. It lets users select any firms within SIC 7370–7379, compares their financial ratios against the industry median, and presents the results in clear charts and plain‑English summaries.  
The product supports preliminary company evaluation and is not intended as direct investment advice.

## 2. Data

- **Source**: WRDS Compustat North America – Fundamentals Annual  
- **Date accessed**: 24 April 2026  
- **Industry filter**: SICH codes 7370–7379 (Computer Programming and Data Processing)  
- **Time range**: Fiscal years from 2018 onward  
- **Key variables**: Total assets (`at`), common equity (`ceq`), net income (`ni`), sales (`sale`), closing price (`prcc_f`), common shares outstanding (`csho`)  
- **Reliability note**: The dataset provides standardised, audited annual financial statements for hundreds of listed U.S. firms. Standard Compustat filters (`indfmt='INDL'`, `datafmt='STD'`, `consol='C'`, `popsrc='D'`) are applied to improve comparability.

## 3. Methods

The notebook implements a full pipeline from data acquisition to user‑facing output:

1. **Parameterised data download** – A `fetch_industry_data()` function uses an f‑string SQL query so that the SICH range and start year can be changed without rewriting SQL.
2. **Data cleaning** – Records with non‑positive equity are removed, and extreme ROE outliers are filtered.
3. **Ratio calculation** – Five indicators are computed: ROE, net profit margin, asset turnover, leverage, and price‑to‑book ratio.
4. **Industry benchmarking** – Annual sector medians are calculated for each ratio so that individual company performance can be compared against a representative benchmark.
5. **User‑driven selection** – In Step 6.1, the user only needs to edit a single `selected_tickers` list. All charts and summaries update automatically.
6. **Visualisation and commentary** – Outputs include time‑series line charts, year‑over‑year growth bar charts, a multi‑dimension radar chart, a P/B valuation snapshot, and a plain‑English investment summary.

## 4. Key Findings (Illustrative Test Case)

Using Microsoft (MSFT) and Alphabet (GOOGL) as test companies, the product shows:

- **Profitability**: Both firms consistently outperformed the industry median on ROE and net profit margin across most years.
- **Financial structure**: Their leverage ratios were generally below the benchmark, indicating conservative capital structures.
- **Growth**: Both companies showed positive year‑over‑year revenue and net income growth.
- **Valuation**: Both traded at a noticeable P/B premium relative to the sector median.

*These findings are automatically regenerated when the user changes the ticker list.*

## 5. How to Run

### Prerequisites
- A WRDS account with access to Compustat North America.
- Python 3.8 or later.
- The packages listed in `requirements.txt`.

### Setup
```bash
pip install -r requirements.txt
```

### Execution

1. Open `ACC102-individual work.ipynb` in Jupyter Notebook or JupyterLab.
2. Run the cells in order from top to bottom.
3. When prompted, enter your WRDS username and password.
4. After the download completes, a table of all available tickers in SIC 7370‑7379 is displayed.
5. Go to **Step 6.1**, change the `selected_tickers` list to the companies you want to compare (e.g., `['MSFT', 'GOOGL']`).
6. Re‑run all cells from Step 6.1 onward.
7. The notebook will display updated charts and auto‑generated summaries for your chosen companies.

> **Note**: The first data download may take 1–2 minutes. Subsequent runs can skip the download if the DataFrame is still in memory.

### Customisation

- To change the industry, modify the `sich_from` and `sich_to` parameters in Step 3.1.
- To change the time range, adjust the `start_year` parameter in Step 3.1 and the function definition in Step 2.

## 6. Product Link & Demo

- **GitHub Repository**: [https://github.com/Shu-26/acc102-track2-individual-tech-financial-health-check/blob/main/ACC102-individual%20work.ipynb]
- **Demo Video** : [https://video.xjtlu.edu.cn/Mediasite/MyMediasite/embedded/presentations/eb1eb5f755f0415aa93c4bbd6a68e2231d]

## 7. Limitations & Next Steps

- The analysis uses annual data only and does not capture quarterly fluctuations or intra‑year volatility.
- The industry sample is restricted to SICH 7370‑7379 and does not represent the entire U.S. technology sector.
- Valuation is assessed only through the P/B ratio; other multiples such as P/E or EV/EBITDA are not included.
- Industry classification may be imperfect, and outlier filtering can affect benchmark values.
- Future improvements could include broader industry coverage, quarterly data, additional valuation metrics, weighted medians by market capitalisation, and a simple Streamlit interface.
