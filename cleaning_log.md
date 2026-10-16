# Cleaning Log: Deliverable 2 (Group 5, Domain D)

| Column | Problem found | Action taken | Statistic before | Statistic after | Handled by |
|---|---|---|---|---|---|
| 9 Census value and weight columns | Numbers stored as text (object dtype) | pd.to_numeric to int64 | dtype object; text max = 99999 | dtype int64; max = 52,665,639,215 | Janek Basi |
| month | Date stored as text YYYY-MM-01 | pd.to_datetime; dropped duplicate text column census_time | dtype object | dtype datetime64 | Janek Basi |
| country | Upper-case text, untrimmed | .str.strip().str.title() | top: TOTAL FOR ALL COUNTRIES | top: Total For All Countries | Janek Basi |
| enduse_desc | Upper-case text, untrimmed | .str.strip().str.title() | top: ARTWORK, ANTIQUES, STAMPS, ETC. | top: Artwork, Antiques, Stamps, Etc. | Janek Basi |
| (all rows) | Possible duplicate rows | drop_duplicates on cty_code + enduse_code + month | 0 duplicates | 0 duplicates | Janek Basi |
| cty_code | All-country total row labelled DET (double counts) | Dropped rows with cty_code '-' | 3,795 total rows; Mar 2025 DET sum $472.38bn | 0 total rows; Mar 2025 DET sum $236.19bn | Janek Basi |
| summary_level / cty_code | Region and trade-bloc rows (CGP) double count countries | Kept DET rows only | 70,342 CGP rows; sum/official up to 5.095x | 0 CGP rows; sum/official = 1.000 | Janek Basi |
| all value columns | Year-to-date phantom rows: every monthly measure = 0 | Dropped rows where all 9 measures are 0 | 101,375 all-zero rows | 0 all-zero rows | Janek Basi |
| air_weight_kg | Air value > 0 but weight 0 kg (rounded below 1 kg) | Set to NaN (handled in Part 3) | 2,521 impossible zeros | 2,521 NaN | Janek Basi |
| vessel_weight_kg | Vessel value > 0 but weight 0 kg | Set to NaN (handled in Part 3) | 113 impossible zeros | 113 NaN | Janek Basi |
| country | Census-specific names (inverted, abbreviated, outdated) | Mapped 10 names to standard short names | e.g. 'Korea, South', 'Burma', 'St Lucia' | 'South Korea', 'Myanmar', 'Saint Lucia' | Janek Basi |
| last_update, commodity_level, summary_level | Constant columns (1 unique value each) | Dropped | nunique = 1, 1, 1 | columns removed | Janek Basi |
| price_index | Blank FRED value for Oct 2025 (MAR on month) | Linear interpolation within each series | 5,066 missing | 0 missing | Priyanshu Batra |
| air_weight_kg | Weight under 0.5 kg recorded as 0 (MNAR) | NaN indicator column + fill 0.5 kg | 2,521 missing | 0 missing; indicator kept | Priyanshu Batra |
| vessel_weight_kg | Weight under 0.5 kg recorded as 0 (MNAR) | NaN indicator column + fill 0.5 kg | 113 missing | 0 missing; indicator kept | Priyanshu Batra |
| calculated_duty_usd | Duty > goods value before 2025 (entry error) | Dropped row; 2025-26 cases kept as real | 1 impossible row(s); 277,593 rows | 0 impossible rows; 277,592 rows | Priyanshu Batra |
| import_value_usd | Very large flows (IQR outliers) | Flag column is_outlier_import_value; values unchanged | max $28,248,952,016 | max unchanged; 48,270 rows flagged | Priyanshu Batra |
| air_weight_kg | Extreme bulk shipping weights | Capped at IQR upper bound 32,510 kg | max 36,887,199 kg | max 32,510 kg (46,845 rows capped) | Priyanshu Batra |
| vessel_weight_kg | Extreme bulk shipping weights | Capped at IQR upper bound 325,818 kg | max 556,279,814 kg | max 325,818 kg (50,782 rows capped) | Priyanshu Batra |
| air_value_usd | Skewness 51.96 | Kept log transform as air_value_usd_log | skew 51.96 | skew -0.88 | Jashanpreet Singh |
| import_value_usd | Skewness 24.70 | Kept log transform as import_value_usd_log | skew 24.70 | skew -0.01 | Jashanpreet Singh |
| consumption_value_usd | Skewness 23.87 | Kept log transform as consumption_value_usd_log | skew 23.87 | skew -0.04 | Jashanpreet Singh |
| calculated_duty_usd | Skewness 22.99 | Kept log transform as calculated_duty_usd_log | skew 22.99 | skew -0.12 | Jashanpreet Singh |
| dutiable_value_usd | Skewness 20.18 | Kept log transform as dutiable_value_usd_log | skew 20.18 | skew -0.42 | Jashanpreet Singh |
| vessel_value_usd | Skewness 18.79 | Kept log transform as vessel_value_usd_log | skew 18.79 | skew -0.41 | Jashanpreet Singh |
| container_value_usd | Skewness 17.18 | Kept log transform as container_value_usd_log | skew 17.18 | skew -0.37 | Jashanpreet Singh |
| air_weight_kg | Skewness 1.20 | Kept log transform as air_weight_kg_log | skew 1.20 | skew -0.51 | Jashanpreet Singh |
| vessel_weight_kg | Skewness 1.19 | Kept log transform as vessel_weight_kg_log | skew 1.19 | skew -0.39 | Jashanpreet Singh |
| *_log value columns | Different scales, outliers kept | Robust scaling (median, IQR) to *_robust | import_value_usd_log median 13.02 | median 0, IQR 1 | Jashanpreet Singh |
| price_index | Unscaled index, no outliers | Z-score to price_index_z | mean 104.01, std 8.94 | mean 0, std 1 | Jashanpreet Singh |
| effective_tariff_rate | New feature | Engineered (Part 6) | did not exist | 277,592 values; corr -0.036 | Jashanpreet Singh |
| tariff_shock_vs_2024 | New feature | Engineered (Part 6) | did not exist | 271,033 values; corr -0.018 | Jashanpreet Singh |
| import_price_yoy | New feature | Engineered (Part 6) | did not exist | 277,592 values; corr 0.040 | Jashanpreet Singh |
| import_value_lag1 | New feature | Engineered (Part 6) | did not exist | 272,629 values; corr 0.813 | Jashanpreet Singh |
| rolling_3m_prior_mean | New feature | Engineered (Part 6) | did not exist | 262,455 values; corr 0.859 | Jashanpreet Singh |
| supplier_share_lag1 | New feature | Engineered (Part 6) | did not exist | 272,629 values; corr 0.421 | Jashanpreet Singh |
| post_tariff_period | New feature | Engineered (Part 6) | did not exist | 277,592 values; corr -0.003 | Jashanpreet Singh |
| **DATASET SUMMARY** | Rows before: 453,105; rows after: 277,592 | Columns before: 21; columns after: 46 | Missing values before: 8,833 | Missing values after: 31,622 (feature NaNs where no earlier data exists; every imputed column is 0) | New features added: 7 |
