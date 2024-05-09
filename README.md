# energy_project

# European Energy Production Dataset Analysis¶

### Introduction
This Jupyter Notebook analyzes the European countries Energy production during 2015-2023 period. The project focuses on studying the efficiency of using renewable and non-renewable sources for electricity production. Also, data on the GDP of selected countries for the same period were used.

### Analysis
### Tools

- Excel - Data cleaning
- SQL Server - Data Analysis
- Python -
1. Create pivot table.
2. Analyze the correlation between columns Total_renewable and Total_Non_Renewable.
3. Grouping by country and calculating the average GDP.
4. Grouping by country and calculating the average value of energy produced from renewable sources.
5. Combining tables by country.
6. Correlation between the indicators of the average GDP in the country and the average value of energy produced from renewable sources.
7. Visualize correlation with scatter plot.
8. Creating pivot table to calculate the total amount of energy produced from renewable and non-renewable sources depending on the year, cumulatively for all European countries. 
9. Plotting with Seaborn.
10. The general conclusion on the dynamics of energy production in Europe based on the data obtained.
- Tableau Public - Creating reports
  
#### Data Loading and Cleaning:

- Loaded the dataset and perform any necessary cleaning steps.
- Data saved in tables: country_capacity.csv, Country, year, GDP 2015-2023.csv.

#### Exploratory Data Analysis (EDA)
EDA involved exploring the data to answer key questions, such as:
- Is there any correlation between the indicators of the average GDP in the country and the average value of energy produced from renewable sources?
- Is there any correlation between the total amount of energy produced from renewable and non-renewable sources?
- Which countries have generated the most electricity from renewable sources?
- Which countries are most dependent on the use of non-renewable energy sources?

#### Data Analysis

```sql
SELECT 
    Country,
    Year,
    GDP
FROM (
    SELECT 
        string_field_0 AS Country,
        CAST(double_field_2 AS STRING) AS `2015`,
        CAST(double_field_3 AS STRING) AS `2016`,
        CAST(double_field_4 AS STRING) AS `2017`,
        CAST(double_field_5 AS STRING) AS `2018`,
        CAST(double_field_6 AS STRING) AS `2019`,
        CAST(double_field_7 AS STRING) AS `2020`,
        CAST(double_field_8 AS STRING) AS `2021`,
        CAST(double_field_9 AS STRING) AS `2022`,
        CAST(double_field_10 AS STRING) AS `2023`
    FROM 
        `energy-project-422313.energy.GDP_3`
    WHERE 
        string_field_0 IN (
'Albania','Andorra','Austria','Belarus','Belgium','Bosnia and Herzegovina','Bulgaria','Croatia','Cyprus','Czechia','Denmark','Estonia',
'Faroe Islands','Finland','France','Germany','Greece','Hungary','Iceland','Ireland','Italy','Kosovo','Latvia','Lithuania','Luxembourg',
'Malta','Montenegro','Netherlands','North Macedonia','Norway','Poland','Portugal','Moldova','Romania','Serbia','Slovakia','Slovenia',
'Spain','Sweden','Switzerland','Ukraine','United Kingdom')
) 
UNPIVOT (
    GDP FOR Year IN (
        `2015`,
        `2016`,
        `2017`,
        `2018`,
        `2019`,
        `2020`,
        `2021`,
        `2022`,
        `2023`
    )
)
ORDER BY 
    Country ASC,
    Year ASC;
```
```sql
SELECT 
    Country,
    Group_Technology,
    Technology,
    RE_or_Non_RE,
    Year,
    Electricity_Installed_Capacity__MW_
FROM 
    `energy-project-422313.energy.Country_new`
WHERE 
    Year BETWEEN 2015 AND 2023
    AND Region = 'Europe'
GROUP BY 
    Country,
    Group_Technology,
    Technology,
    RE_or_Non_RE,
    Year,
    Electricity_Installed_Capacity__MW_
ORDER BY 
    Country;
```

### Python
Jupiter notebook is uploaded [Energy_project.ipynb](Energy_project.ipynb)

### Energy production dashboard
[Tableau Dashboard_European_Electricity_Production](https://public.tableau.com/app/profile/tetiana.lopatynska/viz/EuropeanEnergyProductionDashboard/PrimaryDashboard)

### Video presentation
[Energy_project](https://drive.google.com/file/d/1iRjXTvMeb-eUhx_yzFIOsmK4PIWiuIRS/view?usp=sharing)
