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
