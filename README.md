# NYC Yellow Taxi Exploratory Data Analysis (January 2016)

**Author:** Muhammad Muneeb
**Project Category:** Data Analytics / Portfolio Project

---

## Executive Summary

This project presents a comprehensive Exploratory Data Analysis (EDA) of over 10.8 million New York City Yellow Taxi trip records from January 2016. By leveraging an optimized Python and Pandas data pipeline with Parquet storage chunking, this analysis extracts core operational metrics, passenger behaviors, pricing dynamics, traffic impacts, and revenue drivers. The resulting insights translate massive spatial-temporal datasets into actionable business recommendations regarding fleet allocation, surge pricing strategies, driver shift optimization, and payment processing infrastructure.

---

## Key Highlights & Core Discoveries

* **Solo Commuter Dominance:** Solo passengers accounted for 70.7% of all trips, indicating that the Yellow Cab functions primarily as a single-rider convenience service rather than a group transit option.
* **Operational "Sweet Spot":** The market is dominated by short urban hops, evidenced by a median trip duration of 10.4 minutes (mean: 12.9 minutes) and the vast majority of trips covering under 3 miles.
* **Digital Payment Supremacy:** Credit card transactions vastly outpaced cash payments, capturing roughly double the volume (~7.0 million credit transactions versus ~3.6 million cash transactions).
* **Traffic Congestion vs. Earnings:** Weekday business hours (9:00 AM–6:00 PM) experience significant traffic congestion, dropping average taxi speeds below 10–12 MPH. Consequently, the cost-per-mile increases to approximately $9.50–$10.00 due to meter time accrual.
* **Peak Revenue Window:** Fridays generate the highest revenue, accounting for 18.1% of the weekly total. Furthermore, the 6:00 PM to 7:00 PM window captures the highest market share by total revenue at 6.3%.

---

## Data Engineering & Optimization Pipeline

Processing approximately 10.9 million raw CSV rows (over 1.6 GB) on standard hardware necessitated memory optimization through columnar storage. The data was processed in chunks via PyArrow and converted into the Parquet format to significantly reduce file size and accelerate read times.

**Data Cleaning and Feature Engineering Procedures:**

* **Deduplication:** Eliminated all identical duplicate trip records.


* **Financial & Distance Filters:** Excluded non-positive fares and zero-or-negative trip distances to ensure baseline data validity.


* **Spatial Geofencing:** Restricted pickup and dropoff coordinates to valid NYC boundaries (Latitude: $40.50^\circ \text{N}$ to $40.90^\circ \text{N}$; Longitude: $-74.25^\circ \text{W}$ to $-73.70^\circ \text{W}$).


* **Datetime & Feature Engineering:** Calculated trip durations and average speeds, extracted granular temporal features (hour, day, weekend flags), and generated financial metrics such as cost-per-mile ($\frac{\text{Total Amount}}{\text{Trip Distance}}$). Date-mismatch and midnight anomalies were also removed to preserve data integrity.



---

## In-Depth Exploratory Data Analysis

### 1. Passenger Distribution

* **Single Passengers:** 70.7% of total trips.


* **Two Passengers:** 14.3% of total trips.


* **Five to Six Passengers:** 9.0% combined, reflecting a specialized demand for larger SUV or van taxis.



> **Business Insight:** The service caters overwhelmingly to individual daily commuters and business travelers.
> 
> 

### 2. Operational Dynamics (Duration & Traffic)

* **Median Trip Duration:** 10.4 minutes.


* **Mean Trip Duration:** 12.9 minutes.


* **Average City Speed:** ~18.35 MPH.


* **Average Cost per Mile:** $8.07.



> **Business Insight:** Traffic congestion heatmaps reveal an inverse correlation between operational speed and cost-per-mile. Weekday commuter blocks (9:00 AM–6:00 PM) see speeds drop to 10–12 MPH while cost-per-mile peaks at $9.50–$10.00. Conversely, early morning off-peak hours (12:00 AM–5:00 AM) allow speeds of 25–30 MPH, dropping the cost-per-mile to ~$6.50.
> 
> 

