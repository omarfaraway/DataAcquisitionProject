# EDA findings — Historical Weather Dataset

**Pair:** Omar FARHAT, Omar FATHI · **Dataset:** Open-Meteo Historical Weather API, Grenoble, Chamrousse and Voiron (October 2024 – September 2026) · **Date:** 12 November 2026

**Rows × columns:** 52,560 × 7 · **File:** `Results/weather_data.parquet` (Parquet)

---

## 1. Missingness

**Which columns, and how much?**

| Column | Missing | % | Sentinel |
|---|---:|---:|---|
| temperature_2m | 0 | 0% | None detected |
| relative_humidity_2m | 0 | 0% | None detected |
| precipitation | 0 | 0% | None detected |
| wind_speed_10m | 0 | 0% | None detected |
| snow_depth | 0 | 0% | None detected |

**Do they go missing together?**

No missing values were detected in any weather variable. Therefore, there are no rows with simultaneous missing values.

**What is the mechanism?**

No missingness mechanism was found because the dataset contains no detected missing values.

**MCAR, MAR or MNAR, and how do you know?**

Not applicable to the observed dataset because no missing values were detected. We cannot determine how missingness might occur in future API responses.

**Decision.**

Keep all rows. No imputation or removal is necessary. The dataset remains unchanged with 52,560 rows.

---

## 2. Distributions and outliers

**Per numeric column of interest:**

| Column | min | median | max | Impossible values | Ambiguous values |
|---|---:|---:|---:|---:|---:|
| temperature_2m (°C) | -15.0 | 10.3 | 38.7 | 0 detected | Not assessed |
| relative_humidity_2m (%) | 6 | 77 | 100 | 0 | Not assessed |
| precipitation (mm) | 0 | 0 | 15.7 | 0 | Not assessed |
| wind_speed_10m (km/h) | 0 | 3.7 | 31.1 | 0 | Not assessed |
| snow_depth (m) | 0 | 0 | 1.61 | 0 | Not assessed |

**Impossible** — violates the constraints of the data (a negative duration).

No physically invalid humidity, precipitation, wind speed or snow depth values were detected. The observed temperature range is plausible. No rows were removed.

**Extreme but plausible**.

The boxplots show potential outliers, especially for precipitation, wind speed and snow depth. These extreme values may represent real weather events, so we decided to keep them. The exact number of statistical outliers was not calculated.

**Ambiguous** — cannot be resolved from the file alone (a zero-distance trip).

Zero precipitation and zero snow depth are valid weather observations. We did not identify any confirmed ambiguous values, but we did not perform a separate ambiguity count.

**Shape.**

Temperature has a roughly bell-shaped distribution, with a mean of 10.90°C and a median of 10.3°C.

Precipitation and snow depth are strongly right-skewed, with many zero values and a few higher observations. Their medians are zero, while their means are positive.

For these variables, the median better describes a typical hourly observation, while the mean is influenced by occasional rain or snow.

---

## 3. Temporal patterns

**Range covered:**

The dataset covers October 1, 2024, to September 30, 2026, for Grenoble, Chamrousse and Voiron. This corresponds to two years of hourly weather observations.

**Gaps:**

No missing hourly timestamps were detected for the three locations. The dataset contains 17,520 hourly observations per location, for a total of 52,560 rows.

**Cycles:**

- **Hour-of-day:** Hourly measurements are available, but daily temperature cycles were not specifically analyzed.
- **Day-of-week:** No specific weekly pattern was investigated.
- **Seasonal:** Temperatures are generally higher in summer and lower in winter. Snow depth is higher during colder periods, especially in Chamrousse.

**Timezone:**

The exact timezone representation should be confirmed from the acquisition notebook or the timestamp metadata. The absence of gaps alone does not establish whether timestamps are timezone-aware or timezone-naive.


---

## 4. Representativeness

**Who or what is in this dataset?**

The dataset contains hourly historical weather data for three locations in the Grenoble area: Grenoble, Chamrousse and Voiron, from October 2024 to September 2026.

The data comes from the Open-Meteo Historical Weather API and includes temperature, humidity, precipitation, wind speed and snow depth.

**Who or what is missing?**

The dataset does not cover other cities or regions of France. It also does not include weather conditions outside the selected two-year period.

The data comes from a historical weather API rather than direct measurements from individual weather stations.

**One conclusion this data cannot support.**

"We identified the main weather patterns across all of France."

This conclusion would be incorrect because our dataset only covers three locations near Grenoble.

**Does more data fix it?**

Adding more observations from the same three locations would not solve the geographical coverage problem.

To make conclusions about all of France, we would need data from many other regions and different geographical environments.

## 5. What you need to do next

1. **Limited coverage** — Document the geographical limitations of our dataset.
2. **Different scales** — Standardize weather variables before clustering.
3. **Extreme values** — Keep plausible outliers, as they may represent real weather events.