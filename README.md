# Water Access And Sanitation In Africa
## Table of content
- [Project overview](#project-overview)
- [Data Source](#data-source)
- [Tools](#tools)
- [Data Cleaning](data-cleaning)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Results/Findings](#results-findings)
- [Reccomendations](#reccomendations)

### Project Overview
This project analyzes water access and sanitation across various communities in multiple African countries. By examining key patterns and trends within the dataset, the analysis aims to uncover disparities, identify critical areas for improvement, and provide data-driven recommendations. The insights generated will help governments, policymakers, and stakeholders implement effective strategies to enhance water accessibility and sanitation infrastructure in these communities.

### Data Source
Axia Africa : The primary data used for this analysis is the [Water supply & sanitation in Africa](Water_Supply_Sanitation_Africa.csv) dataset containing details about water availability and sanitation in several communities in selected african countires.

### Tools
- Power query
- SQL

### Data Cleaning
The dataset used in this analysis was provided in a clean and consistent format. An initial assessment was conducted to check for missing values, duplicate entries, and data type inconsistencies. No data cleaning or preprocessing steps were required. The data was determined to be ready for immediate analysis.

### Exploratory Data Analysis
- What is the average water availability (litres per capita per day) for each country?
- Communities with at least one non-functional water points
- The top five communities with the highest annual sanitation maintenance costs.
- Total number of functional and non-functional water points per country
- Communities with a high incidence of waterborne diseases (>20%)
- average distance to the water source per region
- Communities that receive both government and NGO support
- Community with the highest population per country
### Data Analysis
SQL was used to query the dataset to extract valuable insights and arrive at actionable recommendation.
Here are the queries deployed in this analyis.

```sql
SELECT country,
avg(`Water Availability (liters per capita per day)`) AS Avg_Water_Availability
from water_supply_sanitation_africa
group by country;
```
```sql
SELECT `Community Name`, `Number of Non-Functional Water Points`
FROM water_supply_sanitation_africa
WHERE `Number of Non-Functional Water Points` >= 1;
```
```sql
SELECT `Community Name`, `Annual Maintenance Cost (USD)`
FROM water_supply_sanitation_africa
ORDER BY `Annual Maintenance Cost (USD)` DESC
LIMIT 5;
```
```sql
SELECT Country, sum(`Number of Functional Water Points`) AS `Total Functional WaterPoints`, 
                sum(`Number of Non-Functional Water Points`) AS `Total Non Functional Water Points`
FROM water_supply_sanitation_africa
GROUP BY Country
ORDER BY `Total Functional WaterPoints`;
```
```sql
SELECT `Community Name`, `Waterborne Diseases Incidence Rate (%)`
FROM water_supply_sanitation_africa
WHERE `Waterborne Diseases Incidence Rate (%)` > 20;
```
```sql
SELECT region,
avg (`Average distance to water source (km)`)
AS` Average distance to water source (km)`
FROM water_supply_sanitation_africa
GROUP BY region;
```
```sql
SELECT `Community Name` AS `Communities that receive both government and NGO support`
FROM water_supply_sanitation_africa
WHERE `Government Support` = 'Yes'
AND `NGO Support` = 'Yes';
```
```sql
SELECT country, `Community Name`, population
FROM water_supply_sanitation_africa AS 	 table_1
WHERE Population = (  
SELECT MAX(Population)  
FROM water_supply_sanitation_africa AS table_2
WHERE table_1.Country = table_2.Country)
ORDER BY population DESC;
```
### Results/ Findings
- Several communities have non-functional water points, reducing overall water access.
- Some high-population communities have low water availability per capita.
- Some communities travel long distances to access water, increasing hardship, especially for women and children.
- Some communities lack both government and NGO support, making them vulnerable to poor water access and sanitation.
- Some communities lack proper sanitation facilities, increasing the risk of waterborne diseases.
- Some regions have higher annual maintenance costs but low functional water points- an indication of poor resouce management.
### Reccomendations
-	Prioritize Maintenance & Repair of Non-Functional Water Points
-	Increase Water Infrastructure in High-Population, Low-Water Communities
-	Reduce Distance to Water Sources in Remote Regions by developing closer water points in communities where the average distance is significantly high.
-	Encourage public-private partnerships to expand funding and water projects and NGOs should prioritize working in communities with no government support.
-	Invest in Sanitation Facilities & Hygiene Education.
-	Improve Budget Allocation for Water & Sanitation Projects.

  




