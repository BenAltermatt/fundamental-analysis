# Fundamental And Sentiment Analysis

This is my semester long project for Machine Learning (CS 4824).

---

## Overview

The goal behind this project was initially to attempt to use machine learning techniques to exploit market inefficiencies by combining algorithms designed to perform fundamental analysis on stocks with sentiment analysis algorithms built to summarize expert opinions on the value of stocks through articles. The scope of a problem like this is exceedingly large and some simplifying assumptions and decisions have been made to give more space in which to work.

## Fundamental Analysis (Model A)

The first, and more overarching model that I plan on developing is a classification model that does fundamental analysis. The model should look something like this:

|Aspect of Model| Description|
|--|--|
| Feature Space (***X***) | A set of heuristics used for fundamental analysis which I haven't completely decided upon yet. Some of the existing options for the values include: P/E, EPS, PEG, FCF, P/B, ROE, DPR, P/S, Divident-to-Yield, D/E, and maybe some more.|
| Label Space (***Y***) | A value indicating whether this buy would have been more profitable than a concurrent buy of the S&P 500 at the time of purchase. Likely {-1, 1} where -1 is a "bad buy" and 1 is a "good buy"|
| Loss Function ***L(y, yi)*** | |

## Sentiment Analysis (Model B)

This is a repository for a project surrounding the use of sentiment analysis along with fundamental analysis-based regression to build portfolios for stock choices.

---

## Developer's Log

Apparently earnings per share and diluted earnings per share are different things and I have to figure out which one to use in the feature set.

There is also the consideration that a lot of the features I have are based on the same underlying data points. I could accidentally be overrepresenting values, but maybe training will even that out.

I desperately need a way to either calculate price from the data set I have currently or to find a data set that will give me info about prices. I think it will likely be the latter.

### Data set search

It has been kind of a pain to find data sets. Many are locked behind pretty hefty pay walls, so I decided that I would use one that is based on 10k SEC reportings for companies listed on the market and just try to calculate the values of interest to build my own data set. This could go poorly, but I don't have a ton of money to drop on this kind of thing and I think I may have a better chance of learning more about this process if I have some hand in the development of this data set.

### Equations for Heuristics

I need to be able to calculate a lot of values for the heuristics I plan on plugging in to the model, so I have decided on a more consolidated feature set I am going to aim for and I am going to write the equations for the values I find here.

- **Earnings Per Share:**
*This one is given*

- **Price to Earnings Ratio P/E:**
$$PE = \frac{Price}{EPS}$$
Where *price* is the price per share and *EPS* is earnings per share.

- **Price Earnings Growth Rate PEG:**

- ***This Section was not completed as it quickly became unimportant***

### Building the data set

It has come to my attention that the most useful next move is most likely going to be just building the data set from the API I have. This is something I will need to do relatively carefully, given the fact that APIs can be rate limited and I have a limited amount of time to actually build this data set. The data set I am currently thinking of will consist of data points as follows:

#### Features

Again, these were essentially chosen from a large number of otions with guidance from this article at [Investor Academy](https://investoracademy.org/top-10-fundamental-analysis-indicators-for-all-investors/).

|name|id in api|abbreviation|
|--|--|--|
|Price-to-Earnings Ratio| peRatio| pe|
|Earings per share | netIncomePerShare| eps|
|Free Cash Flow per Share | freeCashFlowPerShare| fcf|
|Price to Book Ratio | pbRatio| pb |
|Return on Equity | roe| roe|
|Dividend Payout Ratio | payoutRatio| dpr|
|Dividend Yield Ratio | dividendYield| yield|
|Debt to Equity Ratio | debtToEquity| de|
|Price to Sales Ratio | priceToSalesRatio| ps|

#### Labels

- 1 if the stock is more performative than the S&P 500
- -1 if the stock is less perfomative than the S&P 500

I think I need to make a simplifying assumption here to make the model work. Maybe I will say more performative for the S&P 500 over 6 months. I chose this time period because the average holdng period for stocks is about 5.5 months according to [smartasset.com](https://smartasset.com/investing/what-is-the-average-stock-holding-period).

I do not yet know how I should store this data. Part of the reason being, I don't know how I am going to use multiple separate dates for the same stocks. I remember the timeline or continuity possibly presenting a problem with building data sets like this previously so I am wary of making poor assumptions with my data set.

#### Shape of Data

I don't yet completely know what I want my final data to look like because I am still unsure of what models I want to try, but for now I will prioritize making the data currently more accessible. To me, this means my data might look something like:

```txt
ticker, buy date, pe, eps, fcf, pb, roe, dpr, yield, de, ps, label
```
