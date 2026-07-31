# Data

NHS England Referral to Treatment (RTT) waiting times. Provider-level aggregate
counts — no patient-level records.

Files are gzipped: the raw CSVs total ~1 GB, which is too large for git. They
compress about 25x because the extracts are sparse (121 columns, mostly zeros).

## `raw/`

Monthly full extracts, as published by NHS England.

| File | Period | Rows |
| --- | --- | --- |
| `20241231-RTT-December-2024-full-extract-revised.csv.gz` | Dec 2024 | ~188k |
| `20250131-RTT-January-2025-full-extract-revised.csv.gz` | Jan 2025 | ~188k |
| `20250228-RTT-February-2025-full-extract-revised.csv.gz` | Feb 2025 | ~188k |
| `20250331-RTT-March-2025-full-extract-revised.csv.gz` | Mar 2025 | ~188k |
| `20260131-RTT-January-2026-full-extract.csv.gz` | Jan 2026 | ~188k |

## `processed/`

Derived from `raw/` by the analysis. Included for convenience — they can be
rebuilt from the raw extracts.

| File | Rows | Columns |
| --- | --- | --- |
| `nhs_combined_4months.csv.gz` | 740,746 | 121 |
| `nhs_cleaned.csv.gz` | 204,849 | 112 |
| `final_nhs_analysis.csv.gz` | 204,849 | 112 |

## Reading them

`pandas` handles gzip natively — no need to decompress first:

```python
import pandas as pd

df = pd.read_csv("data/raw/20250131-RTT-January-2025-full-extract-revised.csv.gz")
```

To decompress on the command line:

```bash
gunzip -k data/raw/*.csv.gz
```

`-k` keeps the compressed copy.
