# Data Source Registration

All files are committed unmodified in `/data/raw/`.

## 1. US Census Foreign Trade Statistics: FT-900, Exhibit 13

| Field | Value |
|---|---|
| File | `data/raw/exh13.xlsx` |
| Source | U.S. International Trade in Goods and Services (FT-900), July 2026 release |
| URL | PASTE FT-900 URL HERE |
| Downloaded as | `ft900xlsx.zip` (all exhibits), exh13.xlsx extracted unmodified |
| Filters | Exhibit 13, Part B (Not Seasonally Adjusted), US Imports, end-use categories Capital Goods, Automotive Vehicles etc., Consumer Goods |
| Period used | January 2025 to July 2026 (19 months) |
| Unit | Millions of US dollars, Census basis |
| Pulled | On or before 2026-09-29 09:19 PDT (committed by Janek Basi, commit 6ef2772) |

## 2. FRED: Import Price Indexes by End Use (BLS)

Units: Index 2000=100, Not Seasonally Adjusted, monthly. Full history downloaded; filtering to the study window happens in the join, so the raw files stay untouched.

| File | Series | URL | Pulled |
|---|---|---|---|
| `data/raw/IR2.csv` | Import Price Index (End Use): Capital Goods, Except Automotive | https://fred.stlouisfed.org/graph/fredgraph.csv?id=IR2 | On or before 2026-09-29 09:48 PDT (committed by Jashanpreet Singh, commit 86f490d) |
| `data/raw/IR3.csv` | Import Price Index (End Use): Automotive Vehicles, Parts and Engines | https://fred.stlouisfed.org/graph/fredgraph.csv?id=IR3 | On or before 2026-09-29 09:48 PDT (committed by Jashanpreet Singh, commit 86f490d) |
| `data/raw/IR4.csv` | Import Price Index (End Use): Consumer Goods, Excluding Automotives | https://fred.stlouisfed.org/graph/fredgraph.csv?id=IR4 | On or before 2026-09-29 09:48 PDT (committed by Jashanpreet Singh, commit 86f490d) |

## Category pairing

| exh13 import column | FRED series |
|---|---|
| Capital Goods | IR2 |
| Automotive Vehicles, etc. | IR3 |
| Consumer Goods | IR4 |

## Pulled but not used

`exh6.xlsx`, `exh16.xlsx`, `exh17.xlsx`, `MCOILWTICO.csv`: explored during source selection, not part of the final join.