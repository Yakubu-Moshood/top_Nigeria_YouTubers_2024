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

For the row count; 
- Input Query

  ``` sql
  
SELECT 
COUNT(*) as no_of_row
FROM [top_ng_youtubers_2024].[dbo].[view_ng_youtubers2024];

```

- Output
![row_count_check](https://github.com/Yakubu-Moshood/top_Nigeria_YouTubers_2024/blob/18f21ff1ddc10e7e1ca2836438197b00cb753649/row_count_check_youtubenig.png)



