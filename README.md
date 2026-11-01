# 72-hour heating outlook for nine U.S. cities

A small open dataset of how much heating the next 72 hours are forecast to need in nine U.S. cities,
calculated from official National Weather Service (NWS) forecasts. One file per day, one row per city.

Published by [HeatCool Link](https://servoya.com/). The same numbers are shown, with the method, on
[servoya.com/heating-outlook](https://servoya.com/heating-outlook/).

## Cities

Birmingham AL, Columbus OH, Dallas TX, Huntsville AL, Louisville KY, Memphis TN, Miami FL, Nashville TN, Phoenix AZ.

## Files

- `data/latest.csv`: the most recent snapshot.
- `data/outlook-YYYY-MM-DD.csv`: one snapshot per day (date in UTC).

## Columns

| column | meaning |
|---|---|
| `date_utc` | Date of the snapshot (UTC). |
| `city`, `state` | City and state abbreviation. |
| `window_start_utc`, `window_end_utc` | The 72-hour window, the same instants for every city. |
| `heating_degree_hours_f` | Sum over the window of max(65 - temperature, 0) x hours, in degrees Fahrenheit x hours. Empty unless all 72 hours are covered. |
| `cooling_degree_hours_f` | Sum over the window of max(temperature - 65, 0) x hours. Empty unless all 72 hours are covered. |
| `coldest_forecast_f`, `warmest_forecast_f` | Coldest and warmest forecast temperature inside the window. |
| `covered_hours` | Hours of the window covered by NWS forecast periods (72 means complete). |
| `status` | `complete` when all 72 hours are covered, otherwise `unavailable`. |
| `nws_forecast_url` | The NWS forecast the row was calculated from. |

## Method

Each NWS day or night forecast temperature is held constant over its period and clipped to the window.
The base temperature is 65 F. Missing time is never filled in, and a city with gaps gets empty totals
instead of a guess. NWS day and night values are generally highs and lows, so the totals are coarse
period-based figures, not hourly measurements. The forecasts are for one point per city, not every
neighborhood, and the dataset says nothing about energy use or equipment.

## Source and license

Forecasts: National Weather Service (api.weather.gov), a U.S. government work in the public domain.
The compiled dataset is released under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/):
use it however you like and credit "HeatCool Link, servoya.com/heating-outlook".
