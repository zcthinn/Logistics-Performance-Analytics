# Logistics Performance Analytics — Power BI Project

## 📌 Overview
This Power BI project analyzes end-to-end logistics operations for a delivery/freight network — covering **delivery performance, delay root causes, customer satisfaction, vehicle reliability, driver performance, and hub efficiency**. The dashboard is built across **6 report pages**, all cross-filterable by **Year**, and designed to help operations leadership identify where delays originate and prioritize corrective action.

**Scale of data:** 27,979 total orders | 45 vehicles | 55 drivers | 6 hubs

---

## 🗂️ Report Pages

### 1. Delivery Performance
High-level KPI overview of order fulfillment.
- **KPIs:** Total Orders (27,979), Total Delivered (27,727), Not Successfully Delivered (252), Delay Rate (21%), Avg Satisfaction (4.17/5)
- **Visuals:** Delayed orders by month, on-time orders by month, delay count by issue category, delivery duration distribution, satisfaction split by delay status
- **Key finding:** 99.1% of orders were successfully delivered, but 21.1% experienced delays. Environmental Issues is the leading delay driver (30.2% of delayed orders).

### 2. Correlation of Delay and Customer Satisfaction Analysis
Quantifies the relationship between delays and customer experience.
- **KPIs:** Count of Delayed Orders (5,908), Delay–Satisfaction Correlation (**-0.74**), Avg Satisfaction (4.17), Avg Satisfaction When Delayed (2.94), Avg Satisfaction When On-Time (4.50)
- **Visuals:** Satisfaction gauge, satisfaction score bands ("Very Good/Good" vs "Normal/Poor/Very Poor") by delivery days, satisfaction split donut
- **Key finding:** A strong negative correlation (-0.74) confirms longer delays are closely tied to lower satisfaction — a 1.56-point satisfaction gap between delayed (2.94) and on-time (4.50) orders.

### 3. Reason of Not Successful Delivery & Reason of Delay Analysis
Root-cause breakdown of delay/failure reasons.
- **KPIs:** Total Orders, Delayed Count (5,908), Not Successfully Delivered (252), Most Common Issue Category (Environmental Issues), Most Common Reason (Vehicle Breakdown)
- **Visuals:** Decomposition tree (Issue Category → Description), delay reason trend, delay reasons by quarter (stacked bar)
- **Key finding:** Environmental Issues (road construction, severe weather, traffic congestion) account for 30.2% of delays; Vehicle Breakdown is the single largest individual reason (10.5%).

### 4. Vehicle Analysis
Fleet-level reliability and breakdown analysis.
- **KPIs:** Total Vehicles (45), Total Breakdowns (537), Most Breakdown-Prone Vehicle (FT-010), Most-Used Vehicle Type (Van)
- **Visuals:** Orders vs. breakdowns by vehicle type, breakdowns by purchase year, per-vehicle order/breakdown trend
- **Key finding:** Vans account for ~64% of categorized breakdowns (312 of 485), followed by Trucks (~23%). Vehicle FT-010 is the top individual breakdown offender. Four vehicles (FT-014, FT-024, FT-038, FT-042) show breakdowns but no associated orders in 2023–2024 — flagged as inactive/unutilized rather than true operational breakdowns.

### 5. Driver Performance Analysis
Evaluates driver-level delay behavior against rating and tenure.
- **KPIs:** Driver Count (55), Avg Orders/Driver 2023 (254.1), Avg Orders/Driver 2024 (254.6), Delay Rate by Driver (4%), Avg Driver Performance (3.58/5)
- **Visuals:** Delay rate by performance rating, delay rate per driver, delay by service year, experience vs. delay rate scatter
- **Key finding:** Overall driver delay rate is ~4% (moderate). Performance-rating-2 drivers have the highest delay rate (5%); the worst individual driver reaches 7%. Experience does not reliably reduce delays — rates hover between 3–6% regardless of tenure.

### 6. Hub Performance Analysis
Compares the 6 distribution hubs on load and delay performance.
- **KPIs:** Hub Count (6), Avg Hub Capacity (230), Delay Rate by Hub (4.26%), Most Overloaded Hub (Dallas Main Hub)
- **Visuals:** Delay % by hub, capacity vs. delay scatter, hub load/delay trend, capacity vs. total orders by hub
- **Key finding:** Houston Hub is the best performer (4.10% delay, 6.9K orders). Fort Worth (4.49%) and Austin (4.48%) have the highest delay rates. Dallas Main Hub is the most overloaded relative to capacity (7.3K orders vs. 250 capacity) and should be monitored closely.

---

## 📊 Core Metrics & Data Model (inferred)
| Entity | Fields Observed |
|---|---|
| **Orders (Fact)** | OrderID, IsDelayed, IsSuccessDelivery, DeliveryDays, Month/Quarter, Year |
| **Delay Reasons** | DelayReasonID, IssueCategory, Description (e.g., Road Construction, Severe Weather, Traffic Congestion, Vehicle Breakdown) |
| **Customer Satisfaction** | Satisfaction Score (1–5 scale), linked to IsDelayed |
| **Vehicles** | VehicleID (FT-xxx), VehicleType (Van, Truck, Pickup, Box Truck), Breakdown count, Purchase Year |
| **Drivers** | DriverID, DriverName, Performance Rating (1–5), Years of Service, Delay Rate |
| **Hubs** | HubID, HubName, Hub Capacity, Hub Load %, Delay % |

---

## 🎯 Key Business Insights
1. **Delay rate is 21.1%** overall — the single biggest lever for improving customer satisfaction, given the -0.74 correlation between delay and satisfaction.
2. **Environmental factors** (weather, traffic, road construction) are the top delay category, but **Vehicle Breakdown** is the top *individual* cause — pointing to a preventive maintenance opportunity.
3. **Vans** drive the majority of fleet breakdowns despite being the most-used vehicle type — prioritize preventive maintenance here.
4. **Driver experience alone doesn't reduce delays** — coaching should target specific underperforming drivers (rating 2, or individual delay rates >5%) rather than broad tenure-based programs.
5. **Dallas Main Hub is over capacity** relative to its throughput and should be reviewed for load balancing, while **Houston Hub** offers a benchmark for handling high volume with low delays.

---

## 🛠️ Tools & Techniques Used
- **Power BI Desktop** — data modeling, DAX measures, report design
- **DAX** — KPI cards (Delay Rate %, Avg Satisfaction, Correlation, etc.), calculated measures for on-time/delayed splits
- **Visuals used:** Line charts, clustered/stacked bar charts, donut charts, gauges, scatter plots, decomposition tree, KPI cards
- **Interactivity:** Year slicer, cross-page filtering (IssueCategory, Description drill-through on Page 3)

---

## 🚀 Recommended Next Steps
- Investigate root causes of Fort Worth & Austin hub delay rates (4.48–4.49%)
- Launch a preventive maintenance audit for the Van fleet, prioritizing vehicle FT-010
- Reassess Dallas Main Hub's capacity allocation vs. order volume
- Build a driver coaching program targeting individual delay-rate outliers (>5%)
- Verify status of inactive vehicles (FT-014, FT-024, FT-038, FT-042) before returning to service
