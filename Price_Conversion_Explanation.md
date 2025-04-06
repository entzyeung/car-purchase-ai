# How I Converted the 1990s Car Evaluation Dataset Prices to 2025 UK Pounds

## Introduction

In my Car Purchase AI webapp, I needed to make the categorical price and maintenance cost data from the 1990s Car Evaluation Dataset more relatable to a 2025 UK audience. The dataset uses categories like `vhigh`, `high`, `med`, and `low` for both buying price and maintenance cost, but it doesn’t provide numerical values. My goal was to map these categories to approximate British Pounds (£) ranges that reflect typical used car prices and maintenance costs in the UK as of 2025, adjusted for inflation and market trends since the 1990s. Here’s how I did it.

## Step 1: Understanding the Dataset’s Categories

The Car Evaluation Dataset, sourced from the UCI Machine Learning Repository ([https://archive.ics.uci.edu/ml/datasets/Car+Evaluation](https://archive.ics.uci.edu/ml/datasets/Car+Evaluation)), uses four categories for `buying` (purchase price) and `maint` (maintenance cost): `vhigh`, `high`, `med`, and `low`. These are ordinal, meaning `vhigh` is the most expensive, followed by `high`, `med`, and `low`. Since the dataset is from the 1990s and doesn’t include numerical values, I had to infer what these categories might have meant in terms of 1990s prices before adjusting them to 2025.

## Step 2: Estimating 1990s Prices as a Baseline

To start, I needed a baseline of what used car prices and maintenance costs might have been in the UK during the 1990s:

- **Used Car Prices in the 1990s**: I estimated that a "low" price for a used car in the 1990s might have been around £1,000–£2,000, typical for an older, high-mileage car. A "medium" price might have been £3,000–£5,000, "high" around £6,000–£9,000, and "very high" around £10,000–£15,000, which would have been for nearly new or luxury models. These are rough guesses based on my understanding of the historical car market, as I don’t have exact data from that period.
- **Maintenance Costs in the 1990s**: For annual maintenance, I estimated a "low" cost at £100–£200 (basic servicing for a reliable car), "medium" at £300–£500, "high" at £600–£800, and "very high" at £1,000 or more (e.g., for luxury cars or those needing frequent repairs). Again, these are approximate figures based on general knowledge of car ownership costs at the time.

These 1990s estimates gave me a starting point to adjust for inflation and market changes over the 35 years from 1990 to 2025.

## Step 3: Adjusting for Inflation from 1990 to 2025

To bring these 1990s values into 2025, I needed to account for inflation, which increases the cost of goods and services over time. I used a general inflation rate for the UK, as I didn’t have car-specific inflation data for this period. Based on historical data from the Office for National Statistics (ONS) ([https://www.ons.gov.uk/economy/inflationandpriceindices](https://www.ons.gov.uk/economy/inflationandpriceindices)), the average annual inflation rate in the UK from 1990 to 2025 is roughly 2–3%. I chose an average rate of 2.5% for my calculations, as it balances general inflation trends.

I used the compound inflation formula to calculate the inflation factor over 35 years:

\[
\text{Future Value} = \text{Past Value} \times (1 + \text{average annual inflation rate})^{\text{number of years}}
\]

- **Number of years**: 1990 to 2025 = 35 years
- **Inflation factor**: \((1 + 0.025)^{35} \approx 2.36\)

This means prices in 2025 would be about 2.36 times higher than in 1990 due to inflation. Applying this to my 1990s estimates:

- **Used Car Prices**:
  - `low`: £1,000–£2,000 → £2,360–£4,720
  - `med`: £3,000–£5,000 → £7,080–£11,800
  - `high`: £6,000–£9,000 → £14,160–£21,240
  - `vhigh`: £10,000–£15,000 → £23,600–£35,400
- **Maintenance Costs**:
  - `low`: £100–£200 → £236–£472
  - `med`: £300–£500 → £708–£1,180
  - `high`: £600–£800 → £1,416–£1,888
  - `vhigh`: £1,000+ → £2,360+

These inflation-adjusted values gave me a rough idea of what the 1990s categories might look like in 2025, but I needed to refine them further based on current market trends.

## Step 4: Adjusting for 2025 Market Trends

Inflation alone isn’t enough, as the used car market in 2025 has been influenced by various factors like supply and demand, technological changes (e.g., electric vehicles), and economic conditions. I looked at recent data to get a sense of the 2025 UK used car market:

- **Used Car Prices in 2025**:
  - According to a report from Auto Trader ([https://www.autotrader.co.uk/content/market-insight/used-car-price-trends](https://www.autotrader.co.uk/content/market-insight/used-car-price-trends)), the average retail price of a used car in the UK in early 2025 was £16,774, with predictions of a slight increase in sales to 7.70 million in 2025 (up from 7.61 million in 2024). This suggests prices are stable or slightly rising due to high demand and a 3.1% year-on-year supply drop.
  - Another source, AM Online ([https://www.am-online.com/news/market-insight/used-car-prices-continue-to-rise-in-december-2024](https://www.am-online.com/news/market-insight/used-car-prices-continue-to-rise-in-december-2024)), reported an average used car price of £17,064 in December 2024, with older cars (10–15 years) at £6,532 and 15+ years at £5,516, while 1–3-year-old cars were £24,806.

The average used car price in the UK in 2025 is around £16,774–£17,064, with a range from £5,500 (older cars) to £24,800 (nearly new cars). My inflation-adjusted estimates (£2,360–£35,400) were in the ballpark but needed adjustment to fit this range:

- `low` (< £5,000): This aligns with older cars (e.g., £5,516 for 15+ years), so I set this as < £5,000 to capture the lower end of the market.
- `med` (£5,000–£10,000): This covers older but decent cars, fitting below the average price of £16,774.
- `high` (£10,000–£15,000): This is slightly below the average, representing mid-range used cars.
- `vhigh` (> £15,000): This captures the average and above, up to £24,800 for nearly new cars.

I rounded these ranges for simplicity and to reflect the categorical nature of the dataset, while ensuring they align with 2025 market data.

- **Maintenance Costs in 2025**:
  I didn’t have specific 2025 data for maintenance costs, but I estimated based on general knowledge of car ownership in the UK. A "low" maintenance cost in 2025 might be £300–£500 annually for a reliable car needing minimal servicing, while a "very high" cost might be £2,000+ for a luxury car or one with frequent repairs. My inflation-adjusted estimates (£236–£2,360+) were close, so I adjusted them to round numbers for user-friendliness:
  - `low` (< £500): Matches the lower end of modern maintenance costs.
  - `med` (£500–£1,000): Covers average maintenance for most cars.
  - `high` (£1,000–£2,000): For cars with higher upkeep.
  - `vhigh` (> £2,000): For luxury or high-maintenance vehicles.

## Step 5: Finalizing the Ranges

After combining the inflation adjustments and 2025 market trends, I settled on the following ranges for my webapp:

- **Buying Price**:
  - `vhigh`: > £15,000
  - `high`: £10,000–£15,000
  - `med`: £5,000–£10,000
  - `low`: < £5,000
- **Annual Maintenance Cost**:
  - `vhigh`: > £2,000
  - `high`: £1,000–£2,000
  - `med`: £500–£1,000
  - `low`: < £500

These ranges are approximate because the original dataset doesn’t provide numerical values, and the 2025 market data gives averages rather than categorical breakdowns. However, they reflect typical used car prices and maintenance costs in the UK in 2025, adjusted for inflation and market trends since the 1990s.

## Step 6: Limitations of My Approach

I should point out some limitations in my method:
- The 2.5% inflation rate I used is a general estimate for the UK, as I couldn’t find car-specific CPI data from 1990 to 2025. Car prices might have inflated at a different rate due to factors like technological advancements (e.g., electric vehicles) and market disruptions (e.g., post-COVID supply shortages).
- The 2025 market data I found provides average prices, not categorical ranges, so my mappings are interpretive.
- Regional variations in the UK and differences in car types (e.g., electric vs. petrol) could affect these ranges.

Despite these limitations, I believe these ranges provide a practical approximation for users of my app, balancing the historical context of the 1990s dataset with modern market realities in 2025. If I had access to more precise 1990s UK car price data or a car-specific CPI, I could refine these calculations further.