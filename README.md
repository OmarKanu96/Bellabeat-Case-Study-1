# Bellabeat-Case-Study-1
Bellabeat Data analysis Case Study 
# Inroduction 


Welcome to my Bellabeat data analysis case study! Bellabeat is a high tech manufacturer of health-focused products for women and they are looking for new ways to expand their audience. My role in this case study is to focus on and analyze smart device fitness data that could potentially unlock the new growth that Bellabeat is looking for 

**Background** 

The Bellabeat product that i chose to focus on is the Bellabeat app in search for insights that i can explore and discover in order to make this product that much greater, as well as guide the marketing strategy for Bellabeat fitness. i will be using the Fitbit Fitness Tracker Data which contains personal fitness tracker from 30 fitbit users

**Stakeholders**

* **Urska Srsen**: Bellabeat's cofounder and Chief Creative Officer 
* **Sando Mur**: Mathematician and Bellabeats cofounder; vital member of the Bellabeat 
executive team  

 # Ask 
* Buisness Task: Discover potential opurtunities for growth and recomend ways to improve the Bellabeat app based on trends that i find within the data
* Guided Questions
 1. What are some trends in the smart device usage 
 2. how do the trends apply to the Bellabeat app and customers
 3. How do these trends improve the marketing strategy

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

`# Activity`

`activity %>% 
  select(TotalSteps, TotalDistance, SedentaryMinutes, Calories) %>%
  summary()`
  
`# Active minutes per category`

`activity %>%
  select(VeryActiveMinutes, LightlyActiveMinutes, FairlyActiveMinutes
        SedentaryMinutes) %>%
  summary()`
  
`# Calories`

`calories %>% 
  select(calories)%>%
  summary()`
  
`# Sleep`

`sleep %>%
  select(TotalSleepRecords, TotalMinutesAlseep, TotalTimeInBed) %>%
  summary()`

  # What did I discover?
From the summaries above i was able to find out 
* The total average steps of the participants was 7,638. However by diving a little deeper i found out that the Centers for Disease Control and Prevention(CDC) recomends about 10,000 steps a day 
* Average total distance walked was 5.5 miles 
* Most of our participants are lighlty active 
* On Average particpants spend about 7 hrs asleep
* On Average particpants burn about 97 calories per hour 
* Sedentary minutes on average is about 16.5 hrs

# Share 

**Lets take a look at some visuals!**

`ggplot(data = activty) + geom_point(mapping = aes(x = TotalSteps, y = Calories), color = 'green') +
  geom_smooth(mapping = aes(x = TotalSteps, y = Calories)) + labs(title = "Total Steps vs Calorie Amount")`
  
![file_show](https://github.com/OmarKanu96/Bellabeat-Case-Study-1/assets/127154130/b6fbf466-b11c-4a1d-ae83-c43123289a07)

By looking at the above visual it can be determined that their is a positive correlation between Total number of steps and Calories burned, meaning that the more steps that a participants takes in a day the number of calories burned increases. 

`ggplot(data = sleep) + geom_point(mapping = aes(x = TotalMinutesAsleep, y = TotalTimeInBed), color = 'blue') +
  labs(title = "Time Asleep vs Time in Bed")`

![file_show-2](https://github.com/OmarKanu96/Bellabeat-Case-Study-1/assets/127154130/8d0e966c-550f-480b-a0dd-4a9395d32347)

Again we see a positive correlation in the visual above between the amount of time spent in bed versus the amount of time asleep. One way that this data can be used to improve the bellabeat app is to have a section in their app where amount of sleep you get is tracked, so that users have a good read on how much sleep they are getting. 

`ggplot(data = merged_data) + geom_point(mapping = aes(x = SedentaryMinutes, y = TotalMinutesAsleep)) +
  labs(title = "Sedentary Minutes vs Time Asleep")`

  ![file_show-3](https://github.com/OmarKanu96/Bellabeat-Case-Study-1/assets/127154130/1b848d77-1bf9-4ffe-92aa-f590aa5aa9ba)
`cor(merged_data$TotalMinutesAsleep,merged_data$SedentaryMinutes) = -0.2065253`
Know for the visual above we see a negative correlation meaning that as participants are less active the less amount of sleep they tend to get. 

Lastly, i want to take a closer look at how the day of the week affects our Total Steps. 

`summarized_activity_sleep <- merged_data %>% group_by(Weekday) %>% 
  summarise(AvgDailySteps = mean(TotalSteps),
            AvgAsleepMinutes = mean(TotalMinutesAsleep),
            AvgAwakeTimeInBed = mean(TotalTimeInBed), 
            AvgSedentaryMinutes = mean(SedentaryMinutes),
            AvgLightlyActiveMinutes = mean(LightlyActiveMinutes),
            AvgFairlyActiveMinutes = mean(FairlyActiveMinutes),
            AvgVeryActiveMinutes = mean(VeryActiveMinutes), 
            AvgCalories = mean(Calories))`

`ggplot(data = summarized_activity_sleep) + geom_col(mapping = aes(x = Weekday, y = 
   AvgDailySteps), fill = "blue") + labs(title = "Total Step Count Each Day")`

   ![file_show-5](https://github.com/OmarKanu96/Bellabeat-Case-Study-1/assets/127154130/a67a3da8-ec75-4a40-af43-a4d86f6d35fc)

what we see is that most participants take the most steps on Saturday, Sunday, and Thursday and then we see a dropoff throughout the other days of the week with Friday being the day that they take the least amount of steps. 


# ACT
**Conclusions** 
1. The average amount of steos taken by our participants falls below the avegrage recomneded by the CDC which is 10,000 steps. I recomend including a stpe tracker in the app wherre users are able to see the amount of steps that they take each day with the goal being 10,000 steps per day and if they are to reach that goal on a consistant basis lets say 3-4 days in a week they will get a in app medal,  
2. Majority of our participants are likely active. it will benefit Bellabeat to use catagories within the app showing users where they fall when it comes to how active they are and as they progress in their activity level they should get a notification celebrating the progress they've made and a motivational message for example "Keep up the good work", or "Great job lets keep going" 
3. Based on our data we found that the more steps that is taken each day will more than likely result in a increase of total calories burned. Bellabeat should run a campaign highlighting how important movement is and how it is vital for our health and wellnes 
4. A Campaign can also be ran highlighting the benefits and importance of sleep that individuals should be getting but also a in app sleep tracker that tracks the amount of sleep users are getting a night which will help users know how much sleep they are getting a night.
5. i would also recommed using notifications to give a freindly reminder to users to get active or get some steps in specifically after 1-2 has gone by without any sort of activity from the users. Example after a couple hours apple watches will notify you to drink your water.

# Bellbeat Tableau Dashboard 
![Dashboard 1](https://github.com/OmarKanu96/Bellabeat-Case-Study-1/assets/127154130/36066e1e-8c88-4dfb-bf6b-36e8f3ecb6c3)

(https://public.tableau.com/views/BellabeatCaseStudy_17062359946690/Dashboard1?:language=en-US&:display_count=n&:origin=viz_share_link)

# Powerpoint Presentation 

(https://docs.google.com/presentation/d/1C0TBcV0gjxva3Zz0XdSAYC9BYwBmxEfKVk3GqETebaY/edit?usp=sharing)
