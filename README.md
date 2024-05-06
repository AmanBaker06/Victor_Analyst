# Victor_Analyst

# Covid-19 Report India 2020-21

## Problem Statement

This report analyzes the impact of the Covid-19 pandemic in India during 2020-21. The study comprises of three main components namely, Recorded Cases, Statewise Testing, and Vaccination Data for the given period. The report identifies the spread, mortality rate, and overall impact of the coronavirus in the country while highlighting the performance of the vaccination campaign in all the states. Distribution of Data has been done based on various parameters such as geographical and gender as well as yearly and monthly periods.

## Data Context (Please note)

The dataset contains three imported csv files and a new created table. All tables do not contain related data and primary key to connect with each other thus modelling has been done accordingly. The tables 
comprise of daily data and thus each row contains values continued from previous rows. Thus summing the columns will give inaccurate results. 
Use this snapshot for reference:
![Snap_1]!![image](https://github.com/AmanBaker06/Victor_Analyst/assets/168013894/ad55c466-098a-498f-ba7c-673b53624e84)

Thus proper measures and filters have been created to calculate proper total values. 

### Steps followed 
# ETL Process

- Step 1 : Load data into Power BI Desktop, dataset consists of three csv files. (StatewiseTestingDetails, Covid_19_cases, Statewise Vaccine)
- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 3 : Assigned first row as headers and changed data type of all coloumns accordingly.
- Step 4 : Filtered rows and removed null values from Positive and Negative Columns.
- Step 5 : In the Covid 19 Cases file the states column had numerous erroneous spelling of same states creating multiple categories. Replaced Values to convert them to proper names of the states leading to correct state categories.
- Step 6 : Removed Columns "ConfirmedIndianNational" and "ConfirmedForeginNational" as was needed for analysis.
- Step 7 : Opened Statewise Vaccine file and removed unnecessary columns.
- Step 8 : Unpivot the "Covaxin", "Covishield" and "Sputnik" Columns to create a new "Vaccine" and "DosebyVaccine" Columns. Done to visualize Doses administered by Vaccine.
- Step 9 : Unpivot the "MaleAdministered" & "FemaleAdministered" columns for gender wise analysis through visualization in page 5 (donut chart)
# Modelling and Calculations
- Step 9 : Connected "StatewiseTestingDetails" and "Covid_19_cases" table through Date column. Many-to-Many relationship with "Both" cross filtration.
- Step 10 : Created a new table with DAX to separate the total values of positive, negative cases and samples collected. To be used for specific visualizations like the card visualization on page-"(Drill)RegionalTests":
 "Total = SUMMARIZECOLUMNS(StatewiseTestingDetails[State],StatewiseTestingDetails[State (groups)],"totaposit",max(StatewiseTestingDetails[Positive]),"Totneg",max(StatewiseTestingDetails[Negative]),"TotSamp",max(StatewiseTestingDetails[TotalSamples]))"
- Step 11 : Connected "Total" and "StatewiseTestingDetails" tables through one-to-many relationship, "Both" cross filtration.
- Step 12 : Grouped States from "State/UnionTerritory" column by regions in the "Covid_19_cases" table for regionwise analysis.
- ![Snap_1]![image](https://github.com/AmanBaker06/Victor_Analyst/assets/168013894/3e0cf94e-dc79-419b-80c2-8e6cbb2d5a39)
- Step 13 : Created measure in "Covid_19_Cases" table named "Regiondeaths" calculating Deaths by new region group.
- Step 14 : Created measure named RegionTotalCases to take the last date value which is the final value for confirmed cases. Used for the analysis of region and statewise total confirmed cases. "RegionTotalCases = calculate(sum(covid_19_cases[Confirmed]),LASTDATE(covid_19_cases[Date]))"      
- Step 15 : Created a new group to group states by region in the "StatewiseTestingDetails" table. Group name- "State (groups)    
 - Step 16 : Created a new column named Percent Positive to show the percentage of positive cases from the total samples for each row. 
"Percent Positive = (StatewiseTestingDetails[Positive]/StatewiseTestingDetails[TotalSamples])*100"
 - Step 17 : New measure was created to calculate total distance travelled by flights & a card visual was used to represent total distance.

# Report
  Page 1 - CASES
 - Filled map shows total cases and deaths of each state/union territory emphasizing on intensity of cased through Conditional Formatting - Format Stye = Gradient ,  Based on Confirmed Cases column, Summarization = Maximum
 - Measures "RegionTotalCases" and "Regiondeaths" used in tooltips
 - Line and clustered column chart- Shows Regionwise confirmed cases and deaths. Drill down statewise analysis within each region.
 - Pie Chart- Represents distribution of cases by region. Drill down for statewise analysis of each region individually.
 - Year filter for 2020 & 2021 placed on the page

  Page 2 - TESTING RESULTS
 - Line chart- Total positive and negative cases over time
 - Used Analysis feature of Power BI to analyze: 1) Rapid increase in positive cases between Q2 and Q3 for the year 2021 through a clustered column chart 2) Ribbon chart for abnormal rise in cases between Q1 and Q2 during 2021
 - Treemap- To be used to drillthrough to "(Drill)Regional page for regional analyses.
 - Year filter placed on the page. State(groups) used for the visualization

  Page 3 - (DRILL) REGIONALTESTS
 - Cards showing total samples, total positive and negative cases, percentage of positive cases. (Cards have been group together)
 - Table to show data of the selected region
 - Area Chart- Positive cases over time
 - Column Chart- Statewise cases including positive and negative cases
   
  Page 4 - VACCINATION PERFORMANCE
 - Vaccination overview 2021
 - Bar Chart- Doses administered by state
 - Pie Chart- Dose distribution by Vaccine variety (Shown through unpivoted columns)
 - Line Chart- Doses administered over time. Trend line inserted for better analyses

  Page 5 - POPULATION VACCINATED THROUGHOUT STATES IN INDIA (2021)
 - Slicer has been synced with the previous page
 - Table - shows the top 5 states with highest vaccinated population
 - Donut chart - Genderwise distribution of the vaccinated population (Unpivot columns used)
 - Cards- Shows Total population vaccinated, sites set up for vaccination, total doses administered
 - Filter page by region by using the slicer

 - Page 6 - FINAL OVERVIEW
 - This page gives an overview of the whole report highlighting important data points. Use the slicer or the map for statewise visualization of data.

 -![Snap_1]![image](https://github.com/AmanBaker06/Victor_Analyst/assets/168013894/0eb39f9b-a9f8-4496-92c6-9b2ea7ace332)




 



