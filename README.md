# Video Game Data
Download the data [here](https://www.kaggle.com/ashaheedq/video-games-sales-2019)

## Intro
The data I downloaded was a CSV of video game sales from 1988 all the way until 2019 and a bit of 2020. However, some of the 2019 and 2020 data is incomplete as those figures have not finished being published yet. The data includes total sales, where the sales were made, ratings of games, genres of games, and their titles respectively.

I love python, therefore I did most of my work through pandas and jupyter notebook, then exported my data, and made charts with the seaborn package in python, or in google sheets.

## Data Cleaning

'code'
First off, some of the data is incomplete and have NaaN values. I began by removing any game that did not have a video game review a rating, and use this table for any charts that required the critic rating value
Secondly, I then added a "summed" column. The way this table works is it breaks down each major video game buying region (Japan, EU, NA) and then puts the rest of sales under "other". It then sums those 4 columns into the "Global Sales" column. However, sometimes the numbers for each region aren't explicitly available, so there is another column called "Total Shipped" which just provides the global number instead of breaking it down by region. I therefore made a column called "summed" which took the "Global Sales" if it was not null, and if it was null, then it would take the "Total Shipped" column, and use that instead. This made sure that even if we didn't have a breakdown of sales per region, we would still have a number of sales regardless.

## First Chart

My first inquiry was seeing if the 
