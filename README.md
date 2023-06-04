# Module-11-Challenge
## Time Series forcasting on MercadoLibre E-commerce website.

I've been tasked with analyzing the company's financial and user data in clever ways to make the company grow. So, I want to find out if the ability to predict search traffic can translate into the ability to successfully trade the stock.
Following are the steps to perform the analysis and forcasting.

- Step 1: Find unusual patterns in hourly Google search traffic

- Step 2: Mine the search traffic data for seasonality

- Step 3: Relate the search traffic to stock price patterns

- Step 4: Create a time series model with Prophet

- Step 5 (optional): Forecast revenue by using time series models

## Usage

To use this application, simply clone the repository and open google colab and then upload the file named forecasting_net_prophet.ipynb.
Upon launching the application in google colab notebook, run the file by using the runtime button on the top of the notepad.

Google Colab link- https://colab.research.google.com/drive/1Yqu9tCo5grv3KGLSdxB2dfxlBvfa6yP5#scrollTo=WrGgA-HqbuRX

![image](https://github.com/malika0410/Module-11-Challenge/blob/main/images/1.png)

## Import all the libraries & dependencies

![image](https://github.com/malika0410/Module-11-Challenge/blob/main/images/2.PNG)

![image](https://github.com/malika0410/Module-11-Challenge/blob/main/images/3.png)


## Step 1: Find Unusual Patterns in Hourly Google Search Traffic

Does the Google search traffic for the company link to any financial events or is the search traffic data just random noise?

1. I sliced the data to just the month of May 2020. (During this month, MercadoLibre released its quarterly financial results) and used hvPlot to visualize the results. Did any unusual patterns exist?

![image](https://github.com/malika0410/Module-11-Challenge/blob/main/images/google_search_trens.PNG)



There were no highly unusual patterns existing in the Month of May besides a slight increase on 5/5 which capped at 120 search trends.
2. Then I calculated the total search traffic for the month, and compared the value to the monthly median across all months. Did the Google search traffic increase during the month that MercadoLibre released its financial results?
Monthly traffic for May was 38181, the monthly median across all months was 35172.5 searches, therefore the monthly traffic in May was 3008.5 searches higher than the median by 8%.

## Step 2: Mine the Search Traffic Data for Seasonality
Marketing realizes that they can use the hourly search data, too. If they can track and predict interest in the company and its platform for any time of day, they can focus their marketing efforts around the times that have the most traffic. This will get a greater return on investment (ROI) from their marketing budget.

To that end, you want to mine the search traffic data for predictable seasonal patterns of interest in the company. To do so, I completed the following steps:

1. Group the hourly search data to plot the average traffic by the day of the week (for example, Monday vs. Friday)



Search traffic peaks in the beginning of the week, at it's highest point on Tuesday and tapers off reaching it's lowest point on Sunday.
2. Using hvPlot, visualize this traffic as a heatmap, referencing index.hour for the x-axis and index.dayofweek for the y-axis. Does any day-of-week effect concentrate in just a few hours of that day?

![image](https://github.com/malika0410/Module-11-Challenge/blob/main/images/day_of_week_heatmap.PNG)


The least amount of searches are between 5 and 10 am everyday of the week, and the the most searches are concentrated early in the week extremely late at night and leads into the early morning towards 4 am. Lowest day of the week for searches is Saturday.
3. Group the search data by the week of the year. Does the search traffic tend to increase during the winter holiday period (weeks 40 through 52)?



There is a lot of upward and downward trends throughout the entire year, but after week 42 there is a sharp uptick in searching for traffic trends and has a very sharp decline after week 51.

## Step 3: Relate the Search Traffic to Stock Price Patterns
Next, we want to know if any relationship between the search data and the company stock price exists:

1. Market events emerged during 2020 that many companies found difficult. But after the initial shock to global financial markets, new customers and revenue increased for e-commerce platforms. So, I sliced the data to just the first half of 2020 (2020-01 to 2020-06), and then used hvPlot to plot the data.
Do both time series indicate a common trend that’s consistent with this narrative?







Yes, both plots show a severe dip in search trends and closing price beginning at the end of February resulting in a drop in closing price of $752 to it's lowest point in March to $429. During the month of April there was a sharp uptick in both search trends and closing price showing the predicted revenue increase.
2. I then created a new column in the DataFrame named “Lagged Search Trends” that offsets, or shifts, the search traffic by one hour. I put in two additional columns:

- “Stock Volatility”, which holds an exponentially weighted four-hour rolling average of the company’s stock volatility

- “Hourly Stock Return”, which holds the percentage of change in the company stock price on an hourly basis

3. Does a predictable relationship exist between the lagged search traffic and the stock volatility or between the lagged search traffic and the stock price returns?

![image](https://github.com/malika0410/Module-11-Challenge/blob/main/images/compare_search_trend_Vs_close.PNG)




A predictable relationship does not exist between the lagged search traffic and the stock volatility OR between the lagged search traffic and the stock price returns. The highest correlation is positive .06 which is very low.

![image](https://github.com/malika0410/Module-11-Challenge/blob/main/images/volatilty_corr.PNG)


