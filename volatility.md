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

```kotlin
val values = IntArray(50) { it }

val series = seriesOf(*values)

val (middle, upper, lower) = bb(series, 20, 2)

println("The current middle band value is ${middle[0]}")
println("The current upper band value is ${upper[0]}")
println("The current lower band value is ${lower[0]}")
```

```console
The current middle band value is 39.50...
The current upper band  value is 51.03...
The current lower band value is 27.97...
```

More? see [Investopedia](https://www.investopedia.com/terms/b/bollingerbands.asp)

## Average True Range (ATR)

The average true range (ATR) is a technical analysis indicator that measures market volatility by decomposing the entire range of an asset price for that period. Specifically, ATR is a measure of volatility introduced by market technician J. Welles Wilder Jr. in his book, "New Concepts in Technical Trading Systems."

More? see [Investopedia](https://www.investopedia.com/terms/a/atr.asp)

## Standard Deviation

A standard deviation is a statistic that measures the dispersion of a dataset relative to its mean and is calculated as the square root of the variance. It is calculated as the square root of variance by determining the variation between each data point relative to the mean. If the data points are further from the mean, there is a higher deviation within the data set; thus, the more spread out the data, the higher the standard deviation.

**Formula**

$\sigma = \sqrt{\frac{1}{n}\sum_{i=1}^n(x_i-\mu)^{2}}$

where:

$\mu$ (mean) $=\frac{\small x_0 + x_2 + ... + x_n}{n}$ 

**Code!**

```kotlin
val series = seriesOf(1, 2, 4)

val stdev = stdev(series, 2)

println("The current value is ${stdev[0]}")
println("The previous value is ${stdev[1]}")
println("The oldest value is ${stdev[2]}")
```

```console
The current value is 1
The previous value is 0.5
The oldest value is NaN
```

More? see [Investopedia](https://www.investopedia.com/terms/s/standarddeviation.asp)