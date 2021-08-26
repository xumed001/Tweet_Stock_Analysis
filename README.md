# Twitter & Stock Price Analysis 
![twitter.jpg](analysis_images/twitter.jpg)

## Quick Links 

-    Dashboard: **[Click Here to Visit Our Tableau Public Dashboard.](https://public.tableau.com/app/profile/tara.flynn/viz/Tweet_Stock_Analysis/Dashboard12?publish=yes)**
-    Presentation: **[Click Here to Access Presentation Slides](https://docs.google.com/presentation/d/1eiDhg26rj6FX_s-b5r3N7FIJo1qq6LhwhcxKrEpWc80/edit?usp=sharing)**
-    Tweet Data Source: **[Take Me To Kaggle](https://www.kaggle.com/omermetinn/tweets-about-the-top-companies-from-2015-to-2020)** 

## Project Summary 

The purpose of this project was to analyze how or if Twitter influences the Stock Market. Due to the limitations of the tweet dataset the research was done only on the top `NASDAQ` stocks which are `AAPL` (apple), `AMZN` (amazon), `GOOGL` (google), `MSFT`(microsoft) and `TSLA` (tesla) from the year 2015 to 2019. 

**Hypothesis:**
 - Can we predict how much a stock will trade based on how it's trending on social media?
 - Does tweets impact price action?

## Project Selection Journey
Twitter and its impact on the Stock Market was selected by our group after deliberating a few other potential options such as NBA Team win predeictions, student housing/multi-family tenant geotracking, and the Austin housing market with migration patterns and home cost growth. After taking into considerations of a 5 week time constraint, data limitations from source, and group interests, our topic was chosen. To find the full selection model, you can **[CLICK HERE](https://github.com/tflynn615/Tweet_Stock_Analysis/blob/main/Sam/Project%20Topic%20Selection%20Journey.png)** to view the objective, and limitation details.

## Technology 

  ### Data Cleaning and Analysis
  Excel csvs from Kaggle were used to import the data for tweet data, and Yahoo Finance was utilized for stock/ticker data (Apple, Tesla, Google, Amazon, and Microsoft). `Pandas` was to clean the data and perform an exploratory analysis. Further analysis and manipulation was completed using Python before the data was imported to our PostgresSQL database and connected to our machine learning model.

The ERD for the database that will connect each of these data sources is shown below.

![rough_stock_erd.png](Deliverable_1/ERD_v.1/rough_stock_erd.PNG)

  ### Database Storage
  The database utilized was PostgresSQL with pgadmin 4. Data collected from Kaggle and Yahoo Finance were cleaned during the pre-processing stages with `pandas` and brought into our environment. 5 Ticker tables were brought into our database, 1 for each ticker, and further consolidated to form our master table data. Postgres database was then connected our our machine learning ipynb file for further analysis for prediction and accuracy.

  ### Machine Learning
  SciKitLearn and Tensorflow is the ML library utilized. Machine Learning models utilized were `Linear Regression`, `Logistic Regression`, and `Artifical Neural Network`.


  ### Dashboard and Analysis
  Our final Dashboard is LIVE and available on Tableau public with our findings and ML predictions. We chose to do our analysis and final visualizations in Tableau because we knew that it is a tool popular with many business like the brokerages who might find this model useful, so we planned to make a professional dashboard that would be easy to adopt given its similarity to their native tooling within the client technology ecosystem. 


#### Dashboard Pre-Construction
![dashboard_planning.png](analysis_images/dashboard_planning.png)

The purpose of this initial outline was to identify a framework of worksheets and interactive elements to portray key stories using data analysis of Twitter's impact on NASDAQ Stocks. Analysis includes dynamic integrations between tweet, date, and stock ticker to provide visual grasp to our end users on how tweets and the stock exchange share a relationship in stock liquidity. Analysis of our findings include Tweet Impacts on Stock Prices and Examining Tweet Engagement. 

#### Tweet Volume

![tweet_volume.png](analysis_images/tweet_volume.png) 

*Purpose:* Find which companies are receiving the most tweets and interactions. 

*Analysis:* 
- Sum of all tweets 2015-2019 
- Color by sum of likes, comments, and retweets 

We can see that Apple has the most tweets about their stock ticker while tweets about Tesla see the most likes, retweets, and comments. 

#### Price Action Over Time 

![heat_map.png](analysis_images/heat_map.png) 

*Purpose:* Identify the companies seeing the most change in daily price. 

*Analysis:* 
- Yearly sum of Price Action per Company 
- Color based on Price Action 

The companies with the most negative and positive daily change in price (respectively) are Amazon and Google. This didn't align with the companies receiving the most social media activity, so we needed to keep looking for correlation. 

#### Scatter Plot of Tweet and Stock Volumes 

![scatter_plot.png](analysis_images/scatter_plot.png) 

*Purpose:* Identify the correlation between twitter activity and stock liquidity to align with machine learning. 

*Analysis:* 
- Scatter plot of Tweet Volume against Stock Volume 
- Size based on Tweet Volume 
- Trend line to indicate linear correlation 
- Color by company name 
- URL Action to Explore Machine Learning 

In this scatter plot, we saw a strong correlation between the amount of tweets and the liquidity of a company's stock. This helped us narrow down the purpose of our Machine Learning model to focus on predicting when a stock is likely to see high activity. 

#### Machine Learning Scatter Plot

![ml_scatter.png](analysis_images/ml_scatter.png) 

*Purpose:* Identify how the Machine Learning predictions compare to each other and with the initial scatter plot done in analysis.  

*Analysis:* 
- Tweet Volume plotted against Stock Volume Sold 
- Accuracy determined by whether the resulting Liquidity Level of a day matches what the Machine Learning predicted. 
- Color by whether the Accuracy was True or False 

We can then evaluate how the scatter plot changes when using the resulting data of our Machnine Learning. We can see that where the model accurately predicts liquidity level, there is a clear linear concentration of dots that reinforces that the model has a strong ability to identify liquid stocks based on tweet activity. 

#### Twitter and Stock Volume Over Time 

![volume_time.png](analysis_images/volume_time.png)

*Purpose:* Can we identify any spikes in the Twitter and Stock volumes. 

*Analysis:* 
- A bar chart of all Tweet Volume 
- A line chart of Tweet Volume with colors by Company 
- Both plotted again Month-Year dates 
- URL Action to Explore Machine Learning 

From there, we wanted to see if we could identify any spikes in the volune of Tweets and stocks sold in order to identify any external factors that could be causing this correlation. For example, there's a strong spike with the Tesla tweets in August 2018. 


#### Popular Tweets 

![pop_tweets.png](analysis_images/pop_tweets.png) 

*Purpose:* Use bodies of popular Tweets to identify if any current events driving spikes in social media engagement. 

*Analysis:* 
- Heat map of Tweets with more than 1,000 combined retweets, likes, and comments 
- Color and size by sum of engagement 
- Filter by date 

Using a date filter to drill down, a user could use this worksheet in the dashboard to read tweet bodies and identify any trends to indicate external causation of the correlation. For example, did Apple release a new phone? Or did Elon Musk pull a new stunt? 

We noticed a good deal of promotional tweets that look like Robinhood users attempting to recruit more users, so a future iteration of this model could explore whether these promotions have a significant effect on the market. Additionally, another improvement could be to evaluate the sentiment of tweets and whether they can positively or negatively affect how a stock is sold. 

## Machine Learning Model 
 
**Description of preliminary data preprocessing:**
 - the data pre-processing was done by first summing up the # of tweets for the day as `tweet_activity` and keeping the `date`, `volume` and `price-action` for each ticker. Then separating each ticker into their own csv file and exporting it into the ML model.

**Description of preliminary feature engineering and preliminary feature selection, including their decision-making process**
 - `tweet activity`: was the tweet dataset summed up to its most important factor because of its relation to the stock's price. selected as a feature.
 - `date`: trading date for each stock, was dropped when feeding it into the model because of it lack of importance to the model.
 - `volume`: a given tickers daily trading volume, used in the model as a feature.
 - `price-action`: very important features tells the price movement of the ticker in a given date. used in the model as a feature.
 - `liquid_lvl`: was the target of the dataset as the model was trying to predict how liquid the stock is given its `tweet_count`. 

**Description of how data was split into training and testing sets:**
 - the data for our model was split to the `train-test-split’s default value, which allocates 75% of the data for training and 25% of testing.

**Explanation of model choice, including limitations and benefits:**
 - first `LinearRegression` was used to find a correlation in the dataset if any. `LinearRegression` although benifitial in looking at how one feature of the dataset influences another, it's limited due to its simplicity and is unable to do a training and testing of the dataset. After finding a correlation between `volume` and `tweet-activity` `LogisticRegression` model was used to see how well the model could predict stock liquidity. `LogisticRegression` was successful in predicting a binary outcome, for our dataset but it's limited by low accuracy score and inability to fine tune the model.  

**Explanation of changes in model choice (if changes occurred between the Segment 2 and Segment 3 deliverables):**
 - for segment 3 a neural network model was added to improve accuracy score since `LogisticRegression` was only 57% accurate. The neural network uses one hidden layer and six neurons because of three input features for this model. This new model after 100 iterations gives us an accuracy score of 97%.  

**Description of how they have trained the model thus far, and any additional training that will take place:**
 - the model was trained using `relu` in the hidden layer and `sigmoid` in the output layer as we need the model to tell us if the stock is either liquid or not. `StandardScaler` was used to scale training and testing the features. The model ran for 100 epochs resulting in an accuracy score of 97%  

**Description of current accuracy score:**
 - As mentioned above the current model yields an accuracy score of 97%. Meaning the model can predict if a given stock is liquid (above avg daily volume) feeding the dataset with extreme accuracy.


## Conclusion
Through our research, we identified that our original hypothesis was indeed correct that Twitter has an impact on the Stock Market. From our findings, we were able to discover a positive correlation between `tweet activity` vs `stock volume`. 

But Regarding `tweet activity` vs `price action`, we were not able to find a strong positive correlation, but we identified ways for research to be investigated further through next step iterations.

Since `tweet activity` and `stock volume` had a positive correlation, meaning that if the number of tweet activity increased, the volume of that given stock also increased. This finding was then used to make predictions on the `Liquidity` of the Stock.  Machine Learning models like `Logistic Regression` and `Artificial Neural Network` were used to train a model that predicts Liquidity with the highest accuracy.

After many different variations the final prediction accuracy of the model was 97%. Meaning that if the model was given `tweet activity` data and `stock volume` data it could correctly identify how liquid the stock was at any given day. 

Finally due to the time constraints of the project predicting the stock liquidity was the only thing we were able to accomplish given twitter and the stock market data. The group also had ideas using `NLP`(Natural Language Processing) and `VaderSentiment` to further dive into the tweets itself and discover how that would influence the Stocks. 






