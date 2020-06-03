# Momentum

Momentum is the measurement of the speed or velocity of price changes. These indicators identify the strength of a price movement, comparing the most recent closing price to a previous closing price from any time frame.

## Stochastic Oscillator

A stochastic oscillator is a momentum indicator comparing a particular closing price of a security to a range of its prices over a certain period of time. The sensitivity of the oscillator to market movements is reducible by adjusting that time period or by taking a moving average of the result. It is used to generate overbought and oversold trading signals, utilizing a 0-100 bounded range of values.

$\%K = \bigg(\frac{close - lowest(low,n)}{highest(high,n) - lowest(low,n)}\bigg) * 100$

$\%D = sma(\%K,3)$

where:

$n$ = the number of periods (typically `14`)

$highest(high,n)$ = the highest high price in $n$ periods back

$lowest(low,n)$ = the lowest low price in $n$ periods back

> An extra sma is typically applied to the %K to smooth the line (before calculate %D).

**Code!**

```kotlin
val close = seriesOf(*IntArray(50) { it })

val low = seriesOf(*IntArray(50) { it - it % 2 })
val high = seriesOf(*IntArray(50) { it + it % 2 })

val (k, d) = stoch(close, high, low)

println("The current %K value is ${k[0]}")
println("The current %D value is ${d[0]}")
```

```output
The current %K value is 95.24...
The current %D value is 96.03...
```

More? see [Investopedia](https://www.investopedia.com/terms/s/stochasticoscillator.asp)

## Commodity Channel Index (CCI)

A commodity channel index​ (CCI) is a momentum-based oscillator used to help determine when an investment vehicle is reaching a condition of being overbought or oversold. It is also used to assess price trend direction and strength.

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
val values = IntArray(20) { it % 2 }

val series = seriesOf(*values)

val rsi = rsi(series, 14)

println("The current value is ${rsi[0]}")
println("The previous value is ${rsi[1]}")
```

```output
The current value is 53.09...
The previous value is 49.30...
```

More? see [Investopedia](https://www.investopedia.com/terms/r/rsi.asp)