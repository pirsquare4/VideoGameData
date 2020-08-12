# Video Game Data
Download CSVs for this project [here](https://www.kaggle.com/ashaheedq/video-games-sales-2019)

## Intro
Hi, my name is Giordano Bonora Groome and this is my data vizualization of the video game industry. I really love video games so I thought it might be interesting to make a few graphs to better understand the market, and people's tastes.

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
![EU GRAPH](https://media.journalism.berkeley.edu/upload/2020/08/15972095311a7be88.png)
![JP GRAPH](https://media.journalism.berkeley.edu/upload/2020/08/15972097057689053.png)
![OTHER GRAPH](https://media.journalism.berkeley.edu/upload/2020/08/1597210013c52ff36.png)
![GLOBAL GRAPH](https://media.journalism.berkeley.edu/upload/2020/08/1597210218230cd32.png)

The code to make the excel sheets looked something like this:

`top_10_japan = videogame_data_filtered.sort_values('JP_Sales', ascending = False).head(10)`

`top_10_japan.to_csv("top_10_japan.csv")`

`top_10_japan`

We can see that North America has almost exclusively shooting games as their top video games. Meanwhile Europe also has a lot of shooting games, but there are also a lot of FIFA and soccer games in the top games as well. Japan is way different from both, as they like more anime/cartoon style games, both of which are absent from the top 10 in NA and EU.

## Third Chart: What games dominate the market by genre?
Lastly, I wanted to see what game genre dominated the market. The chart below groups all the video games by genre, and then uses the total amount of copies sold as the value.

![GENRE PIE CHART](https://media.journalism.berkeley.edu/upload/2020/08/1597212362f30784e.png)

I thought it would also be interesting to see how video game sales have been going overtime: 

![YEARLY CHART](https://media.journalism.berkeley.edu/upload/2020/08/15972120754a80299.png)

We can see that shooters and action video games dominate the game market, while simulation and strategy hold up the tail end. An interesting observation is that video game sales in recent years have gone down. I think there are two reasons for this: Games released in 2017 or 2018 are still relatively new, and people are still buying them, therefore the total number is not yet "complete" since people are still buying the video games. Secondly, lots of games have become free to play, with in game purchases. Top video games, like League of Legends and Fortnite both employ this marketing strategy. The game is free to play, but add in game purchases to make your character more asthetically pleasing/more personalized. So this makes it hard for games like these to be tracked, as there are no copies "sold". People aren't playing less video games. People just buy less video games. The rest of the world has a similar taste to North America, with a FIFA game thrown in there. What's interesting, is that globally, PG games, like Mario or Wii Sports are the top games. It seems that while regions have their personal favorite types of games, accross regions as a whole, non-violent, more child oriented games seem to be the most bought and played.

## Conclusion

While critic scores do play a role in game sales, they are not the end all be all of a game. Also, it seems each region has their own game trend, and while action and sports games seem to dominate the market, fun casual games like Mario and Wii Sports are still vastly popular. I did most of my work with pandas in Python 3.8. I attatched my code in the files of this Github if you wanted to take a look at my other expirementations.

# THANK YOU!
