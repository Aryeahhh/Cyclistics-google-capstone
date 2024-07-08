# Google Capstone Project (Cyclistic)
I worked on the Google Data Analytics Capstone Projects involved a company named Cyclists, For this project I followed the steps of the data analysis process: Ask, Prepare, Process, Analyze, Share, and Act.
## Scenario
I am a junior data analyst working on the marketing analyst team at Cyclistic, a bike-share
company in Chicago. 

Cyclistic is a bike-share program that features more than 5,800 bicycles and 600 docking stations. Cyclistic sets itself apart by also offering reclining bikes, hand
tricycles, and cargo bikes, making bike-share more inclusive to people with disabilities and riders who can’t use a standard two-wheeled bike.The director of
marketing believes the company’s future success depends on maximizing the number of annual memberships. Therefore, your team wants to understand how casual riders and
annual members use Cyclistic bikes differently. 

Until now, Cyclistic’s marketing strategy relied on building general awareness and appealing to
broad consumer segments. One approach that helped make these things possible was the
flexibility of its pricing plans: single-ride passes, full-day passes, and annual memberships.
Customers who purchase single-ride or full-day passes are referred to as casual riders.
Customers who purchase annual memberships are Cyclistic members.

## Ask
Business Question: How do annual members and casual
riders use Cyclistic bikes differently?

Business Task: Devising a strategy to convert casual users to annual members.

Key Stakeholder: Lily Moreno, Director of Marketing.

## Prepare
I used Cyclist rides data from June 2023 to June 2024, this data has been licensed and made available by Motivate International Inc. 

There's also a data limitation as **data-privacy** issues
prohibit you from using riders’ personally identifiable information. This means that I won’t be
able to connect pass purchases to credit card numbers to determine if casual riders live in the
Cyclistic service area or if they have purchased multiple single passes.

The provided files have 13 columns of data in each specifying the Ride ID, Type of Bike, Start and End Times, Start and End Stations along with their IDs and Coordinates and it also includes the membership they currently own.

The data is stored on my Desktop and backed up on Google Drive.

## Process

I used the programming language R on RStudio to process the data, after observing all the files, the columns and data types seem to remain consistent across all files.

### Aggregating Data
I used the follow R code to aggregate all csv files in a single folder.
```
combined_data <- list.files(path="path to folder", full.names = TRUE) %>% 
  lapply(read_csv) %>% 
  bind_rows
```
### Removing NULL values
```
cleaned_data <- na.omit(combined_data)
```
### Creating ride_length Column
```
library(lubridate)
cleaned_data$started_at <- ymd_hms(cleaned_data$started_at)  
cleaned_data$ended_at <- ymd_hms(cleaned_data$ended_at)  
cleaned_data$duration <- as.numeric(difftime(cleaned_data$ended_at,cleaned_data$started_at, units = "mins"))
```
### Creating day_of_week Column
```
cleaned_data$day_of_week <- wday(cleaned_data$started_at,label= TRUE)
```
### Removing dupilicate rows
```
cleaned_data <- cleaned_data %>%
  distinct(ride_id, .keep_all = TRUE)
```
### Removing columns with data irrelevant to the analysis
```
cleaned_data <- subset(cleaned_data, select = -c(ride_id,start_station_id,end_station_id,start_lat,start_lng,end_lat,end_lng))
```

## Analyze
Comparing the userbase
![Percentage_of_users (1)](https://github.com/Aryeahhh/Cyclistics-google-capstone/assets/84890401/72a446cf-6d8a-45eb-81da-e3c5740c28a4)


We can observe that majority of the userbase seems to be members of the application, Members create substantially more revenue than casual riders, further efforts should be made to convert more casual users into members.

I wanted to analyze how members and casual users used the app differently, in doing so I compared usage on a variety of factors like, Number of rides per day of week, Rides per hour, Rides per month etc..

Looking at the average ride times.
![Dashboard 2](https://github.com/Aryeahhh/Cyclistics-google-capstone/assets/84890401/26b83d8a-a9a2-42fb-b4f9-e93d1f881328)
The data indicates that casual riders have significantly longer average ride durations compared to members. On average, casual riders' trips last about 23.90 minutes, while members' trips are shorter, averaging 12.53 minutes. This trend suggests that casual riders might be using bikes for leisurely rides or longer explorations, whereas members use them for shorter, more utilitarian trips.

Now looking at the usage over hours of the day and over the course of a week.
![Dashboard 3 (1)](https://github.com/Aryeahhh/Cyclistics-google-capstone/assets/84890401/f72ea742-f5e6-444e-a4ff-a86f0a999876)

The data shows that members predominantly use bikes for commuting, with sharp peaks in usage at 8 AM and 5 PM, indicating travel to and from work. Their bike usage remains consistently high during weekdays, reflecting regular commuting patterns, and slightly decreases on weekends. The highest usage peak occurs at 5 PM, aligning with the end of the workday.

In contrast, casual riders exhibit a different pattern, with a more even distribution of rides throughout the day and a slight increase in the afternoon between 2 PM and 4 PM. Their bike usage peaks on weekends, particularly on Saturday, and significantly drops during weekdays. This suggests that casual riders are more likely to use bikes for leisure activities rather than commuting.


![Rides_per_month](https://github.com/Aryeahhh/Cyclistics-google-capstone/assets/84890401/b5a2b2b4-96a5-42c1-a9d0-8faab755562d)

The above visualization shows that both casual and member riders exhibit a strong seasonal pattern, with peak usage in June (604,076 rides for members and 430,394 for casual riders) and lower activity in the colder months, especially December. Members consistently take more rides than casual riders throughout the year, indicating a more stable and engaged user base. While both groups see the highest number of rides in June, the decline for casual riders is sharper post-peak compared to the more gradual decline observed for members as the bikes are still used for commute.

![Rideable_type_per_month (1)](https://github.com/Aryeahhh/Cyclistics-google-capstone/assets/84890401/4d72cb79-11d4-4d01-b0d2-f0a351f16e5f)
The above visualization shows how different types of bikes are used throughout the year. Classic bikes are the most popular, with a peak of 654,939 rides in June. Their usage drops a lot in the colder months. Electric bikes also see their highest usage in June with 364,955 rides, but their decline is slower. Docked bikes are used the least, with a small peak of 17,830 rides in July. Overall, classic and electric bikes are used much more than docked bikes, especially in the summer.

## Act

### Recommendations
1. Seasonal Promotions should be run during peak usage months (e.g A discount for signing up during May or June)
2. Provide members with exclusive benefits such as priority bike access, free helmet rentals, or access to premium bikes. Enticing more casual users to switch to a membership, introducing a loyalty programme might also lead to a positive outcome.