### 3. Temporal Demand & Revenue Trends

* **Busiest Days:** Friday leads with 18.0% of weekly trip volume and 18.1% of weekly revenue. Saturday follows closely with 15.0% of volume and 14.2% of revenue. Monday represents the slowest day, capturing only 11.8% of volume and 12.1% of revenue.


* **Peak Demand Hours:** The evening rush hour (6:00 PM–7:00 PM) sees peak volume at approximately 680,000 trips, while the 4:00 AM–5:00 AM trough drops to roughly 110,000 trips.



### 4. Vendor & Rate Code Economics

| Vendor Name | Technology Provider | Market Share (Trips) | Market Share (Revenue) |
| --- | --- | --- | --- |
| **Vendor 2** | VeriFone Inc. | 53.9%

 | 54.3%

 |
| **Vendor 1** | Creative Mobile Technologies | 46.1%

 | 45.7%

 |

**Rate Code Breakdown:**

* **Standard City Fare (Rate 1):** Comprises 97.7% of total trips with an average total of $14.26.


* **JFK Airport (Rate 2):** Comprises 2.0% of total trips. A distinct flat fare spike is visible at $52, averaging $64.57 when including tolls and tips.


* **Out-of-City/Special Rates:** Newark Airport (Rate 3) averages $90.04, and Negotiated Fares (Rate 5) average $76.51.



---

## Key Visualizations Summary

| Visualization | Primary Insight |
| --- | --- |
| **Passenger Count Distribution** | Strongly right-skewed, demonstrating that 70.7% of the market consists of single riders.

 |
| **Trip Duration Histogram (0–60 Min)** | Peak density occurs between 5–15 minutes with a sharp decline past 30 minutes.

 |
| **Payment Method Bar Chart** | Credit card usage is preferred over cash at a 2:1 ratio.

 |
| **Fare vs. Distance Scatter Plot** | Displays a clear linear drop rate accompanied by a horizontal pricing band at $52 for JFK airport trips.

 |
| **Day vs. Hour Congestion Heatmaps** | Illustrates the inverted correlation between speed and cost-per-mile during peak rush hours.

 |

---

## Business Recommendations

1. **Optimize Fleet Allocation:** Deploy maximum active fleet capacity between 5:00 PM and 8:00 PM on Thursdays and Fridays to capture the highest commuter demand and maximize revenue.


2. **Revise Driver Incentives:** Introduce targeted driver incentives during early morning hours (4:00 AM–6:00 AM), capitalizing on high traffic speeds that allow for faster trip completion and higher ride turnover.


3. **Prioritize Airport Hubs:** Maintain dedicated queue management and routing for airport trips (JFK and Newark), as these generate 4x–6x higher revenue per ride compared to standard city fares.


4. **Enhance Digital Payment Infrastructure:** Ensure flawless reliability of credit card terminals and digital processing, given that over 70% of the passenger base depends on cashless payment methods.



---

## Project Structure & Technology Stack

**Repository Assets:**

* **`NYC_EDA_Presentation_Slides.pdf`**: Executive slide deck presentation outlining visual findings.


* **`yellow_tripdata_2016-01.parquet`**: Optimized and chunk-processed Parquet dataset.


* **`EDA_NYC_Taxi.ipynb`**: Primary Jupyter Notebook containing the data pipeline, analysis, and modeling code.


* **Exported Visualizations**: Saved outputs including `trip_duration_distribution.png`, `fare_per_mile_heatmap.png`, and `average_speed_heatmap.png`.



**Technology Stack:**

* **Language:** Python 3.14+


* **Data Processing:** pandas, pyarrow


* **Data Visualization:** matplotlib, seaborn


* **Environment:** Jupyter Notebook / Anaconda
