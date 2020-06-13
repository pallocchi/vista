# Momentum

Momentum is the measurement of the speed or velocity of price changes. These indicators identify the strength of a price movement, comparing the most recent closing price to a previous closing price from any time frame.

## Awesome Oscillator (AO)

The Awesome Oscillator (AO) is an indicator used to measure market momentum. AO calculates the difference between a 34-period simple moving average (SMA) and 5-period SMA. The simple moving averages that are used are not calculated using closing price but rather each bar's midpoints. AO is generally used to affirm trends or to anticipate possible reversals.

**Formula**

$AO = sma(mid, 5) - sma(mid, 34)$

where:

$mid$ = $(high+low) / 2$

**Code!**

```kotlin
val data = dataOf("https://bulltimate.github.io/vista/amzn.csv")

val ao = data.ao()

println("The AO of last period is ${ao[0]}")
println("The AO of prev period is ${ao[1]}")
```

```console
The AO of last period is 43.90
The AO of prev period is 67.96
```

More? see [Tradingview](https://www.tradingview.com/scripts/awesomeoscillator/?solution=43000501826)

## Momentum Indicator (MOM)

The Momentum Indicator (MOM) is a leading indicator measuring a security's rate-of-change. It compares the current price with the previous price from a number of periods ago.The ongoing plot forms an oscillator that moves above and below 0. It is a fully unbounded oscillator and has no lower or upper limit. Bullish and bearish interpretations are found by looking for divergences, centerline crossovers and extreme readings.

**Formula**

$momentum(x,n) = x - x_n$

where:

$x$ = the price of current period

$x_n$ = the price of $n$ periods ago

$n$ = the number of periods (typically `10`)

**Code!**

```kotlin
val data = dataOf("https://bulltimate.github.io/vista/amzn.csv")

val mom = data.mom()

println("The MOM(10) of last period is ${mom[0]}")
println("The MOM(10) of prev period is ${mom[1]}")
```

```console
The MOM(10) of last period is 53.52
The MOM(10) of prev period is 33.18
```

More? see [Tradingview](https://www.tradingview.com/ideas/momentum/)

## Commodity Channel Index (CCI)

A commodity channel index​ (CCI) is a momentum-based oscillator used to help determine when an investment vehicle is reaching a condition of being overbought or oversold. It is also used to assess price trend direction and strength.

**Formula**

$cci(x,n) = \frac{\small x - sma(x,n)}{\small .015 * dev(x,n)}$

$dev(x,n) = \frac{1}{n} * \sum_{i=1}^n |x - sma(x,n)|$

where:

$x$ = the price series (usually the typical price)

$n$ = the number of periods (typically `20`)

**Code!**

```kotlin
val data = dataOf("https://bulltimate.github.io/vista/amzn.csv")

val cci = data.cci()

println("The CCI(20) of last period is ${cci[0]}")
println("The CCI(20) of prev period is ${cci[1]}")
```

```console
The CCI(20) of last period is 53.52
The CCI(20) of prev period is 33.18
```

or using the `cci()` function for a specific series:

```kotlin
val cci = cci(series, 20)
```

More? see [Investopedia](https://www.investopedia.com/terms/c/commoditychannelindex.asp)

## Relative Strength Index (RSI)

A relative strength index (RSI) is a momentum indicator used in technical analysis that measures the magnitude of recent price changes to evaluate overbought or oversold conditions in the price of a stock or other asset. The RSI is displayed as an oscillator (a line graph that moves between two extremes) and can have a reading from 0 to 100.

**Formula**

$rsi(x,n) = [100 - \frac{100}{(1 + \frac{\small\overline{G}}{\small\overline{L}})}]$

$\overline{G}$ (average gain) $= rma(max(x - x_1, 0), n)$

$\overline{L}$ (average loss) $= rma(max(x_1 - x, 0), n)$

where:

$x$ = the price series

$n$ = the number of periods (typically `14`)

$rma$ = the [EMA](/trend?id=exponential-moving-average-ema) with $alpha = \frac{1}{n}$

**Code!**

```kotlin
val data = dataOf("https://bulltimate.github.io/vista/amzn.csv")

val rsi = data.rsi()

println("The RSI(14) of last period is ${rsi[0]}")
println("The RSI(14) of prev period is ${rsi[1]}")
```

```console
The RSI(14) of last period is 58.90
The RSI(14) of prev period is 54.91
```

More? see [Investopedia](https://www.investopedia.com/terms/r/rsi.asp)

## Stochastic Oscillator

A stochastic oscillator is a momentum indicator comparing a particular closing price of a security to a range of its prices over a certain period of time. The sensitivity of the oscillator to market movements is reducible by adjusting that time period or by taking a moving average of the result. It is used to generate overbought and oversold trading signals, utilizing a 0-100 bounded range of values.

**Formula**

$\%K = \bigg(\frac{close - lowest(low,n)}{highest(high,n) - lowest(low,n)}\bigg) * 100$

$\%D = sma(\%K,3)$

where:

$n$ = the number of periods (typically `14`)

$highest(high,n)$ = the highest high price in $n$ periods back

$lowest(low,n)$ = the lowest low price in $n$ periods back

**Code!**

```kotlin
val data = dataOf("https://bulltimate.github.io/vista/amzn.csv")

val (k, d) = data.stoch()

println("The %K of last period is ${k[0]}")
println("The %D of last period is ${d[0]}")
```

```console
The %K of last period is 45.00
The %D of prev period is 45.80
```

More? see [Investopedia](https://www.investopedia.com/terms/s/stochasticoscillator.asp)

## Stochastic RSI (StochRSI)

The Stochastic RSI (StochRSI) is an indicator used in technical analysis that ranges between zero and one (or zero and 100 on some charting platforms) and is created by applying the [Stochastic oscillator](#stochastic-oscillator) formula to a set of relative strength index ([RSI](#relative-strength-index-rsi)) values rather than to standard price data. Using RSI values within the Stochastic formula gives traders an idea of whether the current RSI value is overbought or oversold.

**Formula**

$\%K = \bigg(\frac{rsi - lowest(rsi,m)}{highest(rsi,m) - lowest(rsi,m)}\bigg) * 100$

$\%D = sma(\%K,3)$

where:

$rsi(x,n)$ = the RSI of $x$ series for $n$ periods back

$highest(rsi,m)$ = the highest RSI in $m$ periods back

$lowest(rsi,m)$ = the lowest RSI in $m$ periods back

$n$ = the number of periods of the RSI (typically `14`)

$m$ = the number of periods of the Stochastic oscillator (typically `14`)

**Code!**

```kotlin
val data = dataOf("https://bulltimate.github.io/vista/amzn.csv")

val (k, d) = data.stochrsi()

println("The %K of last period is ${k[0]}")
println("The %D of last period is ${d[0]}")
```

```console
The %K of last period is 11.64
The %D of prev period is 9.45
```

More? see [Investopedia](https://www.investopedia.com/terms/s/stochrsi.asp)

## Ultimate Oscillator (UO)

The Ultimate Oscillator (UO) is a technical indicator that was developed by Larry Williams in 1976 to measure the price momentum of an asset across multiple timeframes. By using the weighted average of three different timeframes the indicator has less volatility and fewer trade signals compared to other oscillators that rely on a single timeframe. Buy and sell signals are generated following divergences. The Ultimately Oscillator generates fewer divergence signals than other oscillators due to its multi-timeframe construction.

**Formula**

$UO = \bigg(\frac{(AVG_{n1} * 4) + (AVG_{n2} * 2) + AVG_{n3}}{4 + 2 + 1}\bigg) * 100$

where:

$AVG_n = (\sum_{i=1}^n BP) / (\small\sum_{i=1}^n TR)$

$BP = close - min(low, close_1)$

$TR$ = the true range

$n1$ = the number of periods for first time frame (typically `7`)

$n2$ = the number of periods for second time frame (typically `14`)

$n3$ = the number of periods for third time frame (typically `28`)

**Code!**

```kotlin
val data = dataOf("https://bulltimate.github.io/vista/amzn.csv")

val uo = data.uo()

println("The UO of last period is ${uo[0]}")
println("The UO of prev period is ${uo[1]}")
```

```console
The UO of last period is 52.40
The UO of prev period is 47.81
```

More? see [Investopedia](https://www.investopedia.com/terms/u/ultimateoscillator.asp)

## Williams %R

Williams %R, also known as the Williams Percent Range, is a type of momentum indicator that moves between 0 and -100 and measures overbought and oversold levels. The Williams %R may be used to find entry and exit points in the market. The indicator is very similar to the Stochastic oscillator and is used in the same way. It was developed by Larry Williams and it compares a stock’s closing price to the high-low range over a specific period, typically 14 days or periods.

**Formula**

$\%R = \bigg(\frac{highest(high,n) - close}{highest(high,n) - lowest(low,n)}\bigg) * -100$

where:

$n$ = the number of periods (typically `14`)

$highest(high,n)$ = the highest high price in $n$ periods back

$lowest(low,n)$ = the lowest low price in $n$ periods back

**Code!**

```kotlin
val data = dataOf("https://bulltimate.github.io/vista/amzn.csv")

val wpr = data.wpr()

println("The %R of last period is ${wpr[0]}")
println("The %R of prev period is ${wpr[1]}")
```

```console
The %R of last period is -42.51
The %R of prev period is -63.62
```

More? see [Investopedia](https://www.investopedia.com/terms/w/williamsr.asp)