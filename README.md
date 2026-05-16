# Global-EV-Sales-Dashboard

### Project Overview
As the automotive industry undergoes a massive shift toward sustainable energy, global stakeholders struggle to navigate highly fragmented data regarding Electric Vehicle (EV) adoption. This project provides a unified, interactive Power BI dashboard that synthesizes complex, multi-metric EV data to uncover actionable insights regarding regional market penetration, powertrain shifts, and energy consumption impacts.

### Business Objectives

- Architect a dynamic analytical tool** utilizing robust data modeling and explicit DAX measures to accurately process and visualize mixed-unit parameters (e.g., GWh, vehicle counts, percentages).
- Deliver an interactive visual narrative** empowering users to drill down into year-over-year global EV growth, regional dominance, and the transition between specific powertrains (BEV vs. PHEV).
- Transform raw categorical data into actionable insights** to help policymakers and energy providers optimize strategic planning for power grid capacity and charging infrastructure.

### Tech Stack
- Business Intelligence: Power BI
- Data Transformation: Power Query (ETL)
- Calculations: DAX (Data Analysis Expressions)

### Dataset Description
The analysis is based on the **IEA Global EV Data 2024** dataset. It includes both historical data and future projections (STEPS and APS) across various transport modes and technologies.
* `region`: Geographic region or country.
* `category`: Record type (Historical, Projection-STEPS, Projection-APS).
* `mode`: Transport mode (Cars, Buses, Vans, Trucks).
* `powertrain`: EV drivetrain type (BEV, PHEV, FCEV).
* `parameter`: The measured metric (stock, sales, electricity demand, charging points).
* `unit`: Unit of measurement (Vehicles, GWh, percent).

### Key Features & Dashboard Pages

#### 1. Overview & Regional Trends
* High-level KPIs tracking Total EV Sales, Stock, and Average Sales Share.
* Global heatmap highlighting the top 5 regions contributing to EV adoption.
* Year-over-year growth trendlines comparing developing vs. developed markets.

#### 2. Powertrain & Category Insights
* Deep dive into the distribution of Battery Electric Vehicles (BEV) vs. Plug-in Hybrid Electric Vehicles (PHEV).
* 100% Stacked bar charts showcasing powertrain adoption across passenger (Cars/Buses) and freight (Vans/Trucks) transport modes.
* Matrix visualizations revealing the dominant mode and powertrain combinations by region.

#### 3. Energy & Parameter Analysis
* Area charts tracking the evolution of EV energy consumption (Electricity demand in GWh) over time.
* Filtered visualizations ensuring strict unit separation (preventing the aggregation of incompatible metrics like GWh and vehicle counts).
* Correlation analysis between vehicle stock and new registrations.

### Key Insights & Conclusion

Exponential Growth: The data reveals a massive, uninterrupted upward trajectory in EV sales starting from 2020, with specific global regions acting as primary catalysts for adoption.
Powertrain Dominance: BEVs significantly outpace PHEVs in the passenger vehicle sector, indicating strong consumer confidence in fully electric technology.
Infrastructure Correlation: The rise in EV stock directly correlates with an escalating electricity demand, highlighting the urgent need for synchronized power grid upgrades and charging station deployments.

###  Future Scope

Automated Data Pipelines: Transitioning from a static CSV to an automated ETL pipeline connected to live global energy APIs.
Predictive Forecasting: Leveraging STEPS and APS projections to map out specific infrastructure bottlenecks leading up to 2035.
Geospatial Granularity: Expanding the data model to include city-level data for micro-analysis of charging station density.

### Key DAX Measures Implemented
To handle the mixed-unit nature of the `value` column, specific explicit DAX measures were created:
```DAX
Total EV Sales = 
CALCULATE(
    SUM('IEA Global EV Data'[value]), 
    'IEA Global EV Data'[parameter] = "EV sales", 
    'IEA Global EV Data'[unit] = "Vehicles"
)

Total Electricity Demand = 
CALCULATE(
    SUM('IEA Global EV Data'[value]), 
    'IEA Global EV Data'[parameter] = "Electricity demand",
    'IEA Global EV Data'[unit] = "GWh"
)
