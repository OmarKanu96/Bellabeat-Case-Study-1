# Bellabeat-Case-Study-1
Bellabeat Data analysis Case Study 
# Inroduction 


Welcome to my Bellabeat data analysis case study! Bellabeat is a high tech manufacturer of health-focused products for women and they are looking for new ways to expand their audience. My role in this case study is to focus on and analyze smart device fitness data that could potentially unlock the new growth that Bellabeat is looking for 

**Background** 

The Bellabeat product that i chose to focus on is the Bellabeat app in search for insights that i can explore and discover in order to make this product that much greater. i will be using the Fitbit Fitness Tracker Data which contains personal fitness tracker from 30 fitbit users

**Stakeholders**

* **Urska Srsen**: Bellabeat's cofounder and Chief Creative Officer 
* **Sando Mur**: Mathematician and Bellabeats cofounder; vital member of the Bellabeat 
executive team  

 # Ask 
* Buisness Task: Discover potential opurtunities for growth and recomend ways to improve the Bellabeat app based on trends that i find within the data
* Guided Questions
 1. What are some trends in the smart device usage 
 2. how do the trends apply to the Bellabeat app and customers
 3, How do these trends improve the marketing strategy

# Prepare 
the first thing that i did was upload the data in R studio. i specifically chose 5 datasets each dataset is a fitness tracker from thirty fitbit users. the datasets that i used for this case study were daily activity level, exercise intenisity, calorie tracker, sleep and weight lodd tracker. 

First thing i did was download the neccesary R studio Packacges

`install.packages("tidyverse")`

`installed.packages("lubridate")`

`install.packages("lubridate")`

`install.packages("dplyr")`

`install.packages("tidyr")`

`install.packages("janitor")`

`install.packages("ggplot2")`

`library(tidyverse)`

`library(lubridate)`

`library(dplyr)`

`library(tidyr)`

`library(janitor)`

`library(ggplot2)`
# Process

**Import the datasets (read.csv)**

`activity <- read_csv("dailyActivity_merged.csv")`

`intensities <- read_csv("dailyIntensities_merged.csv")`

`calories <- read_csv("dailyCalories_merged.csv")`

`sleep <- read_csv("sleepDay_merged.csv")`

`weight <- read_csv("weightLogInfo_merged.csv")`

**Clean Data**

After all the dataframes have been imported, i went ahead and started cleaning my data. first thing that i did was get a feel for the data. 

`activty <- activty %>% mutate( Weekday = weekdays(as.Date(ActivityDate, "%m/%d/%y")))`

`calories <- calories %>% mutate(Weekday = weekdays(as.Date(ActivityDay, "%m/%d/%y")))`

`sleep <- sleep %>% mutate(Weekday = weekdays(as.Date(SleepDay, "%m/%d/%y")))` 

From there i am now ready to analyze the data 

# Analayze
fist thing i do is determine the number of participants in each group by using 'n_distinct'

`n_distinct(activity$Id)`

`n_distinct(calories$Id)`

`n_distinct(intensity$Id)`

`n_distinct(sleep$Id)`

`n_distinct(weight$Id)`

In summary we find that there are 33 particpants within the activity, calories, and intensities datasets, 24 participants in the sleep dataset and only about 8 paritcipants in the weight dataset 

# Activity

`activity %>% 
  select(TotalSteps, TotalDistance, SedentaryMinutes, Calories) %>%
  summary()`
  
# Active minutes per category

`activity %>%
  select(VeryActiveMinutes, LightlyActiveMinutes, FairlyActiveMinutes
        SedentaryMinutes) %>%
  summary()`
  
# Calories

`calories %>% 
  select(calories)%>%
  summary()`
  
# Sleep

`sleep %>%
  select(TotalSleepRecords, TotalMinutesAlseep, TotalTimeInBed) %>%
  summary()`
  
