# Nigeria Real Estate Market Analysis (Power BI)

An interactive Power BI dashboard exploring property prices, listings, locations and market patterns across Nigeria, built from 24,326 property listings.

![Dashboard preview](BI%20DASHBOARD.png)

## Project Goal

To show how property supply and prices differ across Nigerian states, property types and price categories, and to highlight where the market is concentrated.

## Dataset

- Source:Kaggle
- Size: 24,326 listings
- Key columns:bedroom, bathroom, toilets, parking_space, title (property type), town, state, price, price_category, parking_space_category

## Tools Used

- PostgreSQL and pgAdmin (data storage and analysis)
- Power BI Desktop
- Power Query (data cleaning)
- DAX (measures and calculated columns)

## SQL Analysis (PostgreSQL)

The data was loaded into a PostgreSQL table (public.nigeria_real_estate) created in pgAdmin. SQL was used to calculate the findings reported in this project, and the table was then connected to Power BI for the dashboard.

## Data Cleaning

- Outlier detection: Sorting by price showed 9 listings priced from about NGN 42B up to NGN 1.8 trillion, which are not realistic for single properties (likely data entry errors).
- Handling: These rows were flagged as Suspected outlier with a Power Query conditional column (price above NGN 40B) and excluded from all price measures. They remain in the dataset for transparency.
- Effect: Average price fell from about NGN 301M to NGN 173M, and maximum price from NGN 1.8T to NGN 15B.
- Small samples: The average price by state chart only shows states with 100 or more listings, so low-volume states do not distort the ranking.


price_flag = if [price] > 40000000000 then "Suspected outlier" else "OK"


## Key DAX Measures

DAX
Avg Price = CALCULATE(AVERAGE('public nigeria_real_estate'[price]), 'public nigeria_real_estate'[price_flag] = "OK")

Median Price = CALCULATE(MEDIAN('public nigeria_real_estate'[price]), 'public nigeria_real_estate'[price_flag] = "OK")

Max Price = CALCULATE(MAX('public nigeria_real_estate'[price]), 'public nigeria_real_estate'[price_flag] = "OK")

Listing Count = COUNTROWS('public nigeria_real_estate')


Price categories: Low (under NGN 20M), Mid Range (NGN 20M and above), High (NGN 100M and above), Luxury (NGN 500M and above).

## Key Insights

- Lagos dominates supply: about 76% of all listings (18.4K of 24.3K).
- Abuja is the priciest state on average: NGN 203.86M, ahead of Lagos at NGN 181.47M.
- A few expensive listings pull the average up: the median (NGN 85M) is well below the average (NGN 173M).
- Mid-market heavy: about 88% of listings are Mid Range or High.
- Detached duplexes lead: about 57% of all listings.
- Ikoyi leads the top end: 6 of the 8 listings priced at NGN 10B and above.

## Dashboard Features

- KPI cards: total listings, average, median and maximum price
- Slicers for state and property type
- Listings by price category, parking spaces, state and property type
- Locations of properties priced at NGN 10B and above
- A separate Key Insights page

## Files

- Nigeria_Real_Estate_Market_Analysis.pbix: the Power BI report
- dashboard.png: dashboard screenshot

## Author

Nusirat | Aspiring data analyst
GitHub: [Nushirot](https://github.com/Nushirot)
