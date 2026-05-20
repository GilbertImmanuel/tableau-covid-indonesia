# Indonesia COVID-19 Health Burden Dashboard 🇮🇩

An interactive, multi-page Tableau dashboard designed to analyze the spread, mortality risk, and healthcare burden of the COVID-19 pandemic across Indonesian provinces. 

This project goes beyond standard cumulative metrics by utilizing calculated fields, window averages, and spatial mapping to highlight specific provincial vulnerabilities, pandemic waves (e.g., Delta and Omicron), and daily infection intensity.

> **View the live interactive dashboard on Tableau Public:** [Click Here](https://public.tableau.com/views/IndonesiaCOVID_17792538866030/GeneralDashboard?:language=en-GB&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)

---

## 📊 Dashboard Structure & Features

The dashboard is split into two connected views, utilizing Tableau Dashboard Actions to allow users to drill down from a macro-national level to a micro-provincial level.

### Page 1: Executive Summary
Designed for high-level spatial and categorical filtering.
* **National Trend Line:** A temporal view of national COVID-19 surges.
* **Choropleth Province Map:** Spatial distribution of total cases across the archipelago. Acts as the primary navigational filter.
* **Mortality Risk (CFR) Ranking:** A horizontal bar chart ranking the Top 10 provinces by Case Fatality Rate (CFR). Includes a dynamic reference line showing the national average, with boolean color-coding for provinces exceeding the average risk.

### Page 2: Provincial Deep Dive
A granular, dynamic view that updates based on the province selected on Page 1.
* **Dynamic Header & KPIs:** Utilizes calculated fields to dynamically display the selected province's name (or "Indonesia Overview" if unselected) alongside precise MAX aggregations for Total Cases, CFR, and Recovery Rate.
* **7-Day Rolling Average (Dual-Axis):** An area chart showing the volume of new cases overlaid with a synchronized line chart for new deaths to visualize the lag between infection surges and mortality.
* **Active Cases Stacked Area Chart:** Maps the proportional distribution of Active Cases, Recoveries, and Deaths over time to illustrate the true concurrent burden on healthcare systems.
* **CFR vs. Recovery Rate Scatter Plot:** Plots the selected province against the national distribution to easily identify outliers in healthcare outcomes.
* **Calendar Heatmap:** A GitHub-style contribution matrix showing daily pandemic intensity. Includes an interactive slider to toggle between years (2020, 2021, 2022) to prevent visual clutter.

---

## 🗄️ Data Structure & Calculated Fields

The underlying dataset contains daily reporting metrics for Indonesian provinces (Date, Province, Island, New Cases, Total Cases, Total Deaths, Total Recovered). 

To power the visualizations, several custom calculated fields were engineered in Tableau:

* **Case Fatality Rate (CFR):** Calculated using the most recent reporting data to prevent cumulative inflation.
  `MAX([Total Deaths]) / MAX([Total Cases])`
* **Above Average CFR (Boolean):** Used for divergent color coding against a dynamic window average.
  `[CFR] >= WINDOW_AVG([CFR])`
* **Active Cases:** Isolates the current active burden from cumulative totals.
  `[Total Cases] - [Total Deaths] - [Total Recovered]`
* **Dynamic Header UI:** Prevents "wall of text" errors when no specific province is selected.
  `IF COUNTD([Province]) > 1 THEN "Indonesia Overview" ELSE ATTR([Province]) + " Overview" END`

---

## 🛠️ Tools & Technologies Used
* **Tableau Desktop / Tableau Public:** Data visualization, calculated fields, dashboard actions, layout containers.
* **Data Processing:** Aggregation of cumulative vs. daily metrics, spatial data mapping.
* **UI/UX Design:** Emphasis on high data-to-ink ratios, removal of default gridlines/borders, and synchronized color palettes (Red for intensity/risk, Grey for baselines/averages).

---

## 📸 Screenshots


**Executive Summary:**
![Executive Summary](images\ExecutiveSummary.png)

**Provincial Deep Dive (Filtered to DKI Jakarta):**
![Provincial Deep Dive](images\ProvincialDeepDive.png)