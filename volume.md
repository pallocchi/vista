# Volume

Volume indicators measure the strength of a trend to confirm a trading direction based on some form of averaging or smoothing of raw volume. The strongest trends often occur while volume increases, in fact, it is the increase in trading volume that can lead to large movements in price.

## Accumulation/Distribution (ADL)

The accumulation/distribution measure seeks to identify divergences between the stock price and volume flow. This provides insight into how strong a trend is. A strongly rising A/D line confirms a strongly rising price. Similarly, if the price is falling and the A/D is also falling, then there is still plenty of distribution and prices are likely to continue to decline. If the price is rising but the indicator is falling this indicates that buying or accumulation volume may not be enough to support the price rise and a price decline could be forthcoming.

**Formula**

$ADL = ADL_1 + MFV$

$MFV = \frac{(\small close - low) - (high - close)}{\small high - low} * volume$

where:

$ADL_1$ = the ADL of previous period

$MFV$ = the money flow volume

**Code!**

```kotlin
val close = seriesOf(1..20)
val volume = seriesOf(1..20)

val high = close * 2
val low = close * 0.5

val adl = accdist(close, high, low, volume)

println("The ADL of current period is ${adl[0]}")
println("The ADL of previous period is ${adl[1]}")
```

```output
The ADL of current period is -69.99...
The ADL of previous period is -63.33...
```

More? see [Investopedia](https://www.investopedia.com/terms/a/accumulationdistribution.asp)

## Chainkin Oscillator

The Chaikin oscillator is named for its creator Marc Chaikin. The purpose of the Chaikin oscillator is to identify underlying momentum during fluctuations in [accumulation/distribution](#accumulationdistribution-adl). For example, a trader wants to determine whether a stock price is more likely to go up or to fall and MACD is trending higher. The Chaikin oscillator generates a bullish divergence when it crosses above a baseline. The baseline is called the accumulation-distribution line. A cross above that line indicates that traders are accumulating, which is typically bullish.

**Formula**

$CO = ema(ADL, 3) - ema(ADL, 10)$

where:

$ADL$ = the accumulation/distribution line

**Code!**

```kotlin
val close = seriesOf(1..20)
val volume = seriesOf(1..20)

val high = close * 2
val low = close * 0.5

val chaikin = chaikin(close, high, low, volume)

println("The CO(3,10) of current period is ${chaikin[0]}")
println("The CO(3,10) of previous period is ${chaikin[1]}")
```

```output
The CO(3,10) of current period is -17.28...
The CO(3,10) of previous period is -16.20...
```

More? see [Investopedia](https://www.investopedia.com/terms/c/chaikinoscillator.asp)

## On-Balance Volume (OBV)

On-balance volume (OBV) is a technical trading momentum indicator that uses volume flow to predict changes in stock price. Joseph Granville first developed the OBV metric in the 1963 book Granville's New Key to Stock Market Profits. He believed that when volume increases sharply without a significant change in the stock's price, the price will eventually jump upward or fall downward.

More? see [Investopedia](https://www.investopedia.com/terms/o/onbalancevolume.asp)

## Volume Rate of Change

The volume rate of change is an indicator that shows whether or not a volume trend is developing in either an up or down direction. To calculate this, you need to divide the volume change over the last n-periods (days, weeks or months) by the volume n-periods ago. The answer is a percentage change of the volume over the last n-periods. Now, what does this mean? If the volume today is higher than n-days (or weeks or months) ago, the rate of change will be a plus number. If volume is lower, the ROC will be minus number. This allows us to look at the speed at which the volume is changing.

More? see [Investopedia](https://www.investopedia.com/articles/technical/02/091002.asp)