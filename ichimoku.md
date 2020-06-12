# Ichimoku Cloud

The Ichimoku Cloud is a collection of technical indicators that show support and resistance levels, as well as momentum and trend direction. It does this by taking multiple averages and plotting them on the chart. It also uses these figures to compute a "cloud" which attempts to forecast where the price may find support or resistance in the future.

## Tenkan-Sen (Conversion Line)

Tenkan-Sen, or Conversion Line, is the mid-point of the highest and lowest prices of an asset over the last nine periods. The Tenkan-Sen is the fastest moving line in the Ichimoku Cloud indicator.

**Formula**

$TS = \frac{1}{2} * [highest(high, 9) + lowest(low, 9)]$

where:

$highest(high,9)$ = the highest high price in 9 periods back

$lowest(low,9)$ = the lowest low price in 9 periods back

**Code!**

```kotlin
val low = seriesOf(1..100)
val high = seriesOf(2..101)

val ichimoku = ichimoku(high, low, 9, 26, 52, 26)

println("The Tenkan-Sen of current period is ${ichimoku.ts[0]}")
println("The Tenkan-Sen of previous period is ${ichimoku.ts[1]}")
```

```output
The Tenkan-Sen of current period is 96.5
The Tenkan-Sen of previous period is 95.5
```

More? see [Investopedia](https://www.investopedia.com/terms/t/tenkansen.asp)


## Kijun-Sen (Base Line)

The Kijun-sen is the midpoint price of the last 26-periods, and therefore an indicator of short- to medium-term price momentum. The indicator aids in assessing the trend, and can also be useful for identifying trading opportunities when combined with the other components of the Ichimoku cloud.

**Formula**

$KS = \frac{1}{2} * [highest(high, 26) + lowest(low, 26)]$

where:

$highest(high,26)$ = the highest high price in 26 periods back

$lowest(low,26)$ = the lowest low price in 26 periods back

**Code!**

```kotlin
val low = seriesOf(1..100)
val high = seriesOf(2..101)

val ichimoku = ichimoku(high, low, 9, 26, 52, 26)

println("The Kijun-Sen of current period is ${ichimoku.ks[0]}")
println("The Kijun-Sen of previous period is ${ichimoku.ks[1]}")
```

```output
The Kijun-Sen of current period is 88.0
The Kijun-Sen of previous period is 87.0
```

More? see [Investopedia](https://www.investopedia.com/terms/k/kijunsen.asp)

## Senkou Span A (Leading Span A)

The Leading Span A is a line used to measure momentum and can provide trade ideas based on support and resistance levels. It works in conjunction with the Senkou Span B line to form a cloud formation known as a "kumo." It is also called Leading Span A because the calculation is plotted 26 periods into the future, showing where support and resistance may form down the road.

**Formula**

$SSA = \frac{1}{2} * [TenkanSen + KijunSen]$

**Code!**

```kotlin
val low = seriesOf(1..100)
val high = seriesOf(2..101)

val ichimoku = ichimoku(high, low, 9, 26, 52, 26)

println("The Senkou Span A of current period is ${ichimoku.ssa[0]}")
println("The Senkou Span A of previous period is ${ichimoku.ssa[1]}")
```

```output
The Senkou Span A of current period is 67.25
The Senkou Span A of previous period is 66.25
```

More? see [Investopedia](https://www.investopedia.com/terms/s/senkouspana.asp)

## Senkou Span B (Leading Span B)

The Leading Span B works in conjunction with the Senkou Span A line to form a cloud formation known as a "kumo." The cloud provides support and resistance levels. Both Senkou Span A and B are plotted 26 periods into the future, providing a glimpse into where support and resistance may form next.

**Formula**

$SSB = \frac{1}{2} * [highest(high, 52) + lowest(low, 52)]$

where:

$highest(high,52)$ = the highest high price in 52 periods back

$lowest(low,52)$ = the lowest low price in 52 periods back

**Code!**

```kotlin
val low = seriesOf(1..100)
val high = seriesOf(2..101)

val ichimoku = ichimoku(high, low, 9, 26, 52, 26)

println("The Senkou Span B of current period is ${ichimoku.ssb[0]}")
println("The Senkou Span B of previous period is ${ichimoku.ssb[1]}")
```

```output
The Senkou Span B of current period is 50.0
The Senkou Span B of previous period is 49.0
```

More? see [Investopedia](https://www.investopedia.com/terms/s/senkouspanb.asp)