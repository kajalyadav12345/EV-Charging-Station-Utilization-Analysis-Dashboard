# EV-Charging-Station-Utilization-Analysis-Dashboard
_ _ _
📌 Project Overview

This Power BI dashboard analyzes Electric Vehicle (EV) charging station utilization, energy consumption, and revenue performance across multiple cities.
The goal is to help EV infrastructure companies optimize station operations, improve charger placement, and maximize revenue.
_ _ _

📊 Dataset Description

The dataset contains 100 rows of EV charging session records with details such as:

Station_ID – Unique ID for each station

City – Location of the charging station

Location_Lat / Location_Lon – GPS coordinates

Session_Start / Session_End – Start and end timestamps

kWh_Delivered – Energy delivered during the session

Price_per_kWh – Pricing for energy consumption

Payment_Method – Card / UPI / Cash

Charger_Type – Fast or Standard charger

Date, Hour, DayOfWeekName, MonthName – Derived for analysis

Session_Duration_Minutes / Hours  

_ _ _

### ** Transform Data in Power Query**
Add calculated columns:
```powerquery
// Extract Date only
DateOnly = DateTime.Date([Session_Start])

// Extract Hour
Hour = Time.Hour([Session_Start])

// Extract Day Name
DayOfWeekName = Date.DayOfWeekName([Session_Start])

// Extract Month Name
MonthName = Date.MonthName([Session_Start])

** Create Measures in DAX**
dax
Copy
Edit
// Total Sessions
Total Sessions = COUNTROWS(ev_charging_sample_100_enhanced)

// Total Energy Delivered
Total kWh = SUM(ev_charging_sample_100_enhanced[kWh_Delivered])

// Total Revenue
Total Revenue = SUM(ev_charging_sample_100_enhanced[Revenue])

// Average Session Duration (Minutes)
Avg Session Duration = AVERAGE(ev_charging_sample_100_enhanced[Session_Duration_Minutes])

// Utilization Rate (%) - assuming 24 hrs available
Utilization Rate = 
DIVIDE(
    SUM(ev_charging_sample_100_enhanced[Session_Duration_Hours]),
    COUNTROWS(DISTINCT(ev_charging_sample_100_enhanced[Date])) * 24
) * 100

_ _ _

💡 Key Insights from the Dashboard

Peak Usage Hours: Most charging occurs between 6 PM – 9 PM, indicating after-work EV charging habits.

Top Performing City: Bengaluru has the highest energy consumption and revenue.

Fast Chargers contribute to 65% of total revenue despite being fewer in number.

Weekend Traffic is higher, suggesting leisure travel impact.

Station Utilization Gaps in certain cities highlight opportunities for marketing or relocation.

Revenue – Calculated from kWh_Delivered × Price_per_kWh
