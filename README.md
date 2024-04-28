# prophet-challenge

# Module 8 Challenge 
# MSU AI Bootcamp 2023 - 2024
## Author:
- Taylor Peterson
# Background
>You’re a growth analyst at [Mercado Libre](http://investor.mercadolibre.com/about-us) (**warning** as this links to an external site). With over 200 million users, Mercado Libre is the most popular e-commerce site in Latin America. You've been tasked with analyzing the company's financial and user data in clever ways to make the company grow. So, you want to find out if the ability to predict search traffic can translate into the ability to successfully trade the stock.

>The instructions for this Challenge are divided into four steps, as follows:
* Step 1: Find unusual patterns in hourly Google search traffic.

* Step 2: Mine the search traffic data for seasonality.

* Step 3: Relate the search traffic to stock price patterns.

* Step 4: Create a time series model with Prophet.

# User Notes
* Clone this repository onto your computer.
* Upload the `forecasting_net_prophet.ipynb` file to a Google Colab Notebook 
* Run each cell in order
    * This may require a few installations that Colab may require a restart of the kernel/session to proceed.
    * After restarting your session, the cells will run appropiately.

# Intructions
* Follow the below steps
# Step 1: Find Unusual Patterns in Hourly Google Search Traffic
The data science manager asks if the Google search traffic for the company links to any financial events at the company. Or, does the search traffic data just present random noise? To answer this question, pick out any unusual patterns in the Google search data for the company, and connect them to the corporate financial events.

To do so, complete the following steps:

1. Read the search data into a DataFrame, and then slice the data to just the month of May 2020. (During this month, MercadoLibre released its quarterly financial results.) Visualize the results. Do any unusual patterns exist?
    #### **Answer:**
    >It appears that search trends in the month of May 2020 had spikes between the 4th and 5th. The rest of the plot follows a similar pattern, where it rises and falls every 3-4 days.

2. Calculate the total search traffic for the month, and then compare the value to the monthly median across all months.

3. Did the Google search traffic increase during the month that MercadoLibre released its financial results? Write your answer in the space provided in the starter file.
    #### **Answer:**
    >They did increase. In the month of May (specifically May, 2020, and when MercadoLibre released it's financial results), the total search traffic was **38181**. Compared to the monthly medium calculated across all months, **35172.5**, there was an increase of **.085536**, or about a 9% increase.

# Step 2: Mine the Search Traffic Data for Seasonality
Marketing realizes that they can use the hourly search data, too. If they can track and predict interest in the company and its platform for any time of day, they can focus their marketing efforts around the times that have the most traffic. This will get a greater return on investment (ROI) from their marketing budget.

To that end, you want to mine the search traffic data for predictable seasonal patterns of interest in the company. To do so, complete the following steps:

1. Group the hourly search data to plot the average traffic by the hour of day. Does the search traffic peak at a particular time of day or is it relatively consistent?
    #### **Answer:**
    >The lowest point of hourly search traffic would be early in the morning, around 5:00/6:00 a.m., while the peaks start to begin their increase at around (10:00 a.m.). The particular time of the highest peak is midnight (00:00:00).

2. Group the hourly search data to plot the average traffic by the day of the week (for example, Monday vs. Friday). Does the search traffic get busiest on any particular day of the week?
    #### **Answer:**
    >The traffic is relatively high at the begining of the week, with the highest point on Tuesday. It tapers off and drastically decreases moving into the weekend, where it hits it's lowest point.

3. Group the hourly search data to plot the average traffic by the week of the year. Does the search traffic tend to increase during the winter holiday period (weeks 40 through 52)?
    #### **Answer:**
    >I would say that yes, the search traffic does increase during the holiday week period. At the end (of week 52), it drops down, only to most likely spike back up again in the following weeks. It absolutely hits it's peak for holiday season right before a major holiday, Christmas (about weeks 49-52).

4. Are there any time based trends that you can see in the data? Write your answer in the space provided in the starter file.
    #### **Answer:**
    > As I stated above, it appears that a time-based trend would be late-night (any time after 8:00 p.m.) to around midnight, that we can see hourly search traffic at it's highest point. 

    >Weekly, we see major highs at the beginning of each week (Monday-Friday), and a drastic decrease going into, and throughout, the weekend. 
    
    >Annual data by week gives us insight into the trends spiking in the holiday season weeks (40-52), which is just below the highest search data weeks of the year, weeks 2 to (about) 8 in the year. Maybe this would reflect gift return season after receiving possibly unwanted holiday gifts?

# Step 3: Relate the Search Traffic to Stock Price Patterns
You mention your work on the search traffic data during a meeting with people in the finance group at the company. They want to know if any relationship between the search data and the company stock price exists, and they ask if you can investigate.

To do so, complete the following steps:

1. Read in and plot the stock price data. Concatenate the stock price data to the search data in a single DataFrame.

2. Market events emerged during the year of 2020 that many companies found difficult. But, after the initial shock to global financial markets, new customers and revenue increased for e-commerce platforms. Slice the data to just the first half of 2020 (2020-01 to 2020-06 in the DataFrame), and then plot the data. Do both time series indicate a common trend that’s consistent with this narrative?
    #### **Answer:**
    >The two plots are rather similar, with similar drops during the month of March. The search trends follow and normal path until May, when the report is released. The closing patterns of the stock data slowly rise until May, where they begin to increase at a rapid rate. These differ slightly, as the 'Search Trends' hit their peak in May, but return to their normal pattern thereafter. The stock closing data peaks in May, but continue to rise for the remainder of this half of the year.

2. Create a new column in the DataFrame named “Lagged Search Trends” that offsets, or shifts, the search traffic by one hour. Create two additional columns:

    * *“Stock Volatility”*, which holds an exponentially weighted four-hour rolling average of the company’s stock volatility

    * *“Hourly Stock Return”*, which holds the percent change of the company's stock price on an hourly basis

4. Does a predictable relationship exist between the lagged search traffic and the stock volatility or between the lagged search traffic and the stock price returns? Write your answer in the space provided in the starter file.
    #### **Answer:** Ref: #7 and #8

    > The correlation between the lagged search traffic (`Lagged Search Trends`) and stock volatility (`Stock Volatility`) is rather weak. In fact, it has a negative correlation (-0.148938). This would make any further predictions between the two, based on this data alone, not incredibly helpful or useful. 

    >Between lagged search traffic (`Lagged Search Trends`) and stock price returns (`Hourly Stock Return`), it would also appear that their relationship is also very weak. However, it is good to mention that there is a slightly positive relationship between the two (0.017929). Meaning, the hourly stock change prices do not necessarily have much predictable influence on how volatile the stock may be.

    >To conclude, the three factors, that I have data for, do not appear to directly influence each other in a meaningful way. The numbers do not appear to display any predictable relationships.

# Step 4: Create a Time Series Model with Prophet
Now, you need to produce a time series model that analyzes and forecasts patterns in the hourly search data. To do so, complete the following steps:

1. Set up the Google search data for a Prophet forecasting model.

2. After estimating the model, plot the forecast. How's the near-term forecast for the popularity of MercadoLibre?
    #### **Answer:** Ref #9
    >The declining `yhat` values would indicate a **decrease** in forecasted popularity. If they were rising, it would be indicative of an increase in popularity of the near-term forecast.

3. Plot the individual time series components of the model to answer the following questions in the space provided in the starter file:

* What time of day exhibits the greatest popularity?
    #### **Answer:** 
    >The hour of the greatest popularity is **Midnight/12:00 a.m./00:00:00**

* Which day of the week gets the most search traffic?
    #### **Answer:**
    >**Tuesday** holds title for the most search traffic when comparing to other days of the week

* What's the lowest point for search traffic in the calendar year?
    #### **Answer:**
    >**October** is the lowest point for search traffic in the calendar year (the plot dips between Sepetember 1 and November 1).

# References

### The references provided below are referenced directly throughout my code, using either the `numbers` that they are assigned, or the specific `module`, `day`, and `activity`.
1. Module 8, Day 1 Activities - The specific activities will be referenced throughout my code.
2. Module 8, Day 2 Activities - The specific activities will be referenced throughout my code.
3. Module 8, Day 3 Activites - The specific activities will be referenced throughout my code.
4. [Pandas Groupby and Computing Median](https://www.geeksforgeeks.org/pandas-groupby-and-computing-median/) - Article by: abhijitmahajan772
5. [Pandas Documentation - Plotting](https://pandas.pydata.org/pandas-docs/version/0.14.0/visualization.html) - Documentation for Pandas plotting methods.
6. [pandas.DataFrame.pct_change](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.pct_change.html) - Pandas Documentaion for calculating percentage
7. [What Is Market Volatility—And How Should You Manage It?](https://www.forbes.com/advisor/investing/what-is-volatility/) - To further my knowledge of market volatility
8. [Time Series as Features](https://www.kaggle.com/code/ryanholbrook/time-series-as-features) - More information on time series analysis: lagging a time series
9. [Understanding FB Prophet: A Time Series Forecasting Algorithm](https://medium.com/illumination/understanding-fb-prophet-a-time-series-forecasting-algorithm-c998bc52ca10) - A member-only story on [Medium](https://medium.com/) that ecplain logic and usage behind Prophet for time series forecasting in Python