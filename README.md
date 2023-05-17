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
