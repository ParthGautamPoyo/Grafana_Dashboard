# Grafana_Dashboard
# Project Overview
This project focuses on creating a dynamic dashboard for vehicle sales and fleet management, providing insights on key metrics like vehicle condition, odometer readings, sales trends, and customer preferences. The dashboard visualizes real-time data, enabling businesses to monitor vehicle performance, identify market trends, and optimize inventory and pricing strategies. It helps managers make data-driven decisions to improve operational efficiency, enhance customer satisfaction, and respond swiftly to market fluctuations. The dashboard supports strategic planning for maintenance, sales, and marketing, maximizing business outcomes.

# Data Overview
### Source and Scope  
The dataset represents a car sales record collected recently, encompassing data from 256,229 entries. It is intended to analyze various factors influencing car sales, including pricing, condition, and other vehicle characteristics.  

### Attributes  
The dataset includes the following key features:  

1. **Year**: Year of manufacture.  
   - Range: 2014 to 2015 (based on a quick glance).  
   - Insight: Indicates the age of the vehicle, which impacts its market value.  

2. **Make**: Manufacturer of the car.  
   - Categories: Includes brands like Kia, BMW, Volvo, etc.  
   - Insight: Brand reputation affects demand and resale value.  

3. **Model**: Specific car model.  
   - Categories: Includes Sorento, 3 Series, S60, etc.  
   - Insight: Popular models may fetch higher prices.  

4. **Trim**: Variant or configuration of the model.  
   - Example: LX, 328i SULEV, T5.  
   - Insight: Higher trims generally have better features and resale value.  

5. **Body**: Body type of the vehicle.  
   - Categories: SUV, Sedan, etc.  
   - Insight: Different body types cater to specific consumer preferences.  

6. **Transmission**: Type of transmission system.  
   - Categories: Automatic, manual, etc.  
   - Insight: Automatic vehicles often command higher prices in specific markets.  

7. **VIN**: Vehicle Identification Number.  
   - Unique for each car.  

8. **State**: Location of the sale.  
   - Insight: Geographic trends may influence demand and pricing.  

9. **Condition**: Vehicle condition rating (numeric).  
   - Insight: Higher condition scores indicate better-maintained cars.  

10. **Odometer**: Mileage of the vehicle.  
    - Range: Varies from low to high mileage.  
    - Insight: Cars with lower mileage are generally priced higher.  

11. **Color**: Exterior color of the car.    

13. **Seller**: Selling entity.  
    - Categories: Includes manufacturers, lease companies, etc.  
    - Insight: Sellers can influence consumer trust and pricing.  

14. **MMR (Manheim Market Report)**: Market value estimation of the car.  
    - Insight: Serves as a benchmark for pricing.  

15. **Selling Price**: Actual price at which the car was sold.  
    - Insight: Dependent on all other attributes.  

### Dataset Features  
- **Volume**: 256,229 rows.  
- **Missing Values**: Some columns like `make`, `model`, `trim`, `body`, `transmission`, etc., have missing values.  
- **Format**: CSV.  

# Data Ingestion Process
The data ingestion process was carefully designed to handle the large dataset and transform it into a time-series format suitable for InfluxDB. Below are the steps in detail:

**Step 1**: Data Preprocessing
**Header Standardization:**
Column names were cleaned and converted to lowercase without spaces (e.g., Rainfall_mm → rainfall_mm).
**Feature Categorization:**
**Numerical Features:** year, condition, odometer, mmr, sellingprice.  
**Categorical Features:** make, model, trim, body, transmission, vin, state, color, seller.
**Datetime Formatting:**
Timestamps were generated for every row to align the dataset with InfluxDB's time-series requirements.
**Step 2:** Transformation to Line Protocol
InfluxDB requires data in a specific format called line protocol. A Python script (convertToinflux.py) was used to:

Convert each row into the format:
measurement,tag_key=tag_value field_key=field_value timestamp

This transformation ensured that numerical values were stored as fields, while categorical values were stored as tags.

**Step 3:** Loading into InfluxDB
**Telegraf Configuration:**
Telegraf was configured to read the transformed data file.
A custom configuration file (telegraf.conf) defined the input and output plugins.
**Data Validation:**
After ingestion, sample queries were run in InfluxDB to verify the data integrity.

