# Trend

Trend indicators measure the direction and strength of a trend by comparing prices to an established baseline.

## Simple Moving Average (SMA)

A simple moving average (SMA) calculates the average of a selected range of prices, usually closing prices, by the number of periods in that range. Used to identify trends and reversals, as well as to set up support and resistance levels (as any other moving average).

**Formula**

$sma(x,n) = \frac{\large x_0 + x_2 + ... + x_n}{n}$ 

where:

$x$ = the price series

$n$ = the number of periods

**Code!**

```kotlin
val data = dataOf("https://bulltimate.github.io/vista/amzn.csv")

val sma = data.sma(9)

println("The SMA(9) of last period is ${sma[0]}")
println("The SMA(9) of prev period is ${sma[1]}")
```

```console
The SMA(9) of last period is 2436.99
The SMA(9) of prev period is 2433.36
```

or using the `sma()` function for a specific series:

```kotlin
val sma = sma(series, 9)
```

More? see [Investopedia](https://www.investopedia.com/terms/s/sma.asp)

## Exponential Moving Average (EMA)

An exponential moving average (EMA) place a greater weight and significance on the most recent data points. The exponential moving average is also referred to as the exponentially weighted moving average. An exponentially weighted moving average reacts more significantly to recent price changes than a simple moving average (SMA), which applies an equal weight to all observations in the period.

**Formula**

$ema(x,n) = alpha * x + (1 - alpha) * ema(x_1,n)$

$alpha = \frac{2}{(n + 1)}$

where:

$x$ = the price series

$n$ = the number of periods

**Code!**

```kotlin
val data = dataOf("https://bulltimate.github.io/vista/amzn.csv")

val ema = data.ema(9)

println("The EMA(9) of last period is ${ema[0]}")
println("The EMA(9) of prev period is ${ema[1]}")
```

```console
The EMA(9) of last period is 2423.31
The EMA(9) of prev period is 2418.55
```

or using the `ema()` function for a specific series:

```kotlin
val ema = ema(series, 9)
```

More? see [Investopedia](https://www.investopedia.com/terms/e/ema.asp)

## Weighted Moving Average (WMA)

A weighted moving average (WMA) puts more weight on recent data and less on past data. This is done by multiplying each bar’s price by a weighting factor. Because of its unique calculation, WMA will follow prices more closely than a corresponding simple moving average (SMA).

**Formula**

$wma(x,n) = \frac{\large x_0 * w_0+ x_2 * w_2 + ... + x_n * w_n}{\normalsize w_0 + w_1 + ... + w_n}$ 

$w_i = n * (n - i)$

where:

$x$ = the price series

$n$ = the number of periods

**Code!**

```kotlin
val data = dataOf("https://bulltimate.github.io/vista/amzn.csv")

val wma = data.wma(9)

println("The WMA(9) of last period is ${wma[0]}")
println("The WMA(9) of prev period is ${wma[1]}")
```

```console
The WMA(9) of last period is 2430.76
The WMA(9) of prev period is 2428.96
```

or using the `wma()` function for a specific series:

```kotlin
val wma = wma(series, 9)
```

More? see [Fidelity](https://www.fidelity.com/learning-center/trading-investing/technical-analysis/technical-indicator-guide/wma)

## Volume Weighted Moving Average (VWMA)

The Volume-weighted Moving Average (VWMA) emphasizes volume by weighing prices based on the amount of trading activity in a given period of time. Users can set the length, the source and an offset. Prices with heavy trading activity get more weight than prices with light trading activity. In periods of low market volume, the SMA and the VWMA are close in value.

**Formula**

$vwma(x,n) = sma(x * volume, n) / sma(volume, n)$

where:

$x$ = the price series

$n$ = the number of periods (typically `20`)

**Code!**

```kotlin
val data = dataOf("https://bulltimate.github.io/vista/amzn.csv")

val vwma = data.vwma(20)

println("The VWMA(20) of last period is ${vwma[0]}")
println("The VWMA(20) of prev period is ${vwma[1]}")
```

```console
The VWMA(20) of last period is 2387.60
The VWMA(20) of prev period is 2394.71
```

or using the `vwma()` function for a specific series:

```kotlin
val vwma = vwma(series, 20)
```

## Hull Moving Average (HMA)

A hull moving average (HMA), developed by Alan Hull, is an extremely fast and smooth moving average. The HMA solves the age old dilemma of making a moving average more responsive to current price activity whilst maintaining curve smoothness. In fact the HMA almost eliminates lag altogether and manages to improve smoothing at the same time.

**Formula**

$hma(x,n) = wma(2 * wma(x,n/2) − wma(x,n)), sqrt(n))$

where:

$x$ = the price series

$n$ = the number of periods

**Code!**

```kotlin
val data = dataOf("https://bulltimate.github.io/vista/amzn.csv")

val hma = data.hma(9)

println("The HMA(9) of last period is ${hma[0]}")
println("The HMA(9) of prev period is ${hma[1]}")
```

```console
The HMA(9) of last period is 2405.99
The HMA(9) of prev period is 2407.17
```

or using the `hma()` function for a specific series:

```kotlin
val hma = hma(series, 9)
```

More? see [Alan Hull](https://alanhull.com/hull-moving-average)

## Moving Average Convergence/Divergence (MACD)

A moving average convergence divergence (MACD) is a trend-following momentum indicator that shows the relationship between two moving averages of a security’s price. The MACD is calculated by subtracting the 26-period exponential moving average (EMA) from the 12-period EMA. The result of that calculation is the MACD line. A nine-day EMA of the MACD called the "signal line" is then plotted on top of the MACD line, which can function as a trigger for buy and sell signals.

**Formula**

$macd(x,a,b) = ema(x,a) - ema(x,b)$

$signal(x,a,b,c) = ema(macd(x,a,b), c)$

$histogram = macd - signal$

where:

$x$ = the price series

$a$ = the number of periods of the fast ema (typically `12`)

$b$ = the number of periods of the slow ema (typically `26`)

$c$ = the number of periods of the signal line (typically `9`)

**Code!**

```kotlin
val data = dataOf("https://bulltimate.github.io/vista/amzn.csv")

val (macd, signal, hist) = data.macd()

println("The MACD(12,26,9) of last period is ${macd[0]} ${signal[0]} ${hist[0]}")
println("The MACD(12,26,9) of prev period is ${macd[1]} ${signal[1]} ${hist[1]}")
```

```console
The MACD(12,26,9) of last period is 48.39 59.15 -10.76
The MACD(12,26,9) of prev period is 49.76 61.84 -12.08
```

or using the `macd()` function for a specific series:

```kotlin
val (macd, signal, hist) = macd(series)
```


More? see [Investopedia](https://www.investopedia.com/terms/m/macd.asp)

## Elder-Ray Index

The Elder-Ray Index is a technical indicator developed by Dr. Alexander Elder that measures the amount of buying and selling pressure in a market. This indicator consists of three separate indicators known as "bull power" and "bear power", which are derived from a 13-period exponential moving average (EMA). The three indicator help traders determine the trend direction and isolate spots to enter and exit trades.

**Formula**

$BullBearPower = BullPower + BearPower$

$BullPower = high - ema(close, n)$

$BearPower = low - ema(close, n)$

where:

$n$ = the number of periods of the EMA (typically `13`)

**Code!**

```kotlin
val data = dataOf("https://bulltimate.github.io/vista/amzn.csv")

val (bb, bull, bear) = data.eri()

println("The Bull-Bear of last period is ${bb[0]}")
println("The Bull Power of last period is ${bull[0]}")
println("The Bear Power of last period is ${bear[0]}")
```

```console
The Bull-Bear of last period is 9.51
The Bull Power of last period is 26.84
The Bear Power of last period is -17.33
```

More? see [Investopedia](https://www.investopedia.com/terms/e/elderray.asp)