[output.docx](https://github.com/PAIonela/paionela.github.io-/files/10375550/output.docx)
# paionela.github.io- Cyclistic bike
Create repository.
---
output:
  word_document: default
  pdf_document: default
  html_document: default
---
---
title: "Case study"
author: "Alina"
date: "2022-12-10"
output: html_document

### Introdution

For the capstone project of the Google Data Analytics certificate, I have chosen the Cyclistic bike share data to work on. For the case study, 
To answer key business questions, I will follow the six steps of the data analysis process : Ask, Prepare, Process, Analyze, Share and Act.


### The scenario

The director of marketing of Cyclistic, Lily Moreno, believes that the company’s future growth depends on maximizing the number of annual memberships. Hence, the marketing analyst team wants to understand how casual riders and annual members use Cyclistic bikes differently. From these insights, the analytics team could be able to design a new marketing strategy to convert casual riders into annual members. 

Three questions will guide the future marketing campaign:

1.How do annual members and casual riders use Cyclistic bikes differently?

2.Why would casual riders buy Cyclistic annual memberships?

3.How can Cyclistic use digital media to influence casual riders to become members?

I have been assigned by Moreno the first question. 


### The Ask phase

* A statement of the business task: 

Moreno has set a clear goal: Design marketing strategies aimed at converting casual riders into annual members

* My key stakeholders are: 

1-Lily Moreno: The director of marketing and my manager.

2-The executive team: The executive team must approve our recommendations

### The Prepare phase

Data Source: 
Previous 12 months of original bike share data set from 10/01/2021 to 09/01/2022 was extracted as 12 zipped .csv  TThe data has been made available by
Motivate International Inc. under this [license](https://ride.divvybikes.com/data-license-agreement).

How is the data organized:
- I create subfolders for the .CSV file and the .XLS or Sheets file so that I  have a copy of the original data, and I move the downloaded files to the appropriate subfolder

Are there issues with bias or credibility in this data? Does your data ROCCC:
The data seem to apply the ROCCC requirements, they are reliable, complete and accurate, are original- are the property of Cyclistic, are comprehensive- I will focus about the previous 12 months of Cyclistic (october 2021- september 2022) trip data, but the dataset record gost bat to 2009. The data are Current- I will use the data of the last 1 months, and the data are cited I work with the data generated from Cyclistic’s.
How are you addressing licensing, privacy, security, and accessibility:
- I store the data in my local desktop, and I don’t share the data. I just use for analys and use for visualization.
How did you verify the data’s integrity:
All the files have consistent columns and each column has the correct type of data
How does it help you answer your question:
The data contain the informationa about the riders and their riding style
Are there any problems with the data:
- in some of the data are missing the stations names ans IDs


###Process Guiding questions:
What tools are you choosing and why:
- for the start I choos Excel- for the first instructions recommended, and tjen I will use the RStudio, because it can process a large volume of data

### The Analyze Phase
#### Setting up the environment

I use multiple packages and libraries

```{r libraries, echo=TRUE, eval=TRUE}
library(tidyverse)
library(janitor)
library(skimr)
library(readr)
library(plyr)
library(dplyr)
library(lubridate)
library(ggplot2)
```
#### Importing data 
Cyclist data from 10/2021 until 09/2022 is imported and read as csv. files. 

```{r csv data collection, echo=TRUE, eval=FALSE}
data_01 <- read_csv("202110-divvy-tripdata.csv")
data_02 <- read_csv("202111-divvy-tripdata.csv")
data_03 <- read_csv("202112-divvy-tripdata.csv")
data_04 <- read_csv("202201-divvy-tripdata.csv")
data_05 <- read_csv("202202-divvy-tripdata.csv")
data_06 <- read_csv("202203-divvy-tripdata.csv")
data_07 <- read_csv("202204-divvy-tripdata.csv")
data_08 <- read_csv("202205-divvy-tripdata.csv")
data_09 <- read_csv("202206-divvy-tripdata.csv")
data_10 <- read_csv("202207-divvy-tripdata.csv")
data_11 <- read_csv("202208-divvy-tripdata.csv")
data_12 <- read_csv("202209-divvy-tripdata.csv")
```
# Compare column names each of the files
# While the names don't have to be in the same order, they DO need to match perfectly before we can use a command to join them into one file

```{r colname inspection, echo=TRUE, eval=TRUE}
colnames(data_01)
colnames(data_02)
colnames(data_04)
colnames(data_05)
colnames(data_06)
colnames(data_07)
colnames(data_08)
colnames(data_09)
colnames(data_10)
colnames(data_11)
colnames(data_12)
```
# Rename columns  to make them consistent 
```{r rename, echo=TRUE, eval=TRUE}
(data_01<- rename(data_01
                        ,trip_id=ride_id
                        ,bikeid=rideable_type
                        ,start_time=started_at
                        ,end_time=ended_at
                        ,from_station_name=start_station_name
                        ,from_station_id=start_station_id
                        ,to_station_name=end_station_name
                        ,to_station_id=end_station_id
                        ,usertype=member_casual))

(data_02<- rename(data_02
                  ,trip_id=ride_id
                  ,bikeid=rideable_type
                  ,start_time=started_at
                  ,end_time=ended_at
                  ,from_station_name=start_station_name
                  ,from_station_id=start_station_id
                  ,to_station_name=end_station_name
                  ,to_station_id=end_station_id
                  ,usertype=member_casual))

(data_03<- rename(data_03
                  ,trip_id=ride_id
                  ,bikeid=rideable_type
                  ,start_time=started_at
                  ,end_time=ended_at
                  ,from_station_name=start_station_name
                  ,from_station_id=start_station_id
                  ,to_station_name=end_station_name
                  ,to_station_id=end_station_id
                  ,usertype=member_casual))

(data_04<- rename(data_04
                  ,trip_id=ride_id
                  ,bikeid=rideable_type
                  ,start_time=started_at
                  ,end_time=ended_at
                  ,from_station_name=start_station_name
                  ,from_station_id=start_station_id
                  ,to_station_name=end_station_name
                  ,to_station_id=end_station_id
                  ,usertype=member_casual))

(data_05<- rename(data_05
                  ,trip_id=ride_id
                  ,bikeid=rideable_type
                  ,start_time=started_at
                  ,end_time=ended_at
                  ,from_station_name=start_station_name
                  ,from_station_id=start_station_id
                  ,to_station_name=end_station_name
                  ,to_station_id=end_station_id
                  ,usertype=member_casual))

(data_06<- rename(data_06
                  ,trip_id=ride_id
                  ,bikeid=rideable_type
                  ,start_time=started_at
                  ,end_time=ended_at
                  ,from_station_name=start_station_name
                  ,from_station_id=start_station_id
                  ,to_station_name=end_station_name
                  ,to_station_id=end_station_id
                  ,usertype=member_casual))

(data_07<- rename(data_07
                  ,trip_id=ride_id
                  ,bikeid=rideable_type
                  ,start_time=started_at
                  ,end_time=ended_at
                  ,from_station_name=start_station_name
                  ,from_station_id=start_station_id
                  ,to_station_name=end_station_name
                  ,to_station_id=end_station_id
                  ,usertype=member_casual))

(data_08<- rename(data_08
                  ,trip_id=ride_id
                  ,bikeid=rideable_type
                  ,start_time=started_at
                  ,end_time=ended_at
                  ,from_station_name=start_station_name
                  ,from_station_id=start_station_id
                  ,to_station_name=end_station_name
                  ,to_station_id=end_station_id
                  ,usertype=member_casual))

(data_09<- rename(data_09
                  ,trip_id=ride_id
                  ,bikeid=rideable_type
                  ,start_time=started_at
                  ,end_time=ended_at
                  ,from_station_name=start_station_name
                  ,from_station_id=start_station_id
                  ,to_station_name=end_station_name
                  ,to_station_id=end_station_id
                  ,usertype=member_casual))

(data_10<- rename(data_10
                  ,trip_id=ride_id
                  ,bikeid=rideable_type
                  ,start_time=started_at
                  ,end_time=ended_at
                  ,from_station_name=start_station_name
                  ,from_station_id=start_station_id
                  ,to_station_name=end_station_name
                  ,to_station_id=end_station_id
                  ,usertype=member_casual))

(data_11<- rename(data_11
                  ,trip_id=ride_id
                  ,bikeid=rideable_type
                  ,start_time=started_at
                  ,end_time=ended_at
                  ,from_station_name=start_station_name
                  ,from_station_id=start_station_id
                  ,to_station_name=end_station_name
                  ,to_station_id=end_station_id
                  ,usertype=member_casual))

(data_12<- rename(data_12
                  ,trip_id=ride_id
                  ,bikeid=rideable_type
                  ,start_time=started_at
                  ,end_time=ended_at
                  ,from_station_name=start_station_name
                  ,from_station_id=start_station_id
                  ,to_station_name=end_station_name
                  ,to_station_id=end_station_id
                  ,usertype=member_casual))
```

# Inspect the dataframes and look for incongruencies
```{r inspect, echo=TRUE, eval=TRUE}
str(data_01)
str(data_02)
str(data_03)
str(data_04)
str(data_05)
str(data_06)
str(data_07)
str(data_08)
str(data_09)
str(data_10)
str(data_11)
str(data_12)
```
# Convert ride_id and rideable_type to character so that they can stack correctly
```{r convert, echo=TRUE, eval=TRUE}
data_01 <-  mutate(data_01, trip_id = as.character(trip_id)
                   ,bikeid = as.character(bikeid))
data_02 <-  mutate(data_02, trip_id = as.character(trip_id)
                   ,bikeid = as.character(bikeid))
data_03 <-  mutate(data_03, trip_id = as.character(trip_id)
                   ,bikeid = as.character(bikeid))
data_04 <-  mutate(data_04, trip_id = as.character(trip_id)
                   ,bikeid = as.character(bikeid))
data_05 <-  mutate(data_05, trip_id = as.character(trip_id)
                   ,bikeid = as.character(bikeid))
data_06 <-  mutate(data_06, trip_id = as.character(trip_id)
                   ,bikeid = as.character(bikeid))
data_07 <-  mutate(data_07, trip_id = as.character(trip_id)
                   ,bikeid = as.character(bikeid))
data_08 <-  mutate(data_08, trip_id = as.character(trip_id)
                   ,bikeid = as.character(bikeid))
data_09 <-  mutate(data_09, trip_id = as.character(trip_id)
                   ,bikeid = as.character(bikeid))
data_10 <-  mutate(data_10, trip_id = as.character(trip_id)
                   ,bikeid = as.character(bikeid))
data_11 <-  mutate(data_11, trip_id = as.character(trip_id)
                   ,bikeid = as.character(bikeid))
data_12 <-  mutate(data_12, trip_id = as.character(trip_id)
                   ,bikeid = as.character(bikeid))
```
# Stack individual quarter's data frames into one big data frame
```{r stacking the datasets , echo=TRUE, eval=TRUE}
all_trips <- bind_rows(data_01, data_02, data_03, data_04, data_05, data_06, data_07, data_08, data_09, data_10, data_11, data_12)
```
# Remove lat, long, birthyear, and gender fields as this data was dropped beginning in 2021
```{r all_trips remove lat, long, birthyear and gender, echo=TRUE, eval=TRUE}
all_trips <- all_trips %>%  
  select(-c(start_lat, start_lng, end_lat, end_lng))
```
####  Clean up and organize data to prepare for analysis
# Inspect the new table that has been created
```{r all_trips inspection, echo=TRUE, eval=TRUE}
colnames(all_trips)
nrow(all_trips)
dim(all_trips) 
head(all_trips)
tail(all_trips)
str(all_trips)
summary(all_trips)
table(all_trips$usertype)
```
# There are a few problems we will need to fix
# Reassign to the desired values (we will go with the current 2021-2022 labels)
```{r reassign, echo=TRUE, eval=TRUE}
all_trips <-  all_trips %>% 
  mutate(usertype = recode(usertype
                                ,"Subscriber" = "usertype"
                                ,"Customer" = "usertype"))
```
# Check to make sure the proper number of observations were reassigned
```{r reassign, echo=TRUE, eval=TRUE}
table(all_trips$usertype)
```
# Add columns that list the date, month, day, and year of each ride
```{r separting ride date and extracting date data, echo=TRUE, eval=TRUE}
all_trips$date <- as.Date(all_trips$start_time) 
all_trips$month <- format(as.Date(all_trips$date), "%m")
all_trips$day <- format(as.Date(all_trips$date), "%d")
all_trips$year <- format(as.Date(all_trips$date), "%Y")
all_trips$day_of_week <- format(as.Date(all_trips$date), "%A")
```
# Add a "ride_length" calculation to all_trips (in seconds)
```{r calulate the ride_length in secs, echo=TRUE, eval=TRUE}
all_trips$ride_length <- difftime(all_trips$end_time,all_trips$start_time)
```
# Inspect the structure of the columns
```{r data inspection, echo=TRUE, eval=TRUE}
str(all_trips)
```
# Convert "ride_length" from Factor to numeric so we can run calculations on the data
```{r converting variables to numeric, echo=TRUE, eval=TRUE}
is.factor(all_trips$ride_length)
all_trips$ride_length <- as.numeric(as.character(all_trips$ride_length))
is.numeric(all_trips$ride_length)
```
# Remove "bad" data
# The dataframe includes a few hundred entries when bikes were taken out of docks and checked for quality by Divvy or ride_length was negative
# We will create a new version of the dataframe (v2) since data is being removed
```{r droppig rows, echo=TRUE, eval=TRUE}
all_trips_v2 <- all_trips[!(all_trips$from_station_name == "HQ QR" | all_trips$ride_length<0),]
```
####CONDUCT DESCRIPTIVE ANALYSIS
# Descriptive analysis on ride_length (all figures in seconds)
```{r decriptive analysis, echo=TRUE, eval=TRUE}
mean(all_trips_v2$ride_length) 
median(all_trips_v2$ride_length)
max(all_trips_v2$ride_length)
min(all_trips_v2$ride_length)  
```
# You can condense the four lines above to one line using summary() on the specific attribute
```{r condense, echo=TRUE, eval=TRUE}
summary(all_trips_v2$ride_length)
```
# Compare members and casual users
```{r compare, echo=TRUE, eval=TRUE}
aggregate(all_trips_v2$ride_length ~ all_trips_v2$usertype, FUN = mean)
aggregate(all_trips_v2$ride_length ~ all_trips_v2$usertype, FUN = median)
aggregate(all_trips_v2$ride_length ~ all_trips_v2$usertype, FUN = max)
aggregate(all_trips_v2$ride_length ~ all_trips_v2$usertype, FUN = min)
```
# See the average ride time by each day for members vs casual users
```{r average ride time, echo=TRUE, eval=TRUE}
aggregate(all_trips_v2$ride_length ~ all_trips_v2$usertype + all_trips_v2$day_of_week, FUN = mean)
```

# Notice that the days of the week are out of order. Let's fix that.
```{r fix, echo=TRUE, eval=TRUE}
all_trips_v2$day_of_week <- ordered(all_trips_v2$day_of_week, levels=c("Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"))
```
# Now, let's run the average ride time by each day for members vs casual users
```{r run, echo=TRUE, eval=TRUE}
aggregate(all_trips_v2$ride_length ~ all_trips_v2$usertype + all_trips_v2$day_of_week, FUN = mean)
```
# analyze ridership data by type and weekday
```{r ridership data by type and weekday, echo=TRUE, eval=TRUE}
all_trips_v2 %>%
  mutate(weekday = wday(start_time, label = TRUE)) %>% 
  group_by(usertype, weekday) %>%
  summarise(number_of_rides = n()
            ,average_duration = mean(ride_length)) %>%
  arrange(usertype, weekday)	
```
# Let's visualize the number of rides by rider type
```{r plot- the number of rides by rider type, echo=TRUE, eval=TRUE}
all_trips_v2 %>%
  mutate(weekday = wday(start_time, label = TRUE)) %>% 
  group_by(usertype, weekday) %>% 
  summarise(number_of_rides = n())
            ,average_duration = mean(ride_length)) %>% 
  arrange(usertype, weekday)  %>%
  ggplot(aes(x = weekday, y = number_of_rides, fill = usertype)) +
  geom_col(position ="dodge")
```
# Let's create a visualization for average duration
```{r plot- visualization for average duration, echo=TRUE, eval=TRUE}
all_trips_v2 %>% 
  mutate(weekday = wday(start_time, label = TRUE)) %>%
  group_by(usertype, weekday) %>% 
  summarise(number_of_rides = n()
            ,average_duration = mean(ride_length)) %>% 
  arrange(usertype, weekday)  %>%
  ggplot(aes(x = weekday, y = average_duration, fill = usertype)) +
  geom_col(position = "dodge")
```
###EXPORT SUMMARY FILE FOR FURTHER ANALYSIS
```{r export csv, echo=TRUE, eval=TRUE}
counts <- aggregate(all_trips_v2$ride_length ~ all_trips_v2$usertype + all_trips_v2$day_of_week, FUN = mean)
write.csv(counts, file = "C:/Users/Alina/Desktop/Divvy_Exercise/cvs/avg_ride_length.csv")
```

### The Share phase 

#### Conclusion
The average ride duration is higher for casual riders for any day of the week.
Number of ride is higher for the member all of the week.

###Recommendations
Based on the average duration the casual member rewarded with benefits such as discount vouchers 50% reduction for the first mounth.
Consider introducing a monthly or weekly pass as casual riders might not want to be tied down to an annual subscription.
