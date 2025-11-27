# Website Traffic Analytics

This data project was originally used as a take-home assignment during the recruitment process for Data Science positions at Linkfire. The dataset is publicly available on StrataScratch:
https://platform.stratascratch.com/data-projects/website-traffic-analysis

The objective of this project is to analyze user traffic, understand the distribution of events, and propose ideas to improve link click-through rates. SQL is used to answer the following analytical questions:
	1.	How many total pageview events did the links in the dataset receive over the full period, and how many per day?
	2.	How many events occurred for the other recorded event types?
	3.	Which countries generated the pageviews?
	4.	What is the overall click rate (clicks/pageviews)?

The dataset (traffic.csv) contains web traffic event logs collected over a 7-day period. Each record represents an event on a specific link, along with categorical attributes such as country, city, artist, album, track, and ISRC.

First, lets check the dataset 

![Dataset Preview](https://github.com/belamon/Website_Traffic_Analysis_Linkfire_Takehome_Assignment/blob/c619b158f47acde9ec862ab43992d2bbe0472558/Screenshot%202025-11-27%20at%2023.04.21.png)

result 

![alt text](<Screenshot 2025-11-27 at 23.00.34.png>)

## Question 1: 

## How many total pageviews events did the links in the dataset receive over the full period, and how many per day?

To answer this, we will break the process into clear, logical steps so readers can easily follow how the result was produced 

🔎 Step 1 — Check the distinct values in the event column
Before counting anything, it’s important to understand which event types exist in the dataset.


![alt text](<Screenshot 2025-11-27 at 23.22.47.png>)

Result:


![alt text](<Screenshot 2025-11-27 at 23.23.08.png>)

We can see that there are 3 distinct event types:
	•	pageview
	•	click
	•	preview

Since we are focusing only on pageviews, we will filter for that specific event.


🧮 Step 2 — Count the total number of pageview events

To calculate how many pageviews occurred across the entire dataset, we use a simple filter + count:

![alt text](<Screenshot 2025-11-27 at 23.39.01.png>)

Result:

![alt text](<Screenshot 2025-11-27 at 23.39.18.png>)

This gives us the total number of pageview events recorded.

📅 Step 3 — Count total pageviews for each day
Now that we know the overall total, the next step is to understand how pageviews are distributed across the 7-day period.
This helps identify traffic patterns, spikes, or drops in user activity.

To get the daily breakdown, we group the data by event_date:


![alt text](<Screenshot 2025-11-28 at 00.14.10.png>)

Result:

![alt text](<Screenshot 2025-11-28 at 00.14.33.png>)

This output shows the number of pageview events for each day, allowing us to analyze which dates had higher or lower engagement.

🧹 Step 4 — Count deduplicated pageviews per day

Sometimes datasets contain duplicate rows, especially when events are logged multiple times by mistake.
To ensure accuracy, we should remove duplicates before counting pageviews per day.

We’ll do this in two parts:
We use a WITH clause (CTE) to create a temporary table containing only unique rows:


![alt text](<Screenshot 2025-11-28 at 00.17.40.png>)

Now we use the deduplicated CTE to count daily pageviews:


![alt text](<Screenshot 2025-11-28 at 00.18.23.png>)

Result:


![alt text](<Screenshot 2025-11-28 at 00.19.00.png>)

This gives us the true daily pageview count, excluding any accidentally duplicated logs.

