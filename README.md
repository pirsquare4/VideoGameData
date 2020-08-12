# Video Game Data
Download the data [here](https://www.kaggle.com/ashaheedq/video-games-sales-2019)

## Intro
The data I downloaded was a CSV of video game sales from 1988 all the way until 2019 and a bit of 2020. However, some of the 2019 and 2020 data is incomplete as those figures have not finished being published yet. The data includes total sales, where the sales were made, ratings of games, genres of games, and their titles respectively.

I love python, therefore I did most of my work through pandas and jupyter notebook, then exported my data, and made charts with the seaborn package in python, or in google sheets.

## Data Cleaning

First off, some of the data is incomplete and have NaaN values. I began by removing any game that did not have a video game review a rating, and use this table for any charts that required the critic rating value

`videogame_data_filtered = videogame_data[videogame_data['Critic_Score'].notnull()]
videogame_data_filtered = videogame_data_filtered.fillna(0)`

Secondly, I then added a "summed" column. The way this table works is it breaks down each major video game buying region (Japan, EU, NA) and then puts the rest of sales under "other". It then sums those 4 columns into the "Global Sales" column. However, sometimes the numbers for each region aren't explicitly available, so there is another column called "Total Shipped" which just provides the global number instead of breaking it down by region. I therefore made a column called "summed" which took the "Global Sales" if it was not null, and if it was null, then it would take the "Total Shipped" column, and use that instead. This made sure that even if we didn't have a breakdown of sales per region, we would still have a number of sales regardless.

`videogame_data_filtered['summed'] = videogame_data_filtered.Total_Shipped+videogame_data_filtered.Global_Sales`

This line of code works because either Total_Shipped is 0 or Global_Sales is 0. They will never both contain a number above 0. 

## First Chart : Correlation between critic score and number of copies sold?

My first inquiry was seeing if there was a correlation between critic ratings and number of sales. This was my first bit of code. On the X-axis we have the critic rating out of 10, and the Y-axis is sales in millions of copies
![Code Image](https://media.journalism.berkeley.edu/upload/2020/08/1597208197a40ad02.png)

However its a bit hard to see as there are some outliers which make our x and y axis very big. Therefore I remove any video game with sales above 30 million, to make the graph smaller and easier to read (This removes about 10 data points out of about 37 000). I also added a best fit line, to see if there was any correlation between the rating and the number of sales. It seems that there is a bit of correlation, but I expected it to fit much much better than it ended up.
![Code Image](https://media.journalism.berkeley.edu/upload/2020/08/1597208327e0c0c64.png)

## Second Chart : What are the top games sold per region? Are there any trends?
For this section, I added all the games back to the tally that didn't have any critic scores, as critic scores don't matter. I then filtered out the data and made 5 different excel sheets: 1 for the top ten games in NA, top ten in EU, top ten in JP, top ten in Other Countries, and top ten globally. This was our result:
![NA GRAPH](https://media.journalism.berkeley.edu/upload/2020/08/1597209013d599560.png)
![EU GRAPH]https://media.journalism.berkeley.edu/upload/2020/08/15972095311a7be88.png)
![JP GRAPH](https://media.journalism.berkeley.edu/upload/2020/08/15972097057689053.png)
![OTHER GRAPH](https://media.journalism.berkeley.edu/upload/2020/08/1597210013c52ff36.png)
![GLOBAL GRAPH](https://media.journalism.berkeley.edu/upload/2020/08/1597210218230cd32.png)
