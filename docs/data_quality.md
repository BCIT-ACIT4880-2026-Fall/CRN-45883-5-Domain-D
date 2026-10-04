# Confirmed Data Quality Issues

## Issue 1: FRED unreported month stored as a blank cell (missing value)

The October 2025 value is blank in all three FRED files we use. The date row exists, but the value after the comma is empty.

| File | Line | Raw content |
|---|---|---|
| `data/raw/IR2.csv` | 552 | `2025-10-01,` |
| `data/raw/IR3.csv` | 534 | `2025-10-01,` |
| `data/raw/IR4.csv` | 522 | `2025-10-01,` |

Line numbers count the header as line 1. Likely cause: the October 2025 federal government shutdown interrupted BLS data collection.

Impact on the join: the inner join still matches October 2025 (the row exists), so those 3 joined rows carry a NULL `price_index`. They must be handled in Deliverable 2, not treated as zero.

Older history shows the same pattern: in the early 1980s, two of every three months are blank (e.g. `IR2.csv` line 3, `1980-01-01,`), consistent with the index being published quarterly before going monthly. Our study window is not affected.

## Issue 2: Mixed units across the data

Values in the joined dataset are measured in incompatible units:

| Column | Source | Unit |
|---|---|---|
| `import_value_musd` | exh13 | Millions of US dollars (stated in exh13 row 4) |
| `price_index` | IR2, IR3, IR4 | Index, 2000 = 100 |

Within the FT-900 files the unit also changes by file and column: exh13 is in millions of dollars, while exh17 row 7 mixes thousands of barrels, thousands of barrels per day, thousands of dollars, and dollars per barrel in one sheet. Any analysis comparing these must convert or normalize first.

Note: the FT-900 exhibits contain no "D" suppressed cells, because they are published aggregates. Suppression appears only in detailed commodity by country data.

## Also observed (layout issues handled in the notebook)

exh13 is a report layout, not a table: year labels on their own rows (e.g. row 38 `2025`), summary rows mixed with months (row 39 `Jan. - Dec.`), revised months with an `(R)` suffix (row 55 `January (R)`), and empty placeholder rows for August to December 2026 (rows 62 to 66).