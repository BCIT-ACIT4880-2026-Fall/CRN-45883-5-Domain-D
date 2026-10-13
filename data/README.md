# Data Sources

Raw data files are **not committed to this repository** (see `.gitignore`). They are stored as
attachments on GitHub Releases so the exact files we used are preserved, even though the
source URLs serve live data that changes over time.

| Release | Used for | Link |
|---|---|---|
| `data-v1` | Deliverable 1 | https://github.com/BCIT-ACIT4880-2026-Fall/CRN-45883-5-Domain-D/releases/tag/data-v1 |
| `data-v2` | Deliverable 2 onward | https://github.com/BCIT-ACIT4880-2026-Fall/CRN-45883-5-Domain-D/releases/tag/data-v2 |

To reproduce: download the files from the release and place them in `data/raw/`.

---

## data-v2 (current)

### 1. Census International Trade API: imports by end use and country

| Field | Value |
|---|---|
| File | `census_enduse_imports.csv` |
| Represents | US monthly imports by 5-digit end-use code and partner country |
| Source | US Census Bureau, International Trade API, endpoint `timeseries/intltrade/imports/enduse` |
| URL | `https://api.census.gov/data/timeseries/intltrade/imports/enduse` |
| Request parameters | `get=CTY_CODE,CTY_NAME,I_ENDUSE,I_ENDUSE_LDESC,GEN_VAL_MO,CON_VAL_MO,DUT_VAL_MO,CAL_DUT_MO,AIR_VAL_MO,VES_VAL_MO,CNT_VAL_MO,AIR_WGT_MO,VES_WGT_MO,SUMMARY_LVL,LAST_UPDATE&COMM_LVL=EU5&time=<YYYY-MM>&key=<redacted>`, one request per month |
| Date range | 2022-01 to 2026-07 (55 months) |
| Pulled | 2026-10-13 09:58:12 (local time, from census_enduse_pull_log.txt) |
| Size | 96,980,557 bytes (about 97 MB) |
| Rows | 866,182 (excluding header) |
| Pull record | `census_enduse_pull_log.txt` (same release): per-month row counts and timestamp |

### 2. FRED: Import Price Indexes by End Use (BLS)

Units: Index 2000 = 100, Not Seasonally Adjusted, monthly. Full history downloaded; filtered to the study window in the notebook.

| File | Series | URL | Pulled | Size | Rows |
|---|---|---|---|---|---|
| `IR2.csv` | Capital Goods, Except Automotive | https://fred.stlouisfed.org/graph/fredgraph.csv?id=IR2 | On or before 2026-09-29 | 9,417 bytes | 561 |
| `IR3.csv` | Automotive Vehicles, Parts and Engines | https://fred.stlouisfed.org/graph/fredgraph.csv?id=IR3 | On or before 2026-09-29 | 9,316 bytes | 543 |
| `IR4.csv` | Consumer Goods, Excluding Automotives | https://fred.stlouisfed.org/graph/fredgraph.csv?id=IR4 | On or before 2026-09-29 | 9,175 bytes | 531 |

Join pairing: end-use codes starting with 2 to IR2, with 3 to IR3, with 4 to IR4.

### What changed from v1 to v2, and why

The Deliverable 1 Census source was FT-900 Exhibit 13, a published aggregate with one row per
end-use category per month. Joined to FRED it produced only 57 rows, below the Domain D minimum
of 20,000. v2 replaces it with the Census API at end-use code x partner country x month grain,
extends the range back to January 2022 to give a pre-tariff baseline, and adds calculated duty
and dutiable value (needed to measure tariffs directly). The FRED files are unchanged.

---

## data-v1 (Deliverable 1, kept as evidence)

| File | Source | URL | Filters | Pulled | Size |
|---|---|---|---|---|---|
| `exh13.xlsx` | US Census FT-900, Exhibit 13 (July 2026 release): US trade in goods by principal end-use category | https://www.census.gov/ft900 | Part B, Not Seasonally Adjusted; imports; Jan 2025 to Jul 2026 | On or before 2026-09-29 | 246,823 bytes (70 rows x 10 columns, report layout) |
| `IR2.csv` | FRED IR2 | https://fred.stlouisfed.org/graph/fredgraph.csv?id=IR2 | Full history | On or before 2026-09-29 | 9,417 bytes, 561 rows |
| `IR3.csv` | FRED IR3 | https://fred.stlouisfed.org/graph/fredgraph.csv?id=IR3 | Full history | On or before 2026-09-29 | 9,316 bytes, 543 rows |
| `IR4.csv` | FRED IR4 | https://fred.stlouisfed.org/graph/fredgraph.csv?id=IR4 | Full history | On or before 2026-09-29 | 9,175 bytes, 531 rows |