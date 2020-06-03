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
val series = seriesOf(1, 2, 3)

val sma = sma(series, 2)

println("The current value is ${sma[0]}")
println("The previous value is ${sma[1]}")
println("The oldest value is ${sma[2]}")
```

```console
The current value is 2.5
The previous value is 1.5
The oldest value is NaN
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
val series = seriesOf(1, 2, 3)

val ema = ema(series, 2)

println("The current value is ${ema[0]}")
println("The previous value is ${ema[1]}")
println("The oldest value is ${ema[2]}")
```

```console
The current value is 2.5
The previous value is 1.5
The oldest value is NaN
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
val series = seriesOf(1, 2, 3)

val wma = wma(series, 2)

println("The current value is ${wma[0]}")
println("The previous value is ${wma[1]}")
println("The oldest value is ${wma[2]}")
```

```console
The current value is 2.67
The previous value is 1.67
The oldest value is NaN
```

More? see [Fidelity](https://www.fidelity.com/learning-center/trading-investing/technical-analysis/technical-indicator-guide/wma)

## Hull Moving Average (HMA)

A hull moving average (HMA), developed by Alan Hull, is an extremely fast and smooth moving average. The HMA solves the age old dilemma of making a moving average more responsive to current price activity whilst maintaining curve smoothness. In fact the HMA almost eliminates lag altogether and manages to improve smoothing at the same time.

**Formula**

$hma(x,n) = wma(2 * wma(x,n/2) − wma(x,n)), sqrt(n))$

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

$b$ = the number of periods of the slow sma (typically `26`)

$c$ = the number of periods of the signal line (typically `9`)

**Code!**

```kotlin
val values = IntArray(50) { it }

val series = seriesOf(*values)

val (macd, signal, hist) = macd(series, 12, 26, 9)

println("The current macd value is ${macd[0]}")
println("The current signal value is ${signal[0]}")
println("The current histogram value is ${hist[0]}")
```

```output
The current macd value is 7
The current signal value is 7
The current histogram value is 0
```

More? see [Investopedia](https://www.investopedia.com/terms/m/macd.asp)