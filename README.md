
# Road accident Analysis

## Table of Contents
- [Project Overview](https://github.com/Tr0z3nAk/Road-Accident-Power-BI#overview)
- [Client Requirements](https://github.com/Tr0z3nAk/Road-Accident-Power-BI#client-requirements)
- [Analysis](https://github.com/Tr0z3nAk/Road-Accident-Power-BI#data-analysis)
- [Insights](https://github.com/Tr0z3nAk/Road-Accident-Power-BI#insights)
- [Recommendations](https://github.com/Tr0z3nAk/Road-Accident-Power-BI#recommendations)

## Overview
This analysis has done by Power BI independently.
One of the key objectives in accident data analysis to identify the main factors associated with road, weather, vehicle and Day/Night. By analyzing various aspects of the accident data, we seek to identify trends, make data-driven recommendations, and gain a deeper understanding.


![Road accident](https://github.com/Tr0z3nAk/Road-Accident-Power-BI/assets/140951166/c707fa8f-7a3b-4268-b150-f502f77283cb)



## Client Requirements
clients wants to create a Road Accident Dashboard for year 2022 and 2023 so that they can have insight on the below requirements:

- Primary KPI-Total Casualties and Total Accident values for Current Year and YoY growth
- Primary KP's- Total Casualties by Accident Severity for Current Year and YoY growth
- Secondary KPY's -Total Casualties with respectto vehicle type for Current Year
- Monthly trend showing comparison of casualties for Current Year and Previous Year
- Casualties by Road Type for Current year
- Current Year Casualties by Area/Location &by Day/ Night
- Total Casualties and Total Accidents by Location

## Data source
source: The primary dataset used for this analysis is the "Road Accident Data.xlsx" file, containing detailed information about two years (i.e. 2022 & 2023) accident records of United Kingdom.

## Tools

- Microsoft Power BI (version: 2.122.1066.0)

## Data Cleaning/Preparation
In the initial data preparation phase, we performed the following tasks:

1. Data loading and inspection.
2. Handling missing values.
3. Data cleaning and formatting.

## Data Analysis

Before going to main analysis for a better understanding and simplification I've created a Calendar Table by taking reference from accident dates.

## Data Modeling

By going to `Model View`, created a realtionship between `Data` table and `Calendar` table.

### Primary KPI
* **Total Casualties and Total Accident values for Current Year and YoY growth:**


To calculate Total Casualties and accident for CY (Current year) I've used Time intelligence Function **TotalYTD()** to create measures CY Casualties and CY accidents

```
CY Casualties  = TOTALYTD(sum(Data[Number_of_Casualties]),'Calendar'[Date])
```

```
CY accidents = TOTALYTD(COUNT(Data[Accident_Index]),'Calendar'[Date])
```

To calculate YoY (Year on Year) growth, we've to calculate Previous Year Casualties and Previous Year accidents measures, Time intelligence Function **SAMEPERIODLASTYEAR()**

```
PY Casualties = CALCULATE(SUM(Data[Number_of_Casualties]),SAMEPERIODLASTYEAR('Calendar'[Date]))
```
```
PY accident = CALCULATE(COUNT(Data[Accident_Index]),SAMEPERIODLASTYEAR('Calendar'[Date]))
```
YoY growth:
```
YoY Casualties = ([CY Casualities]-[PY Casualties])/[PY Casualties]
```
```
YoY Accident = ([CY accidents]-[PY accident])/[PY accident]
```
== formatting YoY to percentage to get the insight regarding CY vs PY Casualties and accidents ==

* **Total Casualties by Accident Severity for Current Year and YoY growth:**

To calculate total Casualties by Accident Severity, I've copied the `CY Casualties` to another Visual Card and taken the `Accidents Severity` column to Filter.
Same as for YoY growth.

By applying different Severity types in the filter get the Current Year total casualties and YoY growth by `Accident Severity`.

- [ ] Slight
- [x] Serious
- [ ] Fatal

### Secondary KPI
- **Total Casualties with respect to vehicle type for Current Year:**

By taking **multi row card** as KPI, inserted the `vehicle Type` and `CY casualties` in fields box to get the appropriate result.

For better Visualisation I've inserted pictures according to the vehicle type.

###

 **Monthly trend showing comparison of casualties for Current Year and Previous Year**

 I've used `Area Chart` to show the Monthly trend for Current Year and Previous Year.

 - Taken **Month** from `Calendar` table to **X-axis**.
- Taken **Total Number_of_Casualties** from `Data` table to **Y-axis**.
- Taken **Year(Date Hierarchy)** from `Calendar` Table to **Legend**.

#

**Casualties by Road Type for Current year**

Used `Clustered Bar Chart` to show this Visualisation.

- Taken **X-axis** as `CY casualties`.
- Taken ** Y-axis** as `Road_Type`.

#
**Current Year Casualties by Area/Location &by Day/ Night**

Used `Donut Chart` to Visualise CY Casualities by **Area Type** and **Day/Night**

- For Area Type Current year casualties
   
    Legend : `Area Type`(Urban/Rural)
 
    Values: `CY Casualities`

- For Day/Night Current Year Casualities

    Legend: `Light Condition`

    Values: `CY Casualities`

**For adding more details to the Visualisation**

Used two `Slicer` 
1. Road Surface Condition 
2. Weather Condition

## Insights
- According to the analysis Current Year casualties are lesser by **12%** from Previous year casualties. And same for accident cases as well lesser than **11.7%** from Previous year accidents.
- Current year accident Severities percentages are also lesser than Previous year accident Severities. 
    
    Severities types are **Slight**, **Serious** and **Fatal** lesser by **10.6%**, **16.2%** and **33.3%** respectively.
- Number of casualties are so much due to **Cars**.
    
         Casualties due to vehicle types are in following sequence:
         
         Car > Goods-Carrier > Bike > Bus > Others > Agricultural

- In both the year **November** is in peak at Casualities, whereas **February** is lowest occured casualties for year 2022 and **January** is the lowest for 2023.

- If we look at Road types then because of **Single Carriageway** more casualties are there.

- According to analysis casualties are occured more at **Day** time and more at **Urban** areas as well.

## Recommendations
Based on the analysis, we recommend the following actions:
-  Convert all the **Single Carriageway** roads into **Double Carriageway road**.

- Deploy speed Limiter at high ways by which we can control the occurance of Casualities.
- Take Serious actions against traffic rule breakers as well as deploy traffic cops.
