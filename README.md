Case Study 2 - How Can a Wellness Technology Company Play It Smart
================
Author: Jason LO
Latest Date of Update: 2022-08-23

## **Introduction**

This is one of the case studies in the [Google Data Analytics -
Professional
Certificate](https://www.coursera.org/professional-certificates/google-data-analytics?utm_source=gg&utm_medium=sem&utm_campaign=B2C_APAC_google-data-analytics_google_FTCOF_professional-certificates_HongKong&utm_content=B2C&campaignid=17960439291&adgroupid=139083671959&device=c&keyword=data%20science%20professional%20certificate&matchtype=b&network=g&devicemodel=&adpostion=&creativeid=615084577328&hide_mobile_promo&gclid=CjwKCAjwo_KXBhAaEiwA2RZ8hNOq3zg7NKnlFIHDmbMri_Ef4ykV3P9g3CvF4jOQ8BxSuWbG498hahoC81UQAvD_BwE).

## **ASK**

**Background**

Bellabeat is a high-tech manufacturer of health-focused products for
women since 2013. Bellabeat launched various health-focused products as
follows.

*Bellabeat app:* Provides health data related to the users’ activity,
sleep, stress, menstrual cycle, and mindfulness habits. This data can
help users better understand their current habits and make healthy
decisions. The Bellabeat app connects to their line of smart wellness
products.

*Leaf:* Bellabeat’s classic wellness tracker can be worn as a bracelet,
necklace, or clip. The Leaf tracker connects to the Bellabeat app to
track activity, sleep, and stress.

*Time:* A wellness watch combines the timeless look of a classic
timepiece with smart technology to track user activity, sleep, and
stress. The Time watch connects to the Bellabeat app to provide you with
insights into your daily wellness.

*Spring:* This is a water bottle that tracks daily water intake using
smart technology to ensure that you are appropriately hydrated
throughout the day. The Spring bottle connects to the Bellabeat app to
track your hydration levels.

*Bellabeat membership:* A subscription-based membership program for
users. Membership gives users 24/7 access to fully personalized guidance
on nutrition, activity, sleep, health and beauty, and mindfulness based
on their lifestyle and goals.

**Scenario**

As a junior data analyst working on the marketing analyst team at
Bellabeat, we have been asked to focus on one of Bellabeat’s products
and analyze smart device data to gain insight into how consumers are
using their smart devices. The insights you discover will then help
guide the marketing strategy for the company.

**Business Task**

Identify the trends in smart device usage

**Project Objective**

What are some trends in smart device usage?

How could these trends apply to Bellabeat customers?

How could these trends help influence Bellabeat marketing strategy?

**Key Stakeholders**

*Urška Sršen:* Bellabeat’s co-founder and Chief Creative Officer

*Sando Mur:* Mathematician and Bellabeat’s cofounder; a key member of
the Bellabeat executive team

*Bellabeat marketing analytics team:* A team of data analysts
responsible for collecting, analyzing, and reporting data that helps
guide Bellabeat’s marketing strategy.

## **PREPARE**

The case study will use non-Bellabeat data - [FitBit Fitness Tracker
Data](https://www.kaggle.com/datasets/arashnic/fitbit)

A good data source should meet the criteria below

**Reliable** - Only contained data from 30 eligible users, causing
insufficient data and confidence.

**Original** - Sourced from [Mobius](https://www.kaggle.com/arashnic),
not sure if the data came from the FitBit company or designated
organization

**Comprehensive** - Missing data in some columns, cannot acquire the
complete data from the record

**Current** - With 6 years of history, data may not be accurate

**Cited** - Data was generated by respondents to a distributed survey
and cited from a crowd-sourcing website - Amazon Mechanical Turk

Data is secured in an individual folder from a privately owned disk,
data will be analysed via RStudio.

## **PROCESS**

##### 1.1 Install and load packages

``` r
library(tidyverse) 
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.2 ──
    ## ✔ ggplot2 3.3.6     ✔ purrr   0.3.4
    ## ✔ tibble  3.1.7     ✔ dplyr   1.0.9
    ## ✔ tidyr   1.2.0     ✔ stringr 1.4.0
    ## ✔ readr   2.1.2     ✔ forcats 0.5.1
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

``` r
library(lubridate)
```

    ## 
    ## Attaching package: 'lubridate'

    ## The following objects are masked from 'package:base':
    ## 
    ##     date, intersect, setdiff, union

##### 1.2 Import .csv files

``` r
knitr::opts_knit$set(root.dir = "C:/Users/USER/Desktop/Case_Study_02/archive/Fitabase Data 4.12.16-5.12.16")
```

``` r
getwd()
```

    ## [1] "C:/Users/USER/Desktop/Case_Study_02/archive/Fitabase Data 4.12.16-5.12.16"

``` r
daily_activity <- read.csv("dailyActivity_merged.csv") 

sleep_day <- read.csv("sleepDay_merged.csv") 

weight_info <- read.csv("weightLogInfo_merged.csv")
```

##### 1.3 Observe the rows and columns

``` r
head(daily_activity) 
```

    ##           Id ActivityDate TotalSteps TotalDistance TrackerDistance
    ## 1 1503960366    4/12/2016      13162          8.50            8.50
    ## 2 1503960366    4/13/2016      10735          6.97            6.97
    ## 3 1503960366    4/14/2016      10460          6.74            6.74
    ## 4 1503960366    4/15/2016       9762          6.28            6.28
    ## 5 1503960366    4/16/2016      12669          8.16            8.16
    ## 6 1503960366    4/17/2016       9705          6.48            6.48
    ##   LoggedActivitiesDistance VeryActiveDistance ModeratelyActiveDistance
    ## 1                        0               1.88                     0.55
    ## 2                        0               1.57                     0.69
    ## 3                        0               2.44                     0.40
    ## 4                        0               2.14                     1.26
    ## 5                        0               2.71                     0.41
    ## 6                        0               3.19                     0.78
    ##   LightActiveDistance SedentaryActiveDistance VeryActiveMinutes
    ## 1                6.06                       0                25
    ## 2                4.71                       0                21
    ## 3                3.91                       0                30
    ## 4                2.83                       0                29
    ## 5                5.04                       0                36
    ## 6                2.51                       0                38
    ##   FairlyActiveMinutes LightlyActiveMinutes SedentaryMinutes Calories
    ## 1                  13                  328              728     1985
    ## 2                  19                  217              776     1797
    ## 3                  11                  181             1218     1776
    ## 4                  34                  209              726     1745
    ## 5                  10                  221              773     1863
    ## 6                  20                  164              539     1728

``` r
head(sleep_day) 
```

    ##           Id              SleepDay TotalSleepRecords TotalMinutesAsleep
    ## 1 1503960366 4/12/2016 12:00:00 AM                 1                327
    ## 2 1503960366 4/13/2016 12:00:00 AM                 2                384
    ## 3 1503960366 4/15/2016 12:00:00 AM                 1                412
    ## 4 1503960366 4/16/2016 12:00:00 AM                 2                340
    ## 5 1503960366 4/17/2016 12:00:00 AM                 1                700
    ## 6 1503960366 4/19/2016 12:00:00 AM                 1                304
    ##   TotalTimeInBed
    ## 1            346
    ## 2            407
    ## 3            442
    ## 4            367
    ## 5            712
    ## 6            320

``` r
head(weight_info) 
```

    ##           Id                  Date WeightKg WeightPounds Fat   BMI
    ## 1 1503960366  5/2/2016 11:59:59 PM     52.6     115.9631  22 22.65
    ## 2 1503960366  5/3/2016 11:59:59 PM     52.6     115.9631  NA 22.65
    ## 3 1927972279  4/13/2016 1:08:52 AM    133.5     294.3171  NA 47.54
    ## 4 2873212765 4/21/2016 11:59:59 PM     56.7     125.0021  NA 21.45
    ## 5 2873212765 5/12/2016 11:59:59 PM     57.3     126.3249  NA 21.69
    ## 6 4319703577 4/17/2016 11:59:59 PM     72.4     159.6147  25 27.45
    ##   IsManualReport        LogId
    ## 1           True 1.462234e+12
    ## 2           True 1.462320e+12
    ## 3          False 1.460510e+12
    ## 4           True 1.461283e+12
    ## 5           True 1.463098e+12
    ## 6           True 1.460938e+12

``` r
colnames(daily_activity) 
```

    ##  [1] "Id"                       "ActivityDate"            
    ##  [3] "TotalSteps"               "TotalDistance"           
    ##  [5] "TrackerDistance"          "LoggedActivitiesDistance"
    ##  [7] "VeryActiveDistance"       "ModeratelyActiveDistance"
    ##  [9] "LightActiveDistance"      "SedentaryActiveDistance" 
    ## [11] "VeryActiveMinutes"        "FairlyActiveMinutes"     
    ## [13] "LightlyActiveMinutes"     "SedentaryMinutes"        
    ## [15] "Calories"

``` r
colnames(sleep_day) 
```

    ## [1] "Id"                 "SleepDay"           "TotalSleepRecords" 
    ## [4] "TotalMinutesAsleep" "TotalTimeInBed"

``` r
colnames(weight_info) 
```

    ## [1] "Id"             "Date"           "WeightKg"       "WeightPounds"  
    ## [5] "Fat"            "BMI"            "IsManualReport" "LogId"

##### 1.4 Inspect the number of distinct ID users and data records

``` r
n_distinct(daily_activity$Id) 
```

    ## [1] 33

``` r
n_distinct(sleep_day$Id) 
```

    ## [1] 24

``` r
n_distinct(weight_info$Id) 
```

    ## [1] 8

**Found that there were 33 distinct users in daily activity which had
the most distinct users among the three records.**

**There were fewest users utilized fitness trackers for weighting.**

``` r
nrow(daily_activity) 
```

    ## [1] 940

``` r
nrow(sleep_day) 
```

    ## [1] 413

``` r
nrow(weight_info) 
```

    ## [1] 67

**There were 940 rows in daily activity.**

**Users tracked their daily activity mostly, least usage for
weighting.**

``` r
nrow(daily_activity)/n_distinct(daily_activity$Id)
```

    ## [1] 28.48485

``` r
nrow(sleep_day)/n_distinct(sleep_day$Id) 
```

    ## [1] 17.20833

``` r
nrow(weight_info)/n_distinct(weight_info$Id) 
```

    ## [1] 8.375

**In daily activity, each user utilized the fitness tracker 28 times,
while only 8 times per user in weighting.**

**Also, it is found that users on average measured their weights 8 times
a month.**

**To sum up, daily activity is one of the factors that most people will
usually use fitness trackers.**

#### 1.5 Check the data types

``` r
str(daily_activity)
```

    ## 'data.frame':    940 obs. of  15 variables:
    ##  $ Id                      : num  1.5e+09 1.5e+09 1.5e+09 1.5e+09 1.5e+09 ...
    ##  $ ActivityDate            : chr  "4/12/2016" "4/13/2016" "4/14/2016" "4/15/2016" ...
    ##  $ TotalSteps              : int  13162 10735 10460 9762 12669 9705 13019 15506 10544 9819 ...
    ##  $ TotalDistance           : num  8.5 6.97 6.74 6.28 8.16 ...
    ##  $ TrackerDistance         : num  8.5 6.97 6.74 6.28 8.16 ...
    ##  $ LoggedActivitiesDistance: num  0 0 0 0 0 0 0 0 0 0 ...
    ##  $ VeryActiveDistance      : num  1.88 1.57 2.44 2.14 2.71 ...
    ##  $ ModeratelyActiveDistance: num  0.55 0.69 0.4 1.26 0.41 ...
    ##  $ LightActiveDistance     : num  6.06 4.71 3.91 2.83 5.04 ...
    ##  $ SedentaryActiveDistance : num  0 0 0 0 0 0 0 0 0 0 ...
    ##  $ VeryActiveMinutes       : int  25 21 30 29 36 38 42 50 28 19 ...
    ##  $ FairlyActiveMinutes     : int  13 19 11 34 10 20 16 31 12 8 ...
    ##  $ LightlyActiveMinutes    : int  328 217 181 209 221 164 233 264 205 211 ...
    ##  $ SedentaryMinutes        : int  728 776 1218 726 773 539 1149 775 818 838 ...
    ##  $ Calories                : int  1985 1797 1776 1745 1863 1728 1921 2035 1786 1775 ...

``` r
str(sleep_day)
```

    ## 'data.frame':    413 obs. of  5 variables:
    ##  $ Id                : num  1.5e+09 1.5e+09 1.5e+09 1.5e+09 1.5e+09 ...
    ##  $ SleepDay          : chr  "4/12/2016 12:00:00 AM" "4/13/2016 12:00:00 AM" "4/15/2016 12:00:00 AM" "4/16/2016 12:00:00 AM" ...
    ##  $ TotalSleepRecords : int  1 2 1 2 1 1 1 1 1 1 ...
    ##  $ TotalMinutesAsleep: int  327 384 412 340 700 304 360 325 361 430 ...
    ##  $ TotalTimeInBed    : int  346 407 442 367 712 320 377 364 384 449 ...

``` r
str(weight_info)
```

    ## 'data.frame':    67 obs. of  8 variables:
    ##  $ Id            : num  1.50e+09 1.50e+09 1.93e+09 2.87e+09 2.87e+09 ...
    ##  $ Date          : chr  "5/2/2016 11:59:59 PM" "5/3/2016 11:59:59 PM" "4/13/2016 1:08:52 AM" "4/21/2016 11:59:59 PM" ...
    ##  $ WeightKg      : num  52.6 52.6 133.5 56.7 57.3 ...
    ##  $ WeightPounds  : num  116 116 294 125 126 ...
    ##  $ Fat           : int  22 NA NA NA NA 25 NA NA NA NA ...
    ##  $ BMI           : num  22.6 22.6 47.5 21.5 21.7 ...
    ##  $ IsManualReport: chr  "True" "True" "False" "True" ...
    ##  $ LogId         : num  1.46e+12 1.46e+12 1.46e+12 1.46e+12 1.46e+12 ...

**Found that the data type of activity date and sleep day is a
character, it is needed to change them into a date-time format for
further analysis.**

#### 1.6 Change the data type of the activity date column from character to date format

``` r
daily_activity$ActivityDate <- mdy(daily_activity$ActivityDate)
```

#### 1.7 Duplicate the activity date column to a new data set

``` r
ActDay <- daily_activity %>% select(ActivityDate)
```

#### 1.8 Distinguish the weekdays from the activity date

``` r
ActDay$weekday <- weekdays(as.Date(ActDay$ActivityDate))
```

#### 1.9 Arrange the weekday in order from Monday to Sunday

``` r
ActDay$weekday <- factor(ActDay$weekday, 
              levels = c("Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday")) 
```

#### 1.10 Change the data type of sleep day column from character to date format

``` r
sleep_day$SleepDay <- mdy_hms(sleep_day$SleepDay)
```

#### 1.11 Duplicate the sleep day column to a new data set

``` r
SlpDay <- sleep_day %>% select(SleepDay)
```

#### 1.12 Distinguish the weekdays from the sleep day

``` r
SlpDay$weekday <- weekdays(as.Date(SlpDay$SleepDay))
```

#### 1.13 Arrange the weekday in order from Monday to Sunday

``` r
SlpDay$weekday <- factor(SlpDay$weekday, 
              levels = c("Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday")) 
```

## **ANALYZE**

#### 2.1 Choose and summarize the selected columns

``` r
#Summarize daily activity

daily_activity %>%   
  
  select(TotalSteps, 
         
         VeryActiveMinutes,
         
         FairlyActiveMinutes,
         
         LightlyActiveMinutes,
         
         SedentaryMinutes, 
         
         Calories) %>% 
  
  summary()
```

    ##    TotalSteps    VeryActiveMinutes FairlyActiveMinutes LightlyActiveMinutes
    ##  Min.   :    0   Min.   :  0.00    Min.   :  0.00      Min.   :  0.0       
    ##  1st Qu.: 3790   1st Qu.:  0.00    1st Qu.:  0.00      1st Qu.:127.0       
    ##  Median : 7406   Median :  4.00    Median :  6.00      Median :199.0       
    ##  Mean   : 7638   Mean   : 21.16    Mean   : 13.56      Mean   :192.8       
    ##  3rd Qu.:10727   3rd Qu.: 32.00    3rd Qu.: 19.00      3rd Qu.:264.0       
    ##  Max.   :36019   Max.   :210.00    Max.   :143.00      Max.   :518.0       
    ##  SedentaryMinutes    Calories   
    ##  Min.   :   0.0   Min.   :   0  
    ##  1st Qu.: 729.8   1st Qu.:1828  
    ##  Median :1057.5   Median :2134  
    ##  Mean   : 991.2   Mean   :2304  
    ##  3rd Qu.:1229.5   3rd Qu.:2793  
    ##  Max.   :1440.0   Max.   :4900

**The mean of total steps was 7638, less than the [recommended daily
steps of 10,000
steps.](https://www.thelancet.com/journals/lanpub/article/PIIS2468-2667(21)00302-9/fulltext)**

**The fairly and very active minutes were not sufficient as
recommended**

*For the young population, it is recommended to do [at least 60 minutes
of moderate-to-vigorous physical activity in a
day.](https://health.gov/sites/default/files/2019-09/Physical_Activity_Guidelines_2nd_edition.pdf)*

*For adults, the suggested moderate-intensity activity is [at least 150
minutes to 300 minutes a week or 75 minutes a week for
vigorous-intensity physical
activity.](https://health.gov/sites/default/files/2019-09/Physical_Activity_Guidelines_2nd_edition.pdf)*

*The mean of very active minutes would reach the adult suggestion (75
minutes a week for vigorous-intensity physical activity) if the users
maintain the record for 7 days/week.*

*But most of the users could not meet the recommendations of both
adolescence and adult as over half of them were below the median of very
active minutes (4 minutes/day) and fairly active minutes (6
minutes/day).*

**Sedentary time was too long as per suggested**

*Sedentary hours with [more than 9 hours a day will increase the risk of
mortality.](https://bmcmedicine.biomedcentral.com/articles/10.1186/s12916-018-1062-2)*

*Users on average had 991.2 sedentary minutes (same as 16.52 hours) per
day which was out of the recommended hours.*

**Overall, users took more time being sedentary than being active.**

``` r
#Summarize sleep day

sleep_day %>%   
  
  select(TotalSleepRecords, 
         
         TotalMinutesAsleep, 
         
         TotalTimeInBed) %>% 
  
  summary() 
```

    ##  TotalSleepRecords TotalMinutesAsleep TotalTimeInBed 
    ##  Min.   :1.000     Min.   : 58.0      Min.   : 61.0  
    ##  1st Qu.:1.000     1st Qu.:361.0      1st Qu.:403.0  
    ##  Median :1.000     Median :433.0      Median :463.0  
    ##  Mean   :1.119     Mean   :419.5      Mean   :458.6  
    ##  3rd Qu.:1.000     3rd Qu.:490.0      3rd Qu.:526.0  
    ##  Max.   :3.000     Max.   :796.0      Max.   :961.0

**Enough sleep time**

*Humans should have [at least 7 hours of sleeping time a
day.](https://cdnsciencepub.com/doi/10.1139/apnm-2020-0034)*

*The mean of total minutes asleep was 419.5 minutes which equals around
7 hours.*

**Fitness tracker users on average had sufficient sleeping time.**

``` r
#Summarize weight information

weight_info %>%   
  
  select(Fat, 
         
         BMI) %>% 
  
  summary() 
```

    ##       Fat             BMI       
    ##  Min.   :22.00   Min.   :21.45  
    ##  1st Qu.:22.75   1st Qu.:23.96  
    ##  Median :23.50   Median :24.39  
    ##  Mean   :23.50   Mean   :25.19  
    ##  3rd Qu.:24.25   3rd Qu.:25.56  
    ##  Max.   :25.00   Max.   :47.54  
    ##  NA's   :65

**Users have an issue of being overweight**

*The normal BMI range is [18.5 kg/m² to 24.9
kg/m².](https://www.nhs.uk/common-health-questions/lifestyle/what-is-the-body-mass-index-bmi/)*

*The mean BMI of the users was 25.19 kg/m².*

**Users tended to have overweight and obesity problems as the maximum
BMI was 47.54 kg/m².**

#### 2.2 Usage frequency in different activities

``` r
#Export the bar chart to find the tracker usage trend in daily activity

ggplot(ActDay, aes(x=weekday, fill=weekday)) + geom_bar() + 
  labs(x = "Weekday", y = "Number of Usage") + ggtitle("Usage Frequency of FitBit Fitness Tracker in Daily Activity")
```
![image](https://user-images.githubusercontent.com/100983196/186110704-ab0e659f-99d3-4633-af24-5e772ff7cf3c.png)

*It recorded a high usage number of FitBit Fitness Tracker on Tuesday,
Wednesday and Thursday, with around 150 users per day.*

**It implies users tracked their daily activities on weekdays instead of
weekends.**

``` r
#Export the bar chart to find the usage trend when sleeping

ggplot(SlpDay, aes(x=weekday, fill=weekday)) + geom_bar() + 
  labs(x = "Weekday", y = "Number of Usage") + ggtitle("Usage Frequency of FitBit Fitness Tracker During Sleep Time")
```

![image](https://user-images.githubusercontent.com/100983196/186110674-faa495d3-331e-4a98-8c16-43adf15562a1.png)

*There were sufficiently high usage numbers of FitBit Fitness Tracker on
Tuesday, Wednesday and Thursday, only these three days were over 60
users per day.*

**It means users tracked their sleeping activities on weekdays instead
of weekends.**

**All in all, there was a situation where users mainly utilized the
fitness trackers on weekdays more than weekends whenever in the daytime
or sleeping.**

#### 2.3 Correaltions among variables

``` r
#Correlation between total steps and calories

ggplot(data= daily_activity, aes(x=TotalSteps, y=Calories)) + geom_point() +
  labs(x = "TotalSteps", y = "Calories Consumed") + ggtitle("Total Steps to Calories Consumption")
```

![image](https://user-images.githubusercontent.com/100983196/186110588-622993f4-7072-4987-8415-5c239da22e23.png)

*The outliers are mainly located in the bottom left corner, showing that
0 total steps but some calories were consumed, maybe owing to other
movements or actions.*

**A positive correlation occurred, which means taking more steps may
burn more calories.**

``` r
#Correlation among very active minutes, fairly active minutes, sedentary minutes and calories

ggplot(data= daily_activity) + geom_point(aes(x=VeryActiveMinutes, y=Calories, color = "Very Active")) + 
  geom_point(aes(x=FairlyActiveMinutes, y=Calories, color = "Fairly Active"))+ 
  geom_point(aes(x=SedentaryMinutes, y=Calories, color = "Sedentary Active")) + 
  scale_color_manual(values = c("Very Active" = "red", "Fairly Active" = "yellow", "Sedentary Active" = "blue")) +
  labs(x = "Active Minutes", y = "Calories") + ggtitle("Active Minutes to Calories")
```

![image](https://user-images.githubusercontent.com/100983196/186110527-1c9817c7-8464-451a-86dd-4e136c140368.png)

*Very active minutes and fairly active minutes had similar results,
users took shorter time when having moderate to high intensive
activities compared to sedentary minutes.*

*There is an implication that moderate to high intensive activities may
burn the same amount of calories in fewer minutes than being sedentary.*

**Moderate to high intensive activities may be more efficient to burn
calories compared to inactivity.**

``` r
#Correlation amid total minutes asleep and total time in bed

ggplot(data= sleep_day, aes(x=TotalMinutesAsleep, y=TotalTimeInBed)) + geom_point() + geom_smooth(formula = y ~ x, method = "loess") +
  labs(x = "Total Minutes Asleep", y = "Total Time In Bed") + ggtitle("Total Minutes Asleep to Total Time In Bed")
```

![image](https://user-images.githubusercontent.com/100983196/186110427-7035a044-c915-498e-bef6-94dcdc3255aa.png)

*Total minutes asleep was highly positive correlated to total time in
bed while some outliers existed.*

*The sleeping time was not directly proportioned to the total time in
bed from most of the outliers.*

**It implies some users mighty take longer time in bed but not
sleeping.**

``` r
#Correlation between weight in Kg and BMI

ggplot(data= weight_info, aes(x=WeightKg, y=BMI)) + geom_point() + 
  labs(x = "Weight in Kg", y = "BMI") + ggtitle("Weight to BMI")
```

![image](https://user-images.githubusercontent.com/100983196/186110145-19aff396-fe33-4933-a085-d8fea347ccc5.png)

*They were not closely related, BMI may be affected by many factors such
as height.*

*Users with high BMI (\>24.9 kg/m²) were at least weighted over 65KG but
the [normal BMI range is 18.5 kg/m² to 24.9
kg/m².](https://www.nhs.uk/common-health-questions/lifestyle/what-is-the-body-mass-index-bmi/)*

**It is a reference to remind users to keep checking their BMI and
weight to maintain health.**

## **SHARE & ACT**

**3.1 Most frequent usage on daily activity**

Users always tracked their total steps taken, calories consumed,
activity time and others on daily activity. It is found that they had
exceeded sedentary time than active time according to the
recommendations.

*3.1.1 Set up active reminder*

An active reminder can encourage users to have more active time rather
than continuously being sedentary. It can remind users to keep moving,
for example, go for a walk or stretch when sitting for a long time.

**3.2 High usages on weekdays**

Apart from the daily activity records, users with fitness trackers also
traced their sleeping time on weekdays rather than at weekends. It may
be because they wanted to know their health records on daily routines
such as working or studying. But they may neglect the records at
weekends so it happened lower usages on Saturday and Sunday.

*3.2.1 Set up daily goals*

A daily health task will motivate users to be more active. With more
intense objectives for users at weekends or holidays, they will have
balance health records on weekdays and at weekends. It will ensure users
will have a constant daily records of activity and sleep time.

**3.3 Lowest usages on weighting**

Among the daily activity, sleep quality and weighing, there were fewest
people use fitness trackers to measure body weight and BMI. But from
those records, some of the users were out of the BMI’s normal range. It
is found that people with overweight and obesity had heavier body
weights. This will trigger chains of health issues.

*3.3.1 Customize body control plan*

[There are many factors affecting body weight and
BMI.](https://www.niddk.nih.gov/health-information/weight-management/adult-overweight-obesity/factors-affecting-weight-health)
Bellabeat can tailor-make a personal fitness plan for users according to
their weight and BMI. Users then can be suggested to start from their
daily activity, for instance, how much moderate to high intense
exercising time they should have, how many calories they should consume,
how many steps they should take, when they should sleep when in bed,
etc. They should be recommended to measure weight and BMI periodically
to record their progress. In this way, users should be acknowledged that
every movement and habit will affect their weight and health.
