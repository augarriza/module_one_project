# Covid-19 outbreak in the United States: Historical death counts per state compared to counts in 2020
*Emily Horton & Alejandro Ugarriza Crespo*

*DAFT March 2020, Ironhack Berlin, April 10th*

## Content
- [Project Description](#project-description)
- [Questions & Hypotheses](#questions-hypotheses)
- [Dataset](#dataset)
- [Database](#database)
- [Workflow](#workflow)
- [Links](#links)

## Project Description
Thousands of deaths per day, hundreds of millions of citizens asked, when not forced, to stay home, national health systems on the verge of collapsing, borders closed, some of the strongest economies in the world forseeing a contraction of their GDP by more than 8 points. The human civilisation forced to look at its reflection on the mirror due to a previously unknown virus named Covid-19.
What is the truth behind all the dramatic headlines? Only data knows.This project is our humble attempt to better understand.

## Questions & Hypotheses
Our main hypotheses was that different socio-economical factors could have a direct impact on the amount of deaths due to Covid-19. In order to further analyse that, we focused on the United States of America given the notorious amount of public data available. Answering the following three main questions became the goal towards which we focused our efforts:
#### 1. Compared to previous years, is there an actual increase in death counts taking the same time frame (February-March)?
#### 2. Are there significant differences between states?
#### 3. If so, could socio-economical factors or demographic indicators shed some light into it?

## Datasets
#### New York Times COVID-19 Data, csv
Pulled on April 8th from Github, State-Level Data for March 31st, 2020
The dataset included a cumulative count of cases and deaths due to COVID19. To match our other data, we chose data for all states on March 31st, 2020. The cumulative aspect helped us match our next dataset. 
https://github.com/nytimes/covid-19-data

#### CDC Provisional Death Counts for Coronavirus Disease (COVID-19), API
Pulled on April 8th, Grouped by State 
The dataset focused on overall deaths and COVID-19 deaths, with additional information about pneumonia and influenza. We chose the columns with information about COVID19 deaths and all deaths, grouping by state. 
The limitation of this dataset was that could have a delay of up to two weeks since the CDC waits for official submission of each death certificate for reporting. Because of this delay, even though we pulled the information on April 8th, we decided that February-March was our time frame.
https://data.cdc.gov/NCHS/Provisional-Death-Counts-for-Coronavirus-Disease-C/hc4f-j6nb

#### CDC Wonder Interface About Underlying Cause of Death, 1999 - 2018, txt
Pulled on April 8th, Grouped By Month (February and March), Grouped by Year (2013-2018), Grouped by State
We made preliminary selections through the Wonder interface, choosing not to change any grouping on cause of death. 
https://wonder.cdc.gov/ucd-icd10.html

#### US Census Demographic Data, csv
Pulled on April 9th from Kaggle
The dataset has gender, ethnicity, and income-related information from 2017. We decided to use only the gender and income per capita columns. 
https://www.kaggle.com/muonneutrino/us-census-demographic-data#acs2015_county_data.csv

#### Health Insurance Dataset, csv
Pulled on April 9th from Kaggle
The dataset focuses on the change in uninsured rate per state between 2010 and 2015 due to the Affordable Care Act. We chose to use the uninsured rate from 2015. 
https://www.kaggle.com/hhs/health-insurance

#### Population Distribution by Age, csv
Pulled on April 9th from KFF website
The dataset shows the age groups for each state from 2017. 
https://www.kff.org/other/state-indicator/distribution-by-age/?currentTimeframe=0&sortModel=%7B%22colId%22:%22Location%22,%22sort%22:%22asc%22%7D

## Folders and Files
#### Datasets
   1. acs2017_census_tract_data.csv : US Census Demographic Data, csv
   2. agegroups_us_population_2017.csv: Population Distribution by Age, csv
   3. Mortality_March-February_2013-2018.txt: CDC Wonder Interface About Underlying Cause of Death, 1999 - 2018, txt
   4. nytimes_cumulative_covid_per_state.csv: New York Times COVID-19 Data, csv
   5. states_healthcare.csv: Health Insurance Dataset, csv
    
#### Notebooks
   I. Import_Cleaning
     1.cdc_api_access.ipynb: getting data from 'CDC Provisional Death Counts for Coronavirus Disease (COVID-19), API'
     2.cleaning_census2017_kaggle_dataset.ipynb: cleaning data from 'acs2017_census_tract_data.csv'
     3.cleaning_groupage_2017_dataset.ipynb: cleaning data from 'agegroups_us_population_2017.csv'
     4.nytimes_mortality_to_data_frame.ipynb: cleaning data from 'nytimes_cumulative_covid_per_state.csv' and 'Mortality_March-              February_2013-2018.txt'
     5.states_healthcare_to_df.ipynb: cleaning data from 'states_healthcare.csv'
        
   II. Merging_Analysis: notebooks used to merge and analyse the data. Suggested order to follow:
     1. Merging_nytimes_and_all_deaths_perstate _df.ipynb
     2. merging_cdc_mortality.ipynb
     3. Further_analysis_nyt_cdc_covid_deathrates.ipynb
     4. cdc_and_mortality_without_covid.ipynb
     5. cdc_mortality_df_analysis_and_plotting.ipynb
     6. merging__census_pop_income__healthcare__agegroups_mortality.ipynb
     7. Tennessee_California_Florida.ipynb
     
#### Pickles
   All the dataframes created through the process of analysis. Suggested order to follow:
    1. nytimes.pkl
    2. cdc_deaths_all_causes.pkl
    3. deaths_all_causes_bystate.pkl
    4. deaths_allcauses_byage.pkl
    5. nytimes_cdcapi_combined.pkl
    6. nytimes_cdcapi_withmortality.pkl
    7. cdc_mortality_df.pkl
    8. cdc_mortality_no_covid_df.pkl
    9. cdc_morality_to_merge.pkl
    10. mortality_aggregation.pkl
    11. df_census_tp_gender.csv
    12. df_census_income.csv
    13. df_census_groupage.csv
    14. healthcare_percentage.pkl
    15. final_df.pkl
    


## Database
Our database is broken down into two tables, one focusing on the mortality per state over time and the second focusing on demographic data per state. We have pulled the 2020 death difference from 2018 and the overall death count from our mortality table into our demographic table. See our relational schema below:

## Workflow
1. We collected data on death counts per state from several sources in order to obtain: cummulative death counts due to Covid per state for February and March, cummulative death counts for all causes per state for February and March, historical cummulative death counts per state for February and March
2. On parallel, we collected data to create our second table focused on demographic and socio-economical indicators per state
3. We combined the data to create our first table focused on the mortality per state over time
4. Based on our "mortality table", we decided to focus on the states with a largest increase in death counts from 2018 to 2020.
5. We then digged into our "dempographic table" and ranked all the states based on three indicators that we considered could have a direct impact on deaths due to Covid-19: the percentage of uninsured population, the percentage of population over 65 years and the percentage of population living under the threshold of poverty.

## Conclusions
After collecting, cleaning and combining all our data we took a step back and asked ourselves whether we were actually capable of moving further with our analysis. We both realised that our data was lacking accuracy and our tools as junior data analysts were not enough to study in more depth a topic that has proven to be of great complexity even for experienced scientists.
We then decided not to try and bring any conclusion to the table.
However, we also realised that we had gathered some interesting data and we are happy to share it with the community hoping it can be of help for anyone who is in a place we are not at the moment and thus capable of reaching higher conclusions.



