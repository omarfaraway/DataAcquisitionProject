# Data Card — Grenoble Area Weather

**Pair:** Omar FARHAT — Omar Fathi

### 1. Source & Collection (M1)
**Source:** Open-Meteo Historical Weather API (`https://archive-api.open-meteo.com/v1/archive`).

**Method:** Python (`requests`, `pandas`), JSON converted to Parquet; no pagination.

**Period:** 01/10/2024–30/09/2026.

**Scope:** 52,560 hourly records (17,520/location) from Grenoble (45.18, 5.72), Chamrousse (45.13, 5.88), and Voiron (45.36, 5.59). Coordinate-based estimates replaced the originally planned station observations.

### 2. Schema
| Column | Type / Unit |
|---|---|
| time, location | datetime, string |
| temperature_2m | float, °C |
| relative_humidity_2m | integer, % |
| precipitation | float, mm |
| wind_speed_10m | float, km/h |
| snow_depth | float, m |

### 3. Quality & Cleaning (M2)
| Check / Decision | Reason | Rows affected |
|---|---|---|
| Missing values | Completeness | 0 |
| Duplicate records | Uniqueness | 0 |
| Hourly continuity | Detect gaps | 0 |
| Invalid values | Physical validity | 0 |
| Keep plausible extremes | Preserve weather events | 0 removed |

**Result:** No rows removed (52,560 retained). Coverage is limited to three locations and two years; API values are historical estimates, not direct station observations.

### 4. Mining (M3)
**Unit:** Location-day (2,190 rows).

**Features:** Daily mean temperature, humidity, wind and snow depth; total daily precipitation.

**Method:** StandardScaler + K-Means, testing k = 2–6.

**Choice:** k = 2 (best silhouette score: 0.421).

**Clusters:** 0 — Cold and Snowy Days (235, mainly Chamrousse); 1 — Other Weather Conditions (1,955).

### 5. License & GDPR
**License:** CC BY 4.0 (attribution required).

**GDPR:** No personal or identifiable data.