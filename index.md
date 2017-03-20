### Moving Averages
We will be using the following library

```
library(forecast)
```

## 12-Term Centered Moving Average for the Monthly Start Series

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
![original resid dist](https://github.com/xinyix/Moving-Average/blob/master/sales.png?raw=true)