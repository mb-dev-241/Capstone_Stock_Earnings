### Project Title
Stock Earnings Price Prediction

**mb-dev-241**

#### Executive summary
In this project, we make use of an LLM to discover sentiment-related features from a company's earnings call. These features are used in several regression models to make a prediction for the opening price of the company's stock the next day. For comparison, we also investigate earnings surprise data as another predictor of the stock's open price. 

#### Rationale
Quarterly earnings releases are a unique event in every company's calendar year. Generally these occur while the market is closed, giving a specific window to assess the impact of the call content on the company's stock price. Earnings calls can easily be studied across many companies to draw conclusions about the effectiveness of predictive models created from this data.

#### Research Question
To what extent is the content of a company's earnings call useful in determining the price of its stock?

#### Data Sources

1. Motley Fool Earnings Call Transcripts [https://www.kaggle.com/datasets/tpotterer/motley-fool-scraped-earnings-call-transcripts/data]
2. finBERT LLM Python library [https://github.com/ProsusAI/finBERT/archive/refs/heads/master.zip]
3. yfinance ohlc daily bars 
4. yfinance earnings data 

#### Methodology
Significant preprocessing needs to take place to prepare for analysis on the given datasets. Once the data is properly generated and formatted, we apply several common regression models to assess the effectiveness of our predictions. General steps taken to create predictions are as follows:

1. Download Earnings Call Transcripts and LLM Python Library
2. Fixup columns from the the earnings call transcripts
3. Add stock ohlc bars, earnings data, and several additional earnings-related features to the stocks studied 
4. Use the finBERT LLM to add sentiment features derived from the earnings call transcripts
5. Visualize the preprocessed data
6. Apply regression models and assess results

We used finBERT as our LLM, which is trained on financial text, much like the earnings transcripts we're using in this project. We used the LLM to create 4 features for every earnings call transcript: positive, negative, neutral, and sentiment (positive - negative). These scores are the sum of the class predictions for all sentences in the transcript. Additionally, we broke the earnings calls into different segments, which allowed us to get sub-scores from portions of the earnings call. The segment sizes chosen were: 1, 3, and 4; meaning we created 4 features for the full earnings call, 4 features for each third of the call, and 4 features for each quarter of the call. 

We used several familiar regression models: Linear Regression, Decision Trees, Random Forest, KNeighbors, Ridge, and SVR across several different hyperparameters. Random Forest had the best performance and we used results from this model to generate results.

#### Results
We found a slight positive correlation between various sentiment factors and stock performance. This correlation was enhanced when we added in earnings surprise data. Each factor had an independent and additive impact on the overall prediction.

Additional commentary and results are contained in the Jupyter notebooks referenced below.

#### Next steps

In order to further develop the results obtained, we make 3 suggestions for potential improvement:

1. Discovery of additional numeric features in the sentiment data
2. Use of additional LLMs
3. Use of additional ensemble techniques

Discovery of additional numeric features

Our LLM was able to generate sentiment data at a sentence level. To simplify analysis, we analyzed sentiment in larger blocks. For example, our variable sentiment_1_1 refers to the sentiment of the full earnings call, sentiment_1_4 refers to sentiment of the first quarter of the earnings call, etc.

Additional structure to the earnings call may have been lost in the process. It may be that poor earnings calls have additional structure at a granular level consisting of a known sentiment pattern (eg. compliment sandwich) that portend even more highly negative outcomes. Discovering these features, if they exist, would provide additional gains to our model.

Use of additional LLMs

In our case, we only used a single LLM. Use of additional LLMs, particularly those tuned to analyzing financial information, would likely result in further improvement.

Use of additional ensemble techniques

We explored a few ensemble techniques in this analysis but our best, Random Forest, only makes use of decision trees. An ensemble technique combining multiple types of estimators may be able to improve this further.

#### Outline of project

- [Initial Setup](https://github.com/mb-dev-241/Capstone_Stock_Earnings/blob/main/0_Initial_Setup.ipynb)
- [Prepare Transcript Data](https://github.com/mb-dev-241/Capstone_Stock_Earnings/blob/main/1_Prepare_Transcript_Data.ipynb)
- [Download and Prepare Stock Data](https://github.com/mb-dev-241/Capstone_Stock_Earnings/blob/main/2_Download_Prepare_Stock_Data.ipynb)
- [Create LLM Features](https://github.com/mb-dev-241/Capstone_Stock_Earnings/blob/main/3_Create_LLM_Features.ipynb)
- [Data Preview](https://github.com/mb-dev-241/Capstone_Stock_Earnings/blob/main/4_Data_Preview.ipynb)
- [Run_Regression_Analysis](https://github.com/mb-dev-241/Capstone_Stock_Earnings/blob/main/5_Run_Regression_Analysis.ipynb)

##### Contact and Further Information

