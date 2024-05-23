# Patient Wait List Project

### Report Link :https://drive.google.com/file/d/1_8PW1DURVZl1G58n8IyTEh-0W4qXmQwd/view?usp=sharing

## Problem Statement

The aim of this project is to develop a comprehensive and dynamic dashboard using Power BI to track, analyze, and visualize patient wait times in healthcare facilities. By providing detailed insights into current wait times, historical trends, and demographic profiles, this project seeks to enhance hospital resource management, reduce patient wait times, and improve overall patient care. The analysis will help identify areas needing urgent attention, optimize resource allocation, and ensure timely treatment for all patients.

## Steps followed 


### 1. REQUIREMENTS GATHERING

###  - Identify Stakeholders
- Healthcare administrators

- Medical staff




### - Objectives
- Track the Current Status of Patient Waiting List

Identify the current number of patients awaiting treatment.
Monitor wait times and the types of treatments patients need.
Enable hospitals to better manage resources and prioritize patient care effectively.
Analyze Historical Monthly Trend of Waiting List in Inpatient and Outpatient Categories:

- Examine how the number of patients on waiting lists has changed from 2018 to 2021.
Identify patterns or trends in monthly wait times.
Differentiate between inpatient (patients who stay in the hospital) and outpatient (patients who do not stay overnight) categories to understand their specific needs.

- Detail Specialty, Level, and Age Profile Analysis:

Analyze the waiting list data to determine which medical specialties have the highest number of patients waiting.
Investigate differences in wait times based on the level of care required (e.g., intensive care vs. regular check-ups).
Explore how patient age affects wait times to identify if older patients experience longer waits than younger ones.

### - Scope of the Study

- Analysis covers patient waitlist data from 2018 to 2021.

- Project Scope: Includes tracking the current status of patient waitlists, analyzing historical trends, and performing detailed analyses by specialty, care level, and age profile.

- Limitations: The analysis is based on the available dataset and does not include real-time data.

### 2. DATA COLLECTION

- Data Source: Used a folder as a data connector to collect inpatient and outpatient data stored in Excel files.
- Loading Data: Loaded the data into Power BI for further processing and analysis.

### 3. DATA TRANSFORMATION

- Ensure Correct Data Types:
Verified that all data types are in the correct format.

Converted date data type from text to date using the Locale method.

- Data Validation:
Counted the number of rows and columns in each dataset to ensure completeness and accuracy.

- Standardize Outpatient Data:
Added a new column, "Case_type," to the outpatient data to match the structure of the inpatient data.

Steps:
Went to the column section, selected "Custom Column."
Added a new column named "Case_type" with the value "Outpatient."

- Append Data:

Combined the inpatient and outpatient data into a single table.

Steps:
Selected "Append Queries as New."
Renamed the new appended table to "All Data."

- Apply Changes:
Clicked "Close & Apply" to save and apply the transformations.

 ### 4. DATA MODELLING
- Mapping Specialty Group:

Specialty Group Table:
Created AND imported a mapping specialty group table containing information on different medical specialties.

- Linking Tables:

Data Model Setup:
Mapped the specialty group table to the "All Data" table in the modelling pane of Power BI.

-  Setting Cardinality:

Relationship Type:
Defined the cardinality of the relationship as "one-to-many," indicating that each specialty in the specialty group table can be associated with multiple records in the "All Data" table.

Crossfilter Direction:
Set the crossfilter direction to "single," ensuring that filters applied on the specialty group table affect the "All Data" table, but not vice versa.

By correctly setting up the data model, I ensured accurate relationships between tables, enabling comprehensive analysis and reporting on the various specialties within the healthcare dataset.


 ### 5. DATA VISUALIZATION
1. Key Performance Indicators (KPIs):

    Latest Month Waitlist:

            DAX EXPRESSION:

            Latest Month Waitlist = CALCULATE(SUM(All_Data[Total]),
             All_Data[Archive_Date] = MAX(All_Data[Archive_Date]))


    Previous Year Month Waitlist:

            DAX EXPRESSION:

           PY Latest Month Waitlist = CALCULATE(SUM(All_Data[Total]),
              VALUE(All_Data[Archive_Date]) = EDATE(MAX(All_Data[Archive_Date]), -12))

Snap of Latest Month Waitlist and PY Latest Month Waitlist:

