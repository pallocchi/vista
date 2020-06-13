# Volatility

Volatility indicators measure the rate of price movement, regardless of direction. This is generally based on change in the highest and lowest historical prices. They provide useful information about the range of buying and selling that take place in a given market and help traders determine points where the market may change direction.

## Bollinger Bands®

A Bollinger Band® is a technical analysis tool defined by a set of trendlines plotted two standard deviations (positively and negatively) away from a simple moving average (SMA) of a security's price, but which can be adjusted to user preferences. Bollinger Bands® were developed and copyrighted by famous technical trader John Bollinger, designed to discover opportunities that give investors a higher probability of properly identifying when an asset is oversold or overbought.

**Formula**

$basis(x,n) = sma(x,n)$

$upper(x,n,m) = basis(x,n) + m * \sigma$

$lower(x,n,m) = basis(x,n) - m * \sigma$

where:

$x$ = the price series

$n$ = the number of periods (typically `20`)

$m$ = the standard deviation factor (typically `2`)

$\sigma$ = the standard deviation

**Code!**

```kotlin
val data = dataOf("https://bulltimate.github.io/vista/amzn.csv")

val (middle, upper, lower) = data.bb()

println("The middle band of last period is ${middle[0]}")
println("The upper band of prev period is ${upper[1]}")
println("The lower band of prev period is ${lower1]}")
```

```console
The middle band of last period is 2394.18
The upper band of last period is 2495.96
The lower band of last period is 2292.41
```

More? see [Investopedia](https://www.investopedia.com/terms/b/bollingerbands.asp)

## Average True Range (ATR)

The average true range (ATR) is a technical analysis indicator that measures market volatility by decomposing the entire range of an asset price for that period. Specifically, ATR is a measure of volatility introduced by market technician J. Welles Wilder Jr. in his book, "New Concepts in Technical Trading Systems."

**Formula**

$tr = max((high-low), abs(high-close_1), abs(low-close_1))$

$atr(n) = \frac{1}{n}\sum_{i=1}^n(tr_i)$

where:

$n$ = the number of periods (typically `14`)

$close_1$ = the close price of previous period


**Code!**

```kotlin
val data = dataOf("https://bulltimate.github.io/vista/amzn.csv")

val wpr = data.atr()

println("The ATR(14) of last period is ${atr[0]}")
println("The ATR(14) of prev period is ${atr[1]}")
```

```console
The ATR(14) of last period is 64.11
The ATR(14) of prev period is 65.64
```

More? see [Investopedia](https://www.investopedia.com/terms/a/atr.asp)

## Standard Deviation

A standard deviation is a statistic that measures the dispersion of a dataset relative to its mean and is calculated as the square root of the variance. It is calculated as the square root of variance by determining the variation between each data point relative to the mean. If the data points are further from the mean, there is a higher deviation within the data set; thus, the more spread out the data, the higher the standard deviation.

**Formula**

$\sigma = \sqrt{\frac{1}{n}\sum_{i=1}^n(x_i-\mu)^{2}}$

where:

$\mu$ (mean) $=\frac{\small x_0 + x_2 + ... + x_n}{n}$ 

**Code!**

```kotlin
val data = dataOf("https://bulltimate.github.io/vista/amzn.csv")

val stdev = data.stdev(20)

println("The standard deviation of last period is ${stdev[0]}")
println("The standard deviation of prev period is ${stdev[1]}")
```

```console
The standard deviation of last period is 50.89
The standard deviation of prev period is 52.82
```

More? see [Investopedia](https://www.investopedia.com/terms/s/standarddeviation.asp)