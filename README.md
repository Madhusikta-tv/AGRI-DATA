Source. Price records are drawn from Daily Prices of Market Yard Commodities in Telan-
gana (Agricultural Marketing and Co-operation Department, Government of Telangana,
2026), published under the Agriculture theme of the Telangana Open Data Portal (https:
//data.telangana.gov.in/search?theme=Agriculture) by the Agricultural Marketing and
Co-operation Department, Government of Telangana. The portal lists the dataset as covering
01-01-2014 to 30-06-2026 and reports, for every market yard and commodity in the state on
every trading day, the raw schema in Table 3. We use the subset of this feed for paddy (Grade-A
variety) from 2014 through 2025, described below.
Table 3: Raw column schema of the Telangana Open Data Portal mandi price feed (Agricultural
Marketing and Co-operation Department, Government of Telangana, 2026).
Column Meaning
DDate Date of the trading day
AmcCode Agricultural Market Committee (AMC) code
AmcName Agricultural Market Committee name
YardCode Agricultural market yard code
YardName Agricultural market yard name
CommCode Commodity code
CommName Commodity name
VarityCode Commodity variety code
VarityName Commodity variety name
Arrivals Quantity traded, in quintals (Qtls)
Minimum Minimum price per quintal (Rs)
Maximum Maximum price per quintal (Rs)
Modal Modal price per quintal (Rs): the price at which most transactions on that day took place
Filtering and harmonisation. We filter CommName to paddy and VarityName to Grade-A—
the most liquid single grade, which keeps the target a coherent product rather than a blend
of grades with different price dynamics. Column names and yard identifiers are mapped to
a canonical schema by regular-expression matching, since the portal’s per-period exports vary
slightly in header formatting. Modal is treated as the price of record throughout the paper, as it
best reflects where the bulk of trading actually clears (Minimum/Maximum bound the day’s range
but are thin-tailed and noisier); Arrivals is retained as a supply-side feature (§4.2). We select
the twelve AMCs with the most complete records and aggregate to one Modal value and one
summed Arrivals value per market per day (a market yard occasionally reports more than one
line for a day, e.g. across sub-lots). Eleven markets retain enough pre-2023 history to estimate
a stable training mean and are kept; the twelfth is dropped.
Weather. Weather is drawn from the NASA POWER daily agroclimatology archive (NASA
Langley Research Center, 2026), queried for temperature (maximum/minimum), bias-corrected
precipitation, mean relative humidity, wind speed and surface shortwave radiation, and merged
on date. POWER is a satellite- and reanalysis-derived product at roughly half-degree resolution;
we describe it as regional rather than gauge-level, and by default share one central Telangana
series across markets. Fill values are treated as missing and interpolated within a market.
