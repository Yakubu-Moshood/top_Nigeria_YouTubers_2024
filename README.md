  # top_nigeria_youtubers_2024
This project provides an in-depth analysis of the top Nigerian YouTubers in 2024 based on key metrics such as total subscribers, video uploads, and total views. The dataset includes the top 100 channels, cleaned and structured for actionable insights.

# Table of Contents
- [Objective](#objective)
- [Data Source](#data-source)
- [Stages](#stages)
- [Design](#design)
  - [Mockup](#mockup)
  - [Tools](#tools)
- [Process](#process)
  - [Data Exploration](#data-exploration)
  - [Data Cleaning](#data-cleaning)
  - [Transform the Data](#transform-the-data)
  - [Create the SQL View](#create-the-sql-view)
- [Testing](#testing)
  - [Data Quality Tests](#data-quality-tests)
- [Visualization](#visualization)
  - [Results](#results)
  - [DAX Measures](#dax-measures)
- [Analysis](#analysis)
  - [Findings](#findings)
  - [Validation]()
  - [Discovery]()
- [Recommendations](#objective)
  - [Potential ROI]()
  - [Potential Courses of Actions]()
- [Conclusion]()

# Objective 
The Head of Marketing for a new fintech company is looking to explore partnerships with top Nigerian YouTubers in 2024 to drive impactful marketing campaigns throughout the coming year(s).

To identify the most influential creators, we need insights into the top YouTubers in Nigeria based on:

  - Subscriber Count: To gauge audience reach.
  - Total Views: To measure content performance.
  - Total Videos: To evaluate consistency and activity.
  - Engagement Metrics: To assess audience interaction and potential influence.
This project aims to deliver a data-driven dashboard to support the marketing team in making informed decisions.

# Data Source

The Dataset needed for this analysis has to include  

- channel names
- total subscribers
- total views
- total videos uploaded

The dataset was sourced from Social Blade and processed using ChatGPT to structure, and convert it into an Excel sheet. The source file can be found [here](https://socialblade.com/youtube/top/country/ng/mostsubscribed) 

# Stages
- Design
- Development
- Testing
- Analysis

# Design

Our dashboard must be designed in such a way that it would be able  to answer the following questions:

Who are the top 10 YouTubers with the most subscribers?
Which 3 channels have uploaded the most videos?
Which 3 channels have the most views?
Which 3 channels have the highest average views per video?
Which 3 channels have the highest views per subscriber ratio?
Which 3 channels have the highest subscriber engagement rate per video uploaded?

## Mockup
- The mockup allows us to visualize what our dashboard will look like before we get started building it.

![Dashboard-Mockup](https://github.com/Yakubu-Moshood/top_Nigeria_YouTubers_2024/blob/467f9888c7e42af6b7b7a787975210544440bcf8/mockup%20for%20dashboard.png)

 ## Tools

 - Excel	Exploring the data
 -  SQL Server	Cleaning, testing, and analyzing the data
 - Power BI	Visualizing the data via interactive dashboards
 - GitHub	Hosting the project documentation and version control
 - Mockup AI	Designing the wireframe/mockup of the dashboard

## Process 
The general approach to creating this project from the beginning till the end is:

- Get the data
- Explore the data in Excel
- Load the data into SQL Server
- Clean the data with SQL
- Test the data with SQL
- Visualize the data in Power BI
- Generate the findings based on the insights
- Write the documentation + commentary
- Publish the data to GitHub Pages

  
## Data Exploration 

This is the stage where I checked my data  for any errors, inconsistencies, bugs, weird and corrupted characters, etc. 
At least four columns contain the data we need for this analysis, which indicates that everything needed for this analysis was in the dataset; hence, the data from the source is sufficient for this analysis. 
I also noticed some additional columns which are not needed for the project, hence the need for them to be removed. Some column names also had to be changed 

## Data cleaning

The aim is to refine our dataset to ensure it is structured and ready for analysis.

The cleaned data should meet the following criteria and constraints:

- Only relevant columns should be retained.
- All data types should be appropriate for the contents of each column.
- No column should contain null values, indicating complete data for all records.

The steps needed to clean and shape the data into the desired format are

- 1. Remove unnecessary columns by only selecting the ones you need
- 2. Rename columns using aliases

## Transforming the Data

The data transformation was done in Power Query where the column headers were changed. 

## Testing

The data quality checks were carried out to ensure the integrity of the dataset we would be using for our analysis using SQL as shown below; 

### Data Testing 

#### Row Count Check: 
Count the total number of records (or rows) in the SQL view

 
```sql
SELECT 
COUNT(*) as no_of_row
FROM view_ng_youtubers2024;
```

- Output

![row_count_check](https://github.com/Yakubu-Moshood/top_Nigeria_YouTubers_2024/blob/18f21ff1ddc10e7e1ca2836438197b00cb753649/row_count_check_youtubenig.png)

#### Column Count Check
Count the total number of columns (or fields) are in the SQL view

```sql
SELECT COUNT(*) AS Column_count 
FROM INFORMATION_SCHEMA.COLUMNS 
WHERE TABLE_NAME = 'view_ng_youtubers2024';
```

![Column_Count_output](https://github.com/Yakubu-Moshood/top_Nigeria_YouTubers_2024/blob/main/columns%20checkyoutube.png?raw=true)

#### Data Type Check 
Check the data types of each column from the view by checking the INFORMATION SCHEMA view

```sql
SELECT COLUMN_NAME, DATA_TYPE
FROM INFORMATION_SCHEMA.COLUMNS 
WHERE TABLE_NAME = 'view_ng_youtubers2024';
```

![Data_type_check_output](https://github.com/Yakubu-Moshood/top_Nigeria_YouTubers_2024/blob/main/data_types_checksyoutube.png?raw=true)

#### Duplicate Count Check 
- 1. Check for duplicate rows in the view
- 2. Group by the channel name
- 3. Filter for groups with more than one row

```sql
SELECT channelname,
	COUNT(*) as duplicate_count
from view_ng_youtubers2024  
GROUP BY channelname
HAVING COUNT(*) > 1
```

![Duplicate_Count_Check](https://github.com/Yakubu-Moshood/top_Nigeria_YouTubers_2024/blob/main/duplicate_checksyoutube%20.png?raw=true)


## Visualization

- Result

![Dashboard](https://github.com/Yakubu-Moshood/top_Nigeria_YouTubers_2024/raw/refs/heads/main/github%20dashboard.mp4)


## DAX Measures

- Total Subscribers (M)
```DAX Measures
Total Subscribers (M) = 
 VAR million = 1000000
 VAR sumofSubscribers = SUM(view_ng_youtubers2024[total_Subscribers])
 VAR totalsubscribers = DIVIDE(sumofSubscribers,million)

 RETURN totalsubscribers
```

-  Total Views (B)
```DAX
Total Views (B) = 
VAR billion = 1000000000
VAR sumoftotalviews = sum(view_ng_youtubers2024[total_views])
VAR totalviews = DIVIDE(sumoftotalviews, billion)

RETURN totalviews
```

- Total Videos
```DAX
Total Videos = 
VAR totalvideos = SUM(view_ng_youtubers2024[total_videos])

RETURN totalvideos
```

- Average Views Per Video
```DAX
Avg ViewS Per Video (M) = 
VAR sumoftotalviews = sum(view_ng_youtubers2024[total_views])
VAR sumoftotalvideos = sum(view_ng_youtubers2024[total_videos])
VAR avgviewspervideo = DIVIDE(sumoftotalviews, sumoftotalvideos, BLANK())
VAR finalavgviewspervideo = DIVIDE(avgviewspervideo, 1000000, BLANK())

RETURN finalavgviewspervideo
```

- Subscribers Engagement Rate
```DAX
Subscribers Engagement Rate = 

VAR sumoftotalsubscribers = SUM(view_ng_youtubers2024[total_Subscribers])
VAR sumoftotalvideos = SUM(view_ng_youtubers2024[total_videos])
VAR SubscribersEngRate = DIVIDE(sumoftotalsubscribers, sumoftotalvideos, BLANK())

RETURN FORMAT(SubscribersEngRate, "#,##0K")
```

- Views Per Subscriber
```DAX
Views Per Subscriber = 
VAR sumoftotalviews = SUM(view_ng_youtubers2024[total_views])
VAR sumoftotalsubscribers = SUM(view_ng_youtubers2024[total_Subscribers])
VAR viewspersubscriber = DIVIDE(sumoftotalviews, sumoftotalsubscribers,BLANK())

RETURN FORMAT(viewspersubscriber, "#,##0K")
```

# Analysis 

- Findings
  
### 1. The Top 10 YouTubers by subscribers count 

![Top 10 most subscribed channel](https://github.com/Yakubu-Moshood/top_Nigeria_YouTubers_2024/blob/d59ab6f72450800d82d0edebb69d72184fdeb12a/Top%2010%20Youtubers%20by%20subscribers%20count.png)


###  2. The top 3 channels that have uploaded the most videos

![Top 3 channels based on video uploads](https://github.com/Yakubu-Moshood/top_Nigeria_YouTubers_2024/blob/d59ab6f72450800d82d0edebb69d72184fdeb12a/top%203%20by%20most%20videos%20upload.png)


### 3. The Top 3 channels with the most views

![Top 3 channels with most views](https://github.com/Yakubu-Moshood/top_Nigeria_YouTubers_2024/blob/d59ab6f72450800d82d0edebb69d72184fdeb12a/Most%20views%20top%203.png)


### 4. The Top 3 channels with the highest average views per video

![Top 3 highest average views per video](https://github.com/Yakubu-Moshood/top_Nigeria_YouTubers_2024/blob/d59ab6f72450800d82d0edebb69d72184fdeb12a/Average%20views%20per%20videos%20top%203.png)


### 5. The top 3 channels with the highest views per subscriber ratio

![Top 3 highest views per subscriber ratio](https://github.com/Yakubu-Moshood/top_Nigeria_YouTubers_2024/blob/d59ab6f72450800d82d0edebb69d72184fdeb12a/Views%20Per%20subscribers%20top%203.png)


### 6. The top 3 channels have the highest subscriber engagement rate per video uploaded

![Top 3 subscriber engagement rate per video uploaded](https://github.com/Yakubu-Moshood/top_Nigeria_YouTubers_2024/blob/d59ab6f72450800d82d0edebb69d72184fdeb12a/Subscribers%20Engagement%20Rate%20top%203.png)







