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
  - [Validation](#validation)
  - [Discovery](#discovery)
- [Recommendations](#recommendations)
  - [Potential ROI](#potential-roi)
  - [Potential Courses of Actions](#potential-courses-of-actionns)
- [Conclusion](#conclusion)

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
- The mockup allows us to visualize our dashboard's appearance before we start building it.

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


### Validation

#### 1.	Youtubers with the most subscribers

a. **MarkAngelComedy**

Calculation breakdown
Campaign idea = product placement
•	Average views per video = 2.20 million
•	Product cost = $5
•	Potential units sold per video = 2.20 million x 2% conversion rate = 44,000 units sold
•	Potential revenue per video = 44,000 x $5 = 220,000
•	Campaign cost (one-time fee) = $50,000
•	Net profit =$220,000 - $50,000 = $170,000

b. **Agbaps Shorts**

•	Average views per video = 5.26 million
•	Product cost = $5
•	Potential units sold per video = 5.26 million x 2% conversion rate = 105,200 units sold
•	Potential revenue per video = 105,200 x $5 = $526,000
•	Campaign cost (one-time fee) = $50,000
•	Net profit = $526,000 - $50,000 = $476,000

c. **Rema**

•	Average views per video = 11.57 million
•	Product cost = $5
•	Potential units sold per video = 11.57 million x 2% conversion rate = 231,400 units sold
•	Potential revenue per video = 231,400 x $5 = $1,157,000
•	Campaign cost (one-time fee) = $50,000
•	Net profit = $1,157,000 - $50,000 = $1,107,000

Best option from category: Rema

### 2. Youtubers with the most videos uploaded

Calculation breakdown
Campaign idea = sponsored video series

a.	**TVC News**
•	Average views per video = 4,000
•	Product cost = $5
•	Potential units sold per video = 20,000 x 2% conversion rate = 80 units sold
•	Potential revenue per video = 80 x $5= $ 400
•	Campaign cost (10-videos @ $5,000 each) = $50,000
•	Net profit = $ 400 - $50,000 = -$49,600 (potential loss)

b. **Nollywoodpicturestv**

•	Average views per video = 98,000
•	Product cost = $5
•	Potential units sold per video = 98,000 x 2% conversion rate = 1,960 units sold
•	Potential revenue per video = 1,960 x $5= $9,800
•	Campaign cost (10-videos @ $5,000 each) = $50,000
•	Net profit = $9,800 - $5-,000 = -$40,200 (potential loss)

c. **CelebrateTV**

•	Average views per video = 20,000
•	Product cost = $5
•	Potential units sold per video = 20,000 x 2% conversion rate = 400 units sold
•	Potential revenue per video = 400 x $5= $2,000
•	Campaign cost (10-videos @ $5,000 each) = $50,000
•	Net profit = $2,000 - $50,000 = -$48,000 (potential loss)

The best option from this category is Nollywoodpicturestv, which incurs the least loss of the top 3.  


### 3. Youtubers with the most views

Calculation breakdown
Campaign idea = Influencer marketing

a. **Agbaps Shorts**

•	Average views per video = 5.26 million
•	Product cost = $5
•	Potential units sold per video = 5.26 million x 2% conversion rate = 105,200 units sold
•	Potential revenue per video = 105,200 x $5 = $526,000
•	Campaign cost (3-month contract) = $90,000
•	Net profit = $526,000 - $90,000 = $436,000

b. **MarkAngelComedy**

•	Average views per video = 2.20 million
•	Product cost = $5
•	Potential units sold per video = 2.20 million x 2% conversion rate = 44,000 units sold
•	Potential revenue per video = 44,000 x $5 = $ 220,000
•	Campaign cost (3-month contract) = $90,000
•	Net profit = $220,000 - $90,000 = $130,000

c. **Rema**

•	Average views per video = 11.59 million
•	Product cost = $5
•	Potential units sold per video = 11.59 million x 2% conversion rate = 231,800 units sold
•	Potential revenue per video = 231,800 x $5 = $1,159,000
•	Campaign cost (3-month contract) = $90,000
•	Net profit = $1,159,000 - $90,000 = $1,069,000

Best option from category: Rema 

## Discovery 

##### Top YouTubers by Subscribers:

MarkAngelComedy leads with 9.36M subscribers.
Other notable channels include Agbaps Shorts (5.4M), Rema (4.6M), and CKay (4.13M).

##### Content Creators with the Most Video Uploads:

TVC News Nigeria has an exceptional count of 138,240 videos.
Nollywoodpicturestv (9,345) and CelebrationTV (9,047) follow, focusing on high-frequency uploads.

##### Channels with the Most Views:

Agbaps Shorts tops with 2.62B views.
MarkAngelComedy (2.39B) and Rema (1.89B) are also highly viewed.

##### Average Views Per Video:

Officialpsquare delivers exceptional average views (12.35M), indicating high engagement on fewer uploads.
Rema (11.57M) and CKay (10.98M) also excel.

##### Engagement Rates:

Jhanzou shows the highest engagement per video upload (106,923), followed by CKay (29,500) and Rema (28,200), demonstrating active audience interaction.

# Recommendations 
Influencer Choices Based on Campaign Goals:

**Broad Reach Campaign:**

Choose Rema or Agbaps Shorts for high average views and overall reach. Their audiences are sizable and actively engaged.

**Engagement-Focused Campaign:**

Jhanzou or CKay is ideal for maximizing audience interaction with content.

**Product Placement Campaigns:**

Channels like Officialpsquare or MarkAngelComedy provide consistent viewership, enhancing product visibility over a broader audience.

**Avoid:**

Channels with disproportionately high uploads and low engagement (e.g., TVC News Nigeria) unless targeting niche, high-frequency content viewers.

### Potential ROI Estimates
Using a baseline:
- Conversion Rate: 2%.
- Product Cost: $5/unit.

**Case Examples:**

- Rema:
Average views per video: 11.57M.
Potential units sold: 231,400.
Revenue: $1,157,000.
Net profit (after $90,000 campaign cost): $1,067,000.

- Agbaps Shorts:
Revenue: $526,000.
Net profit: $436,000.

- MarkAngelComedy:
Revenue: $220,000.
Net profit: $130,000.

Best ROI Channel: Rema (highest net profit potential).

### Action Plan

1.	Identify Key Influencers:

Engage Rema and Agbaps Shorts for primary campaigns.
Include Jhanzou for smaller-scale, engagement-specific campaigns.

2.	Define Campaign Structure:
   
Use Rema for broad-reach campaigns, targeting new fintech products.
Utilize Agbaps Shorts for short, high-impact promotions.

4.	Budget Allocation:
Focus 70% of the influencer budget on high-ROI channels like Rema and Agbaps Shorts.
Allocate 30% for experimental partnerships with engagement-heavy creators like Jhanzou.

5.	Measurement and Optimization:
Track campaign performance using views, engagement rates, and conversion data.
Regularly evaluate ROI to refine ongoing campaigns.

6.	Long-term Collaboration:

Establish exclusive partnerships with top-performing YouTubers to build consistent brand visibility.

# Conclusion 

This project provides a data-driven framework for identifying the top Nigerian YouTubers in 2024, offering critical insights tailored to the needs of a fintech marketing campaign. By analyzing subscriber counts, total views, engagement rates, and video uploads, we identified creators like Rema, Agbaps Shorts, and Jhanzou as prime candidates for maximizing campaign ROI.

The analysis highlights the importance of targeting creators with high average views and engagement rates to optimize reach and conversions.
The need to avoid channels with disproportionate uploads and low engagement, ensuring efficient budget allocation.
With a clear action plan in place, the fintech marketing team can leverage these insights to collaborate with influential YouTubers, drive product visibility, and achieve significant returns on investment. This strategy not only aligns with current audience behaviors but also positions the brand for long-term success in the competitive digital landscape.













