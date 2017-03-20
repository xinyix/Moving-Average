## Moving Averages
We will be using the following library

```
library(forecast)
```

### 12-Term Centered Moving Averages for the Monthly Start Series

```
housing <- read.csv("Monthly_US_Housing_Starts_Private_Single_1965_1975.csv", header=FALSE)
housing <- as.vector(ts(housing, frequency=12))
> housing
  [1]  52.149  47.205  82.150 100.931  98.408  97.351  96.489  88.830  80.876  85.750  72.351  61.198  46.561  50.361  83.236  94.343  84.748  79.828  69.068  69.362  59.404
 [22]  53.530  50.212  37.972  40.157  40.274  66.592  79.839  87.341  87.594  82.344  83.712  78.194  81.704  69.088  47.026  45.234  55.431  79.325  97.983  86.806  81.424
 [43]  86.398  82.522  80.078  85.560  64.819  53.847  51.300  47.909  71.941  84.982  91.301  82.741  73.523  69.465  71.504  68.039  55.069  42.827  33.363  41.367  61.879
 [64]  73.835  74.848  83.007  75.461  77.291  75.961  79.393  67.443  69.041  54.856  58.287  91.584 116.013 115.627 116.946 107.747 111.663 102.149 102.882  92.904  80.362
 [85]  76.185  76.306 111.358 119.840 135.167 131.870 119.078 131.324 120.491 116.990  97.428  73.195  77.105  73.560 105.136 120.453 131.643 114.822 114.746 106.806  84.504
[106]  86.004  70.488  46.767  43.292  57.593  76.946 102.237  96.340  99.318  90.715  79.782  73.443  69.460  57.898  41.041  39.791  39.959  62.498  77.777  92.782  90.284
[127]  92.782  90.655  84.517  93.826  71.646  55.650

housing_12ma <- ma(housing, order=12, centre=TRUE)

plot(housing, type="l", col="blue", ylab="Monthly Starts (in thousands of units)", xlab="Months since Jan 1965", main="Monthly US Housing Starts of \n Privately Owned Single-Family Structures")
lines(housing_12ma, type="l", col="red")
legend("topright", legend=c("Time Series", "12-Term MA"), col=c("blue", "red"), lty=1:1)
```
![original resid dist](https://github.com/xinyix/Moving-Average/blob/master/housing.png?raw=true)

Moving averages allows us to estimate the trend-cycle at time t by averaging values of the time series within some periods of t. Averaging (applying equal weights) to the observations around a point eliminates the randomness in the data. Thus in the plot shown above, the resulting curve (in red) represents a smoothed trend of our data. 

### 4-Term Centered Moving Averages for the Quarterly Expenditure Series
```
expenditures <- read.csv("Quarterly_US_Plant_Equip_Expenditures_1964_1976.csv", header=FALSE)
expenditures <- as.vector(ts(expenditures, frequency=4))
> expenditures
 [1] 10.00 11.85 11.70 13.42 11.20 13.63 13.65 15.93 13.33 16.05 15.92 18.22 14.46 16.69 16.20 18.12 15.10 16.85 16.79 19.03 16.04 18.81 19.25 21.46 17.47 20.33 20.26 21.66
[29] 17.68 20.60 20.14 22.79 19.38 22.01 21.86 25.20 21.50 24.73 25.04 28.48 24.10 28.16 28.23 31.92 25.82 28.43 27.79 30.74 25.87 29.70 30.41 34.52

expenditures_4ma <- ma(expenditures, order=4, centre=TRUE)

plot(expenditures, type="l", col="blue", ylab="Quarterly Expenditures (in billions of dollors)", xlab="Quarters since First Quarter in 1964", main="Quarterly New Plant and Equipment Expenditures in US Industries")
lines(expenditures_4ma, type="l", col="red")
legend("topright", legend=c("Time Series", "4-Term MA"), col=c("blue", "red"), lty=1:1)
```
![original resid dist](https://github.com/xinyix/Moving-Average/blob/master/expenditures.png?raw=true)

The plot above shows the trend of order 4 for the expenditure series. 
