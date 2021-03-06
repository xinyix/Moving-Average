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

### (3x3)-Term Moving Averages and Henderson's Five-Term Moving Averages for the Demand Series
The (3x3)-Term Moving Averages of the demand series is given by first applying a 3-Term Centered Moving Averages, then apply it again on the resulting series. 
```
demand <- read.csv("Monthly_Demand_Repair_Parts_Iowa_1972_1979.csv", header=FALSE)
demand <- as.vector(ts(demand, frequency=12))
> demand
 [1]  954  765  867  940  913 1014  801  990  712  959  828  965  915  891  991  971 1129 1091 1195 1295 1046 1121 1033 1222 1199 1012 1404 1137 1421 1162 1639 1545 1420
[34] 1916 1491 1295 1764 1727 1654 1811 1520 1635 1984 1898 1853 2015 1709 1667 1625 1562 2121 1783 1474 1657 1746 1763 1517 1457 1388 1501 1227 1342 1666 2091 1629 1451
[67] 1727 1736 1952 1420 1345  842 1576 1485 1928 2072 1887 2175 2199 1961 2091 1993 1595 1372 1607 1871 2594 1743 2267 2602 2565 2567 2344 2805

demand_3ma <- ma(demand, order=3, centre=TRUE)
demand_3x3ma <- ma(demand_3ma, order=3, centre=TRUE) 

plot(demand, type="l", col="blue", ylab="Monthly Demand (in thousands of dollors)", xlab="Months since Jan 1972", main="Monthly Demand for Repair Parts \n for a Large Heavy-Equipment Manufacture in Iowa")
lines(demand_3x3ma, type="l", col="red")
legend("topright", legend=c("Time Series", "3x3-Term MA"), col=c("blue", "red"), lty=1:1)
```
![original resid dist](https://github.com/xinyix/Moving-Average/blob/master/demand_3x3ma.png?raw=true)
We can see the smoothed series (in red) traces out the approximate ups and downs in our data, however, a larger order of moving averages would smooth out the series even further. An example is the 12-Term Moving Averages shown above. 

Next we smooth the series using Henderson's Five-Term Moving Averages. We first obtain the weights of a Five-Term Moving Averages, the function henderson(n) returns the weights of a n-Term Moving Averages and is attached at the end
```
H5_wts <- henderson(5)

n <- length(demand)
demand_H5 <- matrix(NA, 1, n)

for (i in 3:(n-2)) {
	demand_H5[i] <- H5_wts %*% demand[(i-2):(i+2)]
}

plot(demand, type="l", col="blue", ylab="Monthly Demand (in thousands of dollors)", xlab="Months since Jan 1972", main="Monthly Demand for Repair Parts \n for a Large Heavy-Equipment Manufacture in Iowa")
lines(as.vector(demand_H5), type="l", col="red")
legend("topright", legend=c("Time Series", "Henderson(5) MA"), col=c("blue", "red"), lty=1:1)
```
![original resid dist](https://github.com/xinyix/Moving-Average/blob/master/demand_H5ma.png?raw=true)

Compared to the (3x3)-Term Moving Average, the Henderson's 5-Term approach traces out the approximate fluctuations in the series more closely. 

The function henderson(n) is provided below
```
## The following code is provided by simonholgate
## You can find it here: https://github.com/simonholgate/R-Scripts/blob/master/henderson.R

henderson <- function(n) {
	r <- (n - 1)/2

	C0 <- (315/8)*(3*r^2 + 12*r - 4)/(64*r^9 + 1152*r^8 + 8592*r^7 + 34272*r^6 + 78204*r^5 + 99288*r^4 + 57203*r^3 - 4302*r^2 - 19323*r - 5670)
	C1 <- (3465/8)*-1/(64*r^9 + 1152*r^8 + 8592*r^7 + 34272*r^6 + 78204*r^5 + 99288*r^4 + 57203*r^3 - 4302*r^2 - 19323*r - 5670)

	# Hard code for test of n=5
	#  C0 <- 1.5617323E-4
	#  C1 <- -5.4836106E-5


	# Solve for coefficients using matrices as suggested by CW
	#  Xa <- 0
	#  Xb <- 0
	#  Yb <- 0
	#  for (i in -r:r){
	#    Xa <- Xa + 
	#      ((r + 1)^2 - i^2)*((r + 2)^2 - i^2)*((r + 3)^2 - i^2)
	#    Xb <- Xb + 
	#      ((r + 1)^2 - i^2)*((r + 2)^2 - i^2)*((r + 3)^2 - i^2)*i^2
	#    Ya <- Xb
	#    Yb <- Yb + 
	#      ((r + 1)^2 - i^2)*((r + 2)^2 - i^2)*((r + 3)^2 - i^2)*i^4
	#  }
	#  Mat1 <- matrix(c(Xa,Xb, Ya,Yb), nrow = 2, ncol=2, byrow=TRUE)
	#  Mat2 <- matrix(c(1,0), nrow=2)
	#  C <- solve(Mat1,Mat2)

	# wk are the weights from -r to r
 	 wk <- vector(mode="numeric", length=n)
  	for (i in -r:r){
  	  wk[i+(r+1)] <- 
   	   ((r + 1)^2 - i^2)*((r + 2)^2 - i^2)*((r + 3)^2 - i^2)*(C0 + C1*i^2)
	#      ((r + 1)^2 - i^2)*((r + 2)^2 - i^2)*((r + 3)^2 - i^2)*(C[1] + C[2]*i^2)
 	 }

	# Return the weights to the calling function
 	 wk
}
```
