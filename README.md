# Time Series Forecasting for Mass Shootings in the U.S. (1966-2021)

## Abstract

According to the $2^{nd}$ Amendment of the United States Constitution, it states *"A well regulated Militia, being necessary to the security of a free State, the right of the people to keep and bear Arms, shall not be infringed"*. In light of the increase of mass shootings and more frequent gun violence in recent years, the discussion concerning the $2^{nd}$ Amendment has gravitated towards becoming a large looming controversy over the American people, and in turn these discussion are seemingly intensifying a political polarization across the country.  

In this study, we will be utilizing a dataset from the Kaggle Database: [Mass Shootings in the United States of America](https://www.kaggle.com/datasets/zusmani/us-mass-shootings-last-50-years?resource=download&select=Mass+Shootings+Dataset.csv), which has recorded various attributes from a shocking $398$ mass shootings that occurred in the United States between the years $1966 - 2021$. With this dataset, the aim of this study is to use *Time Series Analysis* and *Time Series Forecasting* in `R` as a means of predicting the future of the United States and its people, in terms of the presence of mass shootings and gun violence. Focusing on the `Date` and `Total_Victims` features of our dataset, this study will be forecasting the total number of victims (both fatalities and injuries) in the United States for future mass shootings if the state of the nation does not change.  

After preliminary Exploratory Time Series Analysis, it was concluded that a Box-Cox Transformation of the series was best suited to creating a stationary series. After further examination of the transformed series, a first-order differencing at lag 1 was proven to make the series nearly entirely stationary. Next, after analyzing the ACF and PACF plots of the Box-Cox Transformed series differenced at lag 1, some preliminary assumed models were chosen, with a primary assumption of an $ARIMA(1, 1, 1)$ model.  

Moving onto more in depth model comparison, 6 models were considered and compared using the Second-Order Akaike Information Criterion (AICc) and the Bayesian Information Criterion (BIC) tests. As a result, the suitable models were narrowed down to the $ARIMA(0, 0, 1)$, $ARIMA(1, 0, 1)$, and $ARIMA(1, 0, 0)$ models, no longer considering $ARIMA(1, 1, 1)$. Moving these 3 models onto the diagnostic testing stage of the study, after examining visualizations of these models' residuals using Histograms, Normal QQ Plots, Time Series Plots, ACF Plots, PACF Plots, ACF Plots of Squared Residuals; and by evaluating some statistical tests such as the Shapiro-Wilk Test, Box-Pierce Test, Box-Ljung Test, and Box-Ljung Test of Squared Residuals: all models proved to be suitable. Next, the invertibility of the models were evaluated using plots of their unit roots, which also did not prove to be a useful method of narrowing down a final model (as all models were invertible). Hence, our final model was chosen based off of previously computed AICc and BICs, leaving our final model chosen to be an $ARIMA(0, 0, 1)$ or in back-shift operator notation: $\Delta_1 BoxCox(U_t) = (1 + (-0.8818)_{(0.1859)}B)Z_t$. Although the best possible fitting model found, an $ARIMA(0, 0, 1)$ proved not to be the most accurate forecast for predicting the years $2016 - 2021$, an attempt to forecast 9 years into the future of the data $2022 - 2030$ was computed.  

During this great time of sadness, fear, and chaos in the United States, its important to recognize the role that Data Science and statistical methods of research as a whole can play in helping the future of millions of lives. Although this study's forecasting model underestimated the number of mass shooting victims that would occur, perhaps this is more telling? In the hands of the wrong people, this type of research has the potential to spread possibly false statistics that discourage action. Throughout this time series forecasting analysis, it has become evident that these looming issues of gun violence and mass shootings have an exponential increase that could not be foreseen by statistical processes, meaning we have an extremely urgent matter that calls for a way to decrease its trend in order to save the lives of the millions it effects.  

## Introduction

The political divide among the people of the United States has always been present, but in more recent years, this gap between those of different political affiliations appears to widen more and more.  With the growing use of social media to spread videos and ideas in a more efficient manner, new issues and conversations are brought to light, being more easily accessible than ever before. One of these topics of conversation is the issue of increased *Mass Shootings* and *Gun Violence* in the United States. According to various sources, the United States has consistently been the country awarded with the highest number of mass shootings. Although this idea  is objective, factual, numerical, and has been widely known for years, the numbers of mass shootings per year seems to grow exponentially. A controversial topic that seems to be choosing between protecting the lives of primarily children in schools or protecting ones' selves with arms, is an issue in this country that has yet to be solved.  

As stated prior, the [Mass Shootings in the United States of America (1966-2021)](https://www.kaggle.com/datasets/zusmani/us-mass-shootings-last-50-years?resource=download&select=Mass+Shootings+Dataset.csv) dataset from Kaggle will be utilized in this study, which was originally compiled by Zeeshan-Ul-Hassan Usmani. This dataset was allegedly created using multiple sources including "Wikipedia, Mother Jones, Stanford, USA Today and other web sources" (as stated in his acknowledgements), and was given a Kaggle usability score of $7.94$: a score out of $10$ that Kaggle assigns data sets based on their completeness, credibility, and compatibility in order to inform users the validity of the data that is presented.  

Rather than acting as a model of inference showing all the different factors that could explain the increase in the numbers of mass shootings, gun violence, and victims, this time series model will serve as a tool to forecast this dataset and show how these numbers will potentially look like in our near future if this current trend is to continue. Although this study isn't meant to take into account all or even many factors as to why this increase in mass shootings is occurring, creating a window into what this forecasted data may appear like in the future may hopefully incite some further discussion and possible urgency in the hands of all people who have the power to change the current and future state of this nation.  

## R Packages

For this study, data cleaning and time series analysis will be completed using the `R` programming language. We will be utilizing the following packages in `R` throughout the duration of this study...  

```{r}
library(knitr)
library(ggplot2)
library(ggfortify)
library(tinytex)
library(dplyr)
library(tidyverse)
library(MASS)
library(tseries)
library(devtools)
library(forecast)
library(UnitCircle)
library(MuMIn)
```
