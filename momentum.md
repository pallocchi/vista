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
val close = seriesOf(1..20)

val high  = close * 1.5
val low   = close * 0.5

val ao = ao(high, low)

println("The AO of current period is ${ao[0]}")
```

```output
The AO of current period is 14.5
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
val close = seriesOf(1..20)

val mom = mom(close, 10)

println("The MOM of current period is ${mom[0]}")
```

```output
The MOM of current period is 10
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
val series = seriesOf(1..25)

val cci = cci(series, 20)

println("The CCI(20) of current period is ${cci[0]}")
```

```output
The CCI(20) of current period is 126.67...
```

> Use the `typical()` series if you want to calculate the CCI of the typical price.

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
val series = seriesOf(1..20)

val rsi = rsi(series, 14)

println("The RSI(14) of current period is ${rsi[0]}")
```

```output
The RSI(14) of current period is 100
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
val close = seriesOf(1..20)

val high  = close * 1.5
val low   = close * 0.5

val (k, d) = stoch(close, high, low)

println("The %K of current period is ${k[0]}")
println("The %D of current period is ${d[0]}")
```

```output
The %K of current period is 62.76...
The %D of current period is 63.29...
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
val (k, d) = stochrsi(close)

println("The %K of current period is ${k[0]}")
println("The %D of current period is ${d[0]}")
```

```output
The %K of current period is 79.24...
The %D of current period is 81.22...
```

More? see [Investopedia](https://www.investopedia.com/terms/s/stochrsi.asp)

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
val close = seriesOf(1..20)

val high = close * 1.5
val low = close * 0.5

val r = williams(close, high, low, 14)

println("The %R of current period is ${r[0]}")
println("The %R of previous period is ${r[0]}")
```

```output
The %R of current period is -37.73...
The %R of previous period is -37.25...
```

More? see [Investopedia](https://www.investopedia.com/terms/w/williamsr.asp)