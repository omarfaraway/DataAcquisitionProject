# Data Card — Historical Weather in the Grenoble Area

**Pair names:** [Omar FARHAT] — [Omar Fathi]

**Source:** Open-Meteo Historical Weather API

**Registered scope (M0):** Temperature, relative humidity, precipitation, wind speed and snow depth for Grenoble and nearby locations over two years.

### 1. Source
Open-Meteo Historical Weather API.

Endpoint: `https://archive-api.open-meteo.com/v1/archive`

### 2. Collection Method & Dates
Data was collected using Python (`requests`, `pandas`) through API requests for three geographic coordinates. The JSON responses were combined into a single dataset and stored in Parquet format.

Historical period: October 1, 2024 – September 30, 2026.
No pagination was required because the Open-Meteo API returned the requested hourly data for each location in a single response.

### 3. Scope & Size
52,560 hourly observations across three locations, with 17,520 observations per location:

- Grenoble (45.18, 5.72)
- Chamrousse (45.13, 5.88)
- Voiron (45.36, 5.59)

The M1 scope was revised from nearby weather stations to coordinate-based historical weather estimates.

### 4. Schema
| Column | Type | Description |
|---|---|---|
| time | datetime | Hourly timestamp |
| location | string | Geographic location |
| temperature_2m | float | Temperature (°C) |
| relative_humidity_2m | integer | Relative humidity (%) |
| precipitation | float | Precipitation (mm) |
| wind_speed_10m | float | Wind speed (km/h) |
| snow_depth | float | Snow depth (m) |

### 5. Data Quality & Limitations
No missing values, duplicate location-time observations, irregular hourly intervals or invalid non-negative measurements were detected. No rows were removed.

The data represents historical weather estimates for geographic coordinates rather than direct observations from physical weather stations. Results are limited to three locations and two years.

### 6. License / Terms of Service
Open-Meteo provides free API access for non-commercial and educational purposes. The weather data is licensed under Creative Commons Attribution 4.0 International (CC BY 4.0), which permits reuse and redistribution with proper attribution.

Data source: Open-Meteo (https://open-meteo.com/).

The collected data was cleaned, aggregated and analyzed for an academic project.

### 7. GDPR
The dataset contains meteorological variables, timestamps and geographic locations only. It does not contain personal data or identifiable individuals.