# Dashboard Design
**Images**
---
![Screenshot from 2024-11-24 17-33-06](https://github.com/user-attachments/assets/aa463007-9ad9-42b3-abd3-4b6664c7fa85)
![Screenshot from 2024-11-24 17-33-24](https://github.com/user-attachments/assets/ecb01277-ddff-4e6a-b812-33b26f2aca4d)
![Screenshot from 2024-11-24 17-33-32](https://github.com/user-attachments/assets/5103ba34-30f4-4fec-9687-ccd214a2b5c7)
![Screenshot from 2024-11-24 17-33-37](https://github.com/user-attachments/assets/7d141f86-c489-42bf-83b2-2cff6e17e2a8)
---
**Video**
---
[![Grafana Dashboard on Vehicle Sales Data](https://img.youtube.com/vi/x7Lw6onYAMg/0.jpg)](https://www.youtube.com/watch?v=x7Lw6onYAMg "Grafana Dashboard on Vehicle Sales Data")
---

### **Key Questions Addressed**
The Grafana dashboard was designed to answer the following insightful questions about the dataset:

---

### **Average Vehicle Condition Over Time**
- **What is the average condition of vehicles over time?**
  - **Visualization:** Line graph showing the time-series trend of average vehicle condition.
- **Are there any sudden drops or improvements in vehicle conditions?**
  - **Visualization:** Real-time trend analysis to detect anomalies or changes.

---

### **Average Odometer Reading Over Time**
- **How does the average odometer reading of vehicles change over time?**
  - **Visualization:** Line graph showing the streaming trend of odometer readings.
- **Are there specific time periods when vehicles with higher mileage are more common?**
  - **Visualization:** Time-series plot showing peaks and troughs.

---

### **Vehicles Sold Based on Color**
- **Which vehicle colors are the most and least popular among buyers?**
  - **Visualization:** Bar chart comparing the sales count by color.
- **Do certain colors have a consistent trend in sales or fluctuate over time?**
  - **Visualization:** Time-aggregated bar chart with dynamic updates.

---

### **Vehicles Sold by Transmission Type**
- **Which type of transmission (manual or automatic) is more popular among buyers?**
  - **Visualization:** Pie chart showing the distribution of sales by transmission type.
- **Is there a significant shift in demand for manual or automatic vehicles over time?**
  - **Visualization:** Streaming data with segmented comparison by transmission.

---

### **Average Selling Price by Make**
- **What is the average selling price for different vehicle makes?**
  - **Visualization:** Line or bar chart comparing average selling prices by make.
- **Do certain makes consistently sell at higher or lower prices?**
  - **Visualization:** Time-series trend of selling price averages for each make.

---

### **Vehicles Sold Based on Type of Body**
- **Which body type (e.g., SUV, sedan, hatchback) has the highest sales?**
  - **Visualization:** Pie chart or bar chart showing sales distribution by body type.
- **Are there seasonal or time-based trends in the sales of specific body types?**
  - **Visualization:** Time-series graph segmented by body type.

---

### **Total Vehicles Sold**
- **How many vehicles are sold in total over a given time period?**
  - **Visualization:** Gauge chart or real-time counter showing the cumulative total.
- **Are there identifiable peaks in sales that correlate with specific events or campaigns?**
  - **Visualization:** Time-series line chart overlaying sales and event markers.

---

### **Visualizations Implemented**
- **Line Graphs:** For analyzing trends in vehicle condition, odometer readings, and selling prices over time.  
- **Bar Charts:** For comparing the sales of vehicles by color, transmission, and body type.  
- **Pie Charts:** For visualizing the proportions of vehicle sales by transmission and body type.  
- **Gauge Charts:** For tracking the real-time total number of vehicles sold.  

# Additional Questions Considered
1. **How does the average fuel efficiency vary by make and model over time?**  
2. **What is the trend of average maintenance costs for vehicles based on condition?**  
3. **Which states consistently sell the most vehicles?**  
4. **Are there any correlations between vehicle price and odometer readings over time?**  
5. **What is the average time vehicles stay on the market before being sold?**  
6. **How does the average selling price differ between private and dealer sellers?**  
7. **What is the distribution of vehicle sales based on engine type (e.g., diesel, petrol, electric)?**  
8. **How frequently do specific vehicle models appear in sales data over a period?**  
9. **What is the average price fluctuation for vehicles within a specific transmission type?**  
10. **How does the demand for vehicles vary with seasonal or regional events (e.g., holidays, festivals)?**  

# Graphs included in the dashboard
Here are the corresponding queries for each chart title:  

### 1. **Average Vehicle Condition Over Time (Streaming Context)**  
**Query:**  
```sql
SELECT MEAN("condition") AS "Avg Condition" 
FROM "data" 
GROUP BY time(1m) 
FILL(null);
```

---

### 2. **Average Odometer Reading Over Time**  
**Query:**  
```sql
SELECT MEAN("odometer") AS "Avg Odometer" 
FROM "data" 
GROUP BY time(1m) 
FILL(null);
```

---

### 3. **Vehicles Sold Based on Color**  
**Query:**  
```sql
SELECT COUNT("selling_price") AS "Vehicles Sold" 
FROM "data" 
GROUP BY time(1m), "color" 
FILL(0);
```

---

### 4. **Vehicles Sold by Transmission Type**  
**Query:**  
```sql
SELECT COUNT("selling_price") AS "Vehicles Sold" 
FROM "data" 
GROUP BY time(1m), "transmission" 
FILL(0);
```

---

### 5. **Average Selling Price by Make**  
**Query:**  
```sql
SELECT MEAN("selling_price") AS "Avg Selling Price" 
FROM "data" 
GROUP BY time(1m), "make" 
FILL(null);
```

---

### 6. **Vehicles Sold Based on Type of Body**  
**Query:**  
```sql
SELECT COUNT("selling_price") AS "Vehicles Sold" 
FROM "data" 
GROUP BY time(1m), "body_type" 
FILL(0);
```

---

### 7. **Total Vehicles Sold**  
**Query:**  
```sql
SELECT COUNT("selling_price") AS "Total Vehicles Sold" 
FROM "data" 
GROUP BY time(1m) 
FILL(0);
```
### **Insights from the Dashboard**

---

#### **1. Average Vehicle Condition Over Time**
- **Average Vehicle Condition:** The line graph shows a steady trend in vehicle condition, suggesting that most vehicles are maintained at a consistent level of quality.
- **Sudden Changes:** Occasional dips indicate potential instances of older or poorly maintained vehicles entering the dataset.
- **Real-Time Monitoring:** The time-series trend highlights moments when overall condition metrics require attention, potentially aligning with specific operational or maintenance events.

---

#### **2. Average Odometer Reading Over Time**
- **Odometer Trends:** The line graph illustrates a gradual increase in average odometer readings, reflecting the usage patterns of vehicles over time.
- **Mileage Peaks:** Certain spikes in the graph may indicate the inclusion of high-mileage vehicles or seasonal trends where older vehicles are more prevalent.
- **Insights for Fleet Management:** Tracking this data helps identify when vehicles are nearing the end of their optimal performance lifecycle.

---

#### **3. Vehicles Sold Based on Color**
- **Color Preferences:** The bar chart reveals distinct trends in the popularity of specific vehicle colors. For example:
  - **Top-Selling Colors:** Certain colors dominate the market, indicating strong customer preference.
  - **Least Popular Colors:** These may represent opportunities for promotional strategies to boost sales.
- **Dynamic Fluctuations:** The streaming nature of the data enables businesses to adjust inventory in real-time based on color demand.

---

#### **4. Vehicles Sold by Transmission Type**
- **Transmission Popularity:** The pie chart shows the distribution of manual and automatic vehicles sold.
  - **Dominance of a Type:** A larger share of either transmission type highlights customer preference trends.
  - **Potential Shifts:** Real-time updates enable quick responses to changing preferences in the market.
- **Strategic Stocking:** Insights from this data can inform dealerships about which transmission types to prioritize.

---

#### **5. Average Selling Price by Make**
- **Price Trends by Make:** The bar chart provides insights into the average selling price for various vehicle brands:
  - **Premium Makes:** Certain brands consistently sell at higher prices, indicating a perception of luxury or quality.
  - **Budget-Friendly Makes:** Lower average prices may align with brands catering to cost-conscious customers.
- **Time-Based Insights:** Monitoring changes in selling prices over time helps identify seasonal demand or promotional effects.

---

#### **6. Vehicles Sold Based on Type of Body**
- **Body Type Distribution:** The pie chart highlights customer preferences for different body types (e.g., SUV, sedan, hatchback).
  - **Dominant Types:** The most popular body types point to market demand trends.
  - **Lesser-Preferred Types:** These may require targeted marketing campaigns to increase sales.
- **Insights for Product Development:** This data informs manufacturers and dealerships about shifting preferences for vehicle body styles.

---

#### **7. Total Vehicles Sold**
- **Cumulative Sales:** The gauge chart tracks the real-time total of vehicles sold:
  - **Performance Peaks:** Sudden increases may align with promotional events or seasonal trends.
  - **Strategic Planning:** Understanding sales patterns aids in aligning production and inventory with demand.

---

### **General Insights**
- **Actionable Trends:** The dashboard enables stakeholders to track real-time trends and make data-driven decisions regarding inventory, marketing, and sales.
- **Customer Preferences:** Insights into colors, body types, and transmission preferences guide targeted promotions and stock adjustments.
- **Operational Efficiency:** Tracking average condition and odometer readings supports proactive fleet maintenance and replacement planning.
- **Dynamic Decision-Making:** Streaming data visualization empowers businesses to respond swiftly to market fluctuations, optimizing operations and customer satisfaction.

### **Managerial Insights from the Dashboard**

---

#### **1. Real-Time Monitoring of Vehicle Metrics**
- **Dashboard Panels Tracking Metrics:** Average vehicle condition, odometer readings, and total vehicles sold are monitored in real time, enabling immediate feedback on performance and trends.
  
**Key Actionable Insight:**  
Managers can detect anomalies, such as sudden dips in condition or spikes in odometer readings, and address issues like maintenance backlogs or aging fleet concerns. Real-time tracking of sales empowers managers to adjust inventory or promotional strategies dynamically.

---

#### **2. Popularity of Vehicle Features**
- **Dashboard Visualization:** Charts highlighting vehicles sold by color, body type, and transmission preferences showcase customer trends.  

**Key Actionable Insight:**  
Inventory can be tailored to customer demand by prioritizing popular colors, body types, and transmission types. For example, dealerships could stock more vehicles in high-demand colors or offer incentives to shift less popular inventory.

---

#### **3. Pricing Strategy Optimization**
- **Dashboard Insight:** The average selling price by vehicle make reveals pricing trends and customer willingness to pay for different brands.  

**Key Actionable Insight:**  
Managers can set competitive pricing strategies based on the perceived value of each brand. Premium brands may justify higher prices, while budget-friendly brands can be used to attract cost-conscious customers. Dynamic pricing adjustments can also be tested in real-time to maximize revenue.

---

#### **4. Market Demand Analysis**
- **Dashboard Insight:** Vehicles sold by body type and transmission type provide insight into customer preferences for specific vehicle features.  

**Key Actionable Insight:**  
Targeted marketing campaigns can be developed for underperforming categories (e.g., promoting sedans if they lag behind SUVs in sales). Additionally, manufacturing and stocking decisions can align with the most popular features.

---

#### **5. Fleet Performance and Maintenance Planning**
- **Dashboard Insight:** Monitoring average vehicle condition and odometer readings helps track fleet wear and tear.  

**Key Actionable Insight:**  
Predictive maintenance can be scheduled to prevent downtime or costly repairs. Vehicles nearing high mileage thresholds can be flagged for replacement or decommissioning. This ensures operational efficiency and cost management.

---

#### **6. Sales Performance Evaluation**
- **Dashboard Visualization:** The total vehicles sold gauge provides an aggregated view of sales performance in real time.  

**Key Actionable Insight:**  
Managers can identify peak selling periods and allocate resources accordingly. Insights into underperforming timeframes may inform strategies like promotional events or targeted advertising campaigns.

---

#### **7. Resource Allocation Based on Insights**
- **Dashboard Utility:** By correlating real-time data, managers can allocate resources effectively across inventory, maintenance, and marketing efforts.  

**Key Actionable Insight:**  
Regions with high sales of specific body types or colors can be prioritized for additional inventory. Conversely, areas with low sales can receive promotional resources or discounts to boost demand.

---

#### **8. Customer Preference Analysis**
- **Dashboard Visualization:** Insights into transmission preferences and body type demand enable alignment with customer expectations.  

**Key Actionable Insight:**  
Dealerships can optimize their inventory mix based on evolving trends. For example, if automatic transmissions are gaining popularity, more automatic models can be stocked to meet market demand.

---

#### **9. Strategic Decision-Making Support**
- **Dashboard Integration:** Aggregated insights across metrics like condition, sales, and pricing provide a comprehensive view for strategic planning.  

**Key Actionable Insight:**  
Data-driven decisions, such as investing in high-demand vehicle features, optimizing pricing structures, and planning targeted campaigns, improve business outcomes. The dashboard supports long-term strategic goals by highlighting emerging trends and areas for improvement.

---

#### **10. Enhancing Customer Satisfaction**
- **Dashboard Insights:** Understanding trends in body types, colors, and pricing preferences ensures that customer needs are met.  

**Key Actionable Insight:**  
By aligning inventory and marketing with customer preferences, dealerships can enhance customer satisfaction and build loyalty. Offering promotions on preferred features can further strengthen the brand’s reputation.

---