![Screenshot 2024-05-23 115119](https://github.com/TheDataVirtuoso/CollinsBahati.github.io/assets/87636760/b7793e06-ab28-4d36-a6af-dd585ac9c06f)



2.  Creating a Dynamic Measure for Median and Average:

Blank Table:

I created a blank table named "Calc Method" with columns "Calc Method" containing values "Median" and "Average".

Create Slicer:
I used the "Calc Method" table to create a slicer.
changed the slicer to a tile style.
and turned off the header to make it look like a button.
I turned on the single select option.

3. DAX Expressions for Average and Median Wait Lists:

    Average Wait List:

            DAX EXPRESSION:

            Average Wait List = AVERAGE(All_Data[Total])



    Median Wait List:

            DAX EXPRESSION:

            Median Wait List = MEDIAN(All_Data[Total])


4. Dynamic Measure to Interact with Button:


            DAX EXPRESSION:

            Avg/Med Wait List = SWITCH(VALUES('Calculation Method'[Calc Method]),
             "Average", [Average Wait List], "Median", [Median Wait List])


Snap of Dynamic Measure

![Screenshot 2024-05-23 121006](https://github.com/TheDataVirtuoso/CollinsBahati.github.io/assets/87636760/9fa1898e-baef-4c71-8a60-d5cde6cd0383)

5. Dynamic Title for Key Indicator:

       DAX EXPRESSION:

            Dynamic Title = SWITCH(VALUES('Calculation Method'[Calc Method]), "Average",
             "Key Indicators - Patient Wait List (Average)", "Median", "Key Indicators - 
             Patient Wait List (Median)")

6. Visualization Creation:

-  Donut Chart:

I used "Avg/Med Wait List" as the value.

I added "case_type" as the legend.

Placed a card in the center of the donut chart displaying the overall "Avg/Med Wait List".

Snap of Donut Chart

![Screenshot 2024-05-23 121915](https://github.com/TheDataVirtuoso/CollinsBahati.github.io/assets/87636760/7fe8b123-c5a3-4d43-8cbd-e34dd4d04da9)

-  Stacked Column Chart:

I used "Avg/Med Wait List" as the value.

I added "time_bands" and "age_profile" as the axis and legend, respectively.


Snap of Column Chart

![Screenshot 2024-05-23 122452](https://github.com/TheDataVirtuoso/CollinsBahati.github.io/assets/87636760/2b46d556-f02e-40d6-84fd-70ee6c649066)

-  Multirow Card:

I showed the top 5 by "speciality_name" using the "Avg/Med Wait List" measure.

Snap of Multirow card

![Screenshot 2024-05-23 122722](https://github.com/TheDataVirtuoso/CollinsBahati.github.io/assets/87636760/a7696878-bbb1-403c-915c-86dbe6947712)

-  Line Chart:

Inpatient and Day Case Patients:
I used "Date" on the x-axis and "Case_type" as the legend.
I filtered by "Inpatient" and "Day case" patients.

Outpatient:
I used "Date" on the x-axis and "Case_type" as the legend.
I filtered by "Outpatient".

Snap of Line charts

![Screenshot 2024-05-23 122922](https://github.com/TheDataVirtuoso/CollinsBahati.github.io/assets/87636760/d3e9811e-8275-4629-8b3c-f8ddcc9fb104)



-  Slicers:

I created slicers for:
Date,
Case_type,
Speciality_name,
Age_profile and
Time_bands,

Snap of Slicers

![Screenshot 2024-05-23 123222](https://github.com/TheDataVirtuoso/CollinsBahati.github.io/assets/87636760/68b514b9-e3d7-4968-891c-3b4d8613d6e2)


-  Matrix Table:

I added "date" and "case_type" (daycase, inpatient, outpatient) as rows.

I drilled down to show "time_bands" and "speciality groups".

Snap of Matrix Table

![Screenshot 2024-05-23 123531](https://github.com/TheDataVirtuoso/CollinsBahati.github.io/assets/87636760/5a79a78f-c31c-457c-81a8-d5f46304519c)


7. Build Aesthetics:

Canvas Background:
I changed the canvas background using MS PowerPoint to enhance the visual appeal.

I ensured that the background complemented the overall theme and was not too distracting.

8. Interactivity:

Edit Interactions:
I enabled edit interactions to ensure every visual was interactive with each other.
This ensured that selections in one visual filtered the data in the other visuals, providing a more dynamic and insightful user experience.

 
 # Report Snapshot (Power BI DESKTOP)

 
![PATIENT WAITLIST](https://github.com/TheDataVirtuoso/CollinsBahati.github.io/assets/87636760/69f8b307-f32b-4be1-9970-6ae8ef787d4b)

![DETAIL SNAP](https://github.com/TheDataVirtuoso/CollinsBahati.github.io/assets/87636760/c18c7aee-bca4-448f-9cc7-7304cacd3360)


# Insights

A double page report was created on Power BI Desktop 

Following inferences can be drawn from the report;

### [1] Patient Waitlist Statistics:

   The latest month's waitlist reached 709K patients, while the previous year's waitlist was slightly lower at 640K patients.

 Outpatient cases exhibited the highest average waitlist, with 629K patients in the latest month and 563K patients in the previous year. This was followed by day case and inpatient cases, which had comparatively lower average waitlists.


           
### [2] Trend Analysis:


  
  There was a noticeable gradual increase in the outpatient waitlist from 2018 to 2021, indicating a growing demand for outpatient services. 
  
  ### [3] Specialty Analysis:
  
General Surgery emerged as the specialty with the highest patient waitlist in both the latest month and the previous year, with 14K and 11K patients, respectively. This was followed closely by Orthopaedics.

Development Pediatrics had the lowest patient waitlist, suggesting a lower demand for services in this specialty.

 ### [4] Age Profile Analysis:
Patients aged between 16-64 exhibited a high waitlist, indicating a higher demand for services among adults compared to children. 


 ### [5] Time Band Analysis:


Patients in the age group of 18+ experienced high waiting times within the time band analysis, highlighting potential areas for improvement in service delivery.
 
 ### Recommendations:
 
 
 
        Capacity Planning:

 Given the increasing demand for outpatient services and the high waitlists observed, healthcare facilities should prioritize resource allocation and capacity planning in outpatient departments..

          Specialty Allocation:

  Considering the high patient waitlists in specialties like General Surgery and Orthopaedics, it's crucial to allocate resources efficiently and potentially expand services in these areas to meet the demand.


         Data-Driven Decision Making:

  Continuous monitoring and analysis of patient waitlist data are essential to identify trends and patterns, enabling proactive decision-making and resource allocation to address emerging needs effectively.


       Staff Training and Workflow Optimization:

  Providing training to staff on efficient patient management techniques and streamlining workflows can improve operational efficiency, leading to reduced wait times and enhanced patient satisfaction.


        Resource Reallocation:

  Periodic assessment of resource distribution across departments and shifts can help optimize resource allocation based on demand fluctuations, ensuring efficient utilization and reducing wait times.









