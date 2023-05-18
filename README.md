# ***Predicting Pakistan Trade with Countries for Future using Previous Trade Data***
![Alt text](https://www.adb.org/sites/default/files/content-media/150106-pakistan-01.jpg)
## *Brief description of the project*
This project aims to predict Pakistan's trade with other countries in the future using previous
trade data. The challenge in this project is that there are multiple time series within the data,
which makes it difficult to do feature engineering and achieve high accuracy due to other factors.
Feature engineering is the process of selecting and transforming the data to create features that
can be used to train a predictive model. However, with multiple time series, it can be difficult to
identify the most important features and how they relate to each other.
![Alt text](https://cdn.educba.com/academy/wp-content/uploads/2020/05/Time-Series-Analysis.jpg)
## *Dataset availability*
The data will be used from this site:
- [https://comtrade.un.org/data](#index) [Site link](https://comtrade.un.org/data)
- [https://wits.worldbank.org/](#index) [Site link](https://wits.worldbank.org/)

We get the websites from APIs and we use R script to get the data from APIs.Then we used python formatter to convert the APIs into R script. 
The data is categorized into 2 categories Export Items and Import items. Furthermore the data was divided based on the geographical location of the trade partner country. 
The data was also available  with respect to commodities.We downloaded 3 types of commodities:

- [Knit](#index)
- [Linen](#index)
- [Rice](#index)

The data available was from `2003-2021` and the trade data was from all the countries of Pakistan.

## ***Workflow***

- [Data Preprocessing](#index)
- [Models](#index)

# ***Data Preprocessing***
![Alt text](https://assets-global.website-files.com/5d7b77b063a9066d83e1209c/627d122b8fdb884d672952bf_61f7bfab94334458028eec7d_data-preprocessing-cover.png)
We used the data `rice.csv` for doing prediction first from the Export file and worked on it.
We performed data preprocessing on a Pandas dataframe ‘df’. Specifically, it is renaming two columns in the dataframe using the rename method.We modified the dataframe df with the two columns renamed as specified.Then we add a new column named 
- [RSI](#index)
- [EMAF](#index)
- [EMAM](#index)
- [EMAS](#index)

## ***RST***
RSI stands for Relative Strength Index: A technical analysis indicator that measures the strength of a security by comparing its upward movements to its downward movements.

## ***EMAF***
EMAF stands for Exponential Moving Average with a short-term period: A type of moving average that gives more weight to recent prices, with the short-term period typically ranging from a few days to a few weeks.

## ***EMAM***
EMAM stands for Exponential Moving Average with a medium-term period: A type of moving average that gives more weight to recent prices, with the medium-term period typically ranging from a few weeks to a few months.

## ***EMAS***
EMAS stands for Exponential Moving Average with a long-term period: A type of moving average that gives more weight to recent prices, with the long-term period typically ranging from several months to a year or more.
We added these to the dataframe, and filled it with values calculated using the relative strength index with a window length of 2,4,10 and 15 respectively which is computed using the ta.rsi function from the ta module.

After that we added a new column named Target to the dataframe, and filled it with the values of the Value_In_Dollars column, shifted one row up and dropped the Period column.We sorted a DataFrame called data_set by the values in the 'Year' column in ascending order.
The output is the sorted DataFrame, where each row corresponds to a record in the original dataset, but they are now ordered based on the 'Year' column.
Then we interpolate the missing values in the DataFrame using linear interpolation method. Linear interpolation method estimates the missing values based on the linear relationship between the known adjacent values.
Then the missing values are filled with a forward filling method. Forward filling method fills the missing values with the most recently observed value.
Then we did the minmax scaling of the data and prepared the input data X and target data y for a machine learning model. It creates a sliding window of past back candles, time steps of the input features from the data_set_scaled dataframe and appends them to X. The target variable is extracted from the last column of data_set_scaled and appended to y. Finally, X and y are converted to numpy arrays.The output X is a 3-dimensional numpy array of shape (number of samples, back candles, number of features), and y is a 2-dimensional numpy array of shape (number of samples, 1).

<img width="602" alt="v7" src="https://github.com/farheenlatif/project/assets/88893044/d81eca4e-34b8-4112-85dc-85c872c37ceb">


# ***Models***
- [LSTM](#index)
- [Regression](#index)
- [Random Forest](#index)

## ***LSTM***
![Alt text](https://modeling-languages.com/wp-content/uploads/2019/07/Architecture-EncoderDecoder_v2-1080x453.png)
Following are the layers of LSTM and the steps involved:
- [Input Layer](#index)
- [LSTM Layer](#index)
- [Dense Layer](#index)
- [Activation Layer](#index)
- [Model Compilation](#index)
- [Model Fitting](#index)

## ***Input Layer***
The input layer is defined as a three-dimensional tensor, where the first dimension represents the number of samples, the second dimension represents the number of time steps, and the third dimension represents the number of features. In this case, the input shape is (back candles, 4), which means that each sample has backcandles time steps, and each time step has four features.

## ***LSTM Layer***
The LSTM layer has 150 units, which means that it will output 150 values for each input sequence. The output of this layer is a sequence of hidden states, where each hidden state represents the "memory" of the model for a particular time step.

## ***Dense Layer***
The dense layer is a fully connected layer with one unit. It takes the output of the LSTM layer and applies a linear transformation to it, resulting in a single output value for each input sequence.

## ***Activation Layer***
The activation layer applies the linear activation function to the output of the dense layer. In this case, the linear activation function is used because the goal of the model is to predict continuous values.

## ***Model Completion***
The model is compiled using the Adam optimizer and mean squared error (MSE) loss function. The optimizer is responsible for updating the model's parameters based on the gradients computed during backpropagation. The MSE loss function is used to measure the difference between the predicted and actual values.

## ***Model Fitting***
The model is trained on the training data (X_train and y_train) for a specified number of epochs and batch size. The validation split is set to 0.1, which means that 10% of the training data is used for validation. The verbose parameter is set to 0, which means that the training progress is not printed to the consol.

<img width="709" alt="v8" src="https://github.com/farheenlatif/project/assets/88893044/944de0ed-c3c2-42b6-8041-2ed735b25dc5">


## ***Regression***
![Alt text](https://www.imsl.com/sites/default/files/styles/social_preview_image/public/image/2021-06/IMSL%20What%20is%20Regression%20Model%20Blog%20Feature.png?itok=y6F7nJ19)
## ***Preprocessing***
First we read multiple CSV files and concatenate them into a single DataFrame called df. The columns of interest are selected and stored in a new DataFrame called df_partners. The columns "Partner Code" and "Partner" are selected, and duplicate rows are dropped to obtain a DataFrame with unique partner codes and partner names.
The next step drops columns "Partner" and "Trade Flow" from the df DataFrame, as they are not required for the analysis. The df_export and df_import DataFrames are created by filtering the df DataFrame based on the values in the "Trade Flow Code" column. The value 2 indicates an export, while the value 1 indicates an import. The "Trade Flow Code" column is then dropped from both DataFrames.The joining function is used next, which takes a DataFrame as input and performs the following steps:
- [Identifies unique years and countries present in the input DataFrame.](#index)
- [Transposes a matrix consisting of repeated years and countries, where each combination represents a unique year-country pair.](#index)
- [Merges this matrix with the input DataFrame based on the "Year" and "Partner Code" columns.](#index)
- [Removes any rows with a "Partner Code" of 0, indicating an unknown partner.](#index)
- [Fills any missing values with 0.](#index)

The joining function essentially ensures that the resulting DataFrame has all unique year-country pairs, with missing values filled in with 0. This is important as it allows for the creation of a pivot table where each row represents a unique country and each column represents a unique year.

Overall, these preprocessing steps are preparing the data for analysis by ensuring that all required columns are present, and that there are no missing or duplicate values. It also creates two separate DataFrames for exports and imports, which can be used for further analysis. Finally, it creates a complete DataFrame with all unique year-country pairs, which can be used to create a pivot table for analysis.

<img width="891" alt="v9" src="https://github.com/farheenlatif/project/assets/88893044/b585fbc9-0415-438d-af66-c828da8efef1">


## ***Visualizations***
The first visualization plots the imports of Pakistan with top 10 countries with respect to Trade Value in dollars of the year 2021.

<img width="468" alt="v1" src="https://github.com/farheenlatif/project/assets/88893044/00e9ea69-c398-4d57-bc02-8f8428ad6728">

The second visualization plots the export value in US dollars over time for the top 10 partner countries with the highest export values. The data used for this visualization is contained in the df_pivot dataframe.

<img width="480" alt="v2" src="https://github.com/farheenlatif/project/assets/88893044/cc7b7a5a-61ab-4650-84cb-bfda78b57ee3">

## ***Model Training***
## ***Concept of Lags and Moving Averages***
In time series analysis, lags and moving averages are used to model and forecast future values based on past observations.

A lag is simply a shift in the time series data by a specific number of time periods. For instance, a lag of 1 on a monthly dataset would mean that the value of each observation is replaced by the value from one month prior. This can be useful for detecting trends and seasonality in the data, as well as for removing autocorrelation.

Moving averages, on the other hand, smooth out the data by calculating the mean of a specified number of past observations. For example, a 3-period moving average on a monthly dataset would replace each observation with the average of that observation and the two prior ones. This can help to remove noise in the data and highlight long-term trends.

In this specific dataset, lags and moving averages are used to create additional features that may help to improve the accuracy of a linear regression model for forecasting.
## ***Training Workflow***
We performed time series analysis on a dataset containing yearly export data for various countries. The analysis is performed using a for loop that iterates over each country's column in the dataset.

For each country, the code creates a new DataFrame with the country's yearly export data and several lag and moving average features. The lag features are created by shifting the country's export data by 1, 2, and 3 years. The moving average features are created by calculating the rolling mean of the country's export data over windows of 3, 5, and 7 years.

The data is then scaled using the MinMaxScaler, which scales each feature to a range between 0 and 1. The scaled data is split into training and testing sets, with the first 18 years used for training and the last 2 years used for testing.

A linear regression model is then trained on the training set using the lag and moving average features as inputs and the country's export data as the output. The model is then used to make predictions on the test set.

<img width="302" alt="v10" src="https://github.com/farheenlatif/project/assets/88893044/8d8f138b-4626-40a0-9f4b-dee5623e7fdc">

The root mean squared error `RMSE` is calculated as a measure of the difference between the predicted export values and the actual export values for each country. The for loop iterates over each country's column in the dataset, appending the predicted export values and actual export values to separate lists, which are then used to calculate the overall RMSE for the dataset.

## ***Scoring Metric***
RMSE value of 0.056 means that the average difference between the predicted and actual export values for the test set, across all the countries, is about 5.6% of the range of the exported values. Since the exported values are scaled between 0 and 1, this means that the average difference between the predicted and actual export values for the test set is around 0.056, or 5.6% of the total range of the exported values. This is a reasonably low error rate and indicates that the model is performing well in predicting the future exports of these countries based on their past export patterns.

<img width="480" alt="v3" src="https://github.com/farheenlatif/project/assets/88893044/d23e6671-d935-4281-b5d5-459d02465e7e">

## ***How will you solve the problem?***
The importance of this project lies in its potential to help businesses and individuals develop
products with an eye towards future demand. Predicting future trade trends can help businesses
identify new markets to target, as well as optimize their supply chains and pricing strategies. It
can also help policymakers make informed decisions about trade policies and identify potential
areas for economic growth. Overall, this project has the potential to be a valuable tool for a wide
range of stakeholders in Pakistan and beyond.
We will explore new techniques to solve the problem at hand, specifically using LSTM and
regression models with lag features derived from previous years' trade data. By utilizing these
methods, we aim to improve our understanding and potentially achieve more accurate
predictions.Then it predicts the target variable by using the trained model model and the test input data X_test. The predicted values are stored in y_pred.The for loop iterates through each pair of predicted and actual values.The output shows the predicted value and actual value for each pair of observations in the test set.Then we plot the data into graphs to show visualizations.

<img width="475" alt="v4" src="https://github.com/farheenlatif/project/assets/88893044/0c8f7255-30e6-4994-8de9-f8a1e9647eee">

<img width="413" alt="v6" src="https://github.com/farheenlatif/project/assets/88893044/1ca05e21-aec8-4c2b-83ba-cd717e59484d">


