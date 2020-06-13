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
val data = dataOf("https://bulltimate.github.io/vista/amzn.csv")

val ic = data.ichimoku()

println("The Tenkan-Sen of last period is ${ic.ts[0]}")
println("The Tenkan-Sen of prev period is ${ic.ts[1]}")
```

```console
The Tenkan-Sen of last period is 2427.73
The Tenkan-Sen of prev period is 2427.73
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
val data = dataOf("https://bulltimate.github.io/vista/amzn.csv")

val ic = data.ichimoku()

println("The Kijun-Sen of last period is ${ic.ks[0]}")
println("The Kijun-Sen of prev period is ${ic.ks[1]}")
```

```console
The Kijun-Sen of last period is 2390.92
The Kijun-Sen of prev period is 2390.92
```

More? see [Investopedia](https://www.investopedia.com/terms/k/kijunsen.asp)

## Senkou Span A (Leading Span A)

The Leading Span A is a line used to measure momentum and can provide trade ideas based on support and resistance levels. It works in conjunction with the Senkou Span B line to form a cloud formation known as a "kumo." It is also called Leading Span A because the calculation is plotted 26 periods into the future, showing where support and resistance may form down the road.

**Formula**

$SSA = \frac{1}{2} * [TenkanSen + KijunSen]$

**Code!**

```kotlin
val data = dataOf("https://bulltimate.github.io/vista/amzn.csv")

val ic = data.ichimoku()

println("The Senkou Span A of last period is ${ic.ssa[0]}")
println("The Senkou Span A of prev period is ${ic.ssa[1]}")
```

```console
The Senkou Span A of last period is 2176.25
The Senkou Span A of prev period is 2157.23
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
val data = dataOf("https://bulltimate.github.io/vista/amzn.csv")

val ic = data.ichimoku()

println("The Senkou Span B of last period is ${ic.ssb[0]}")
println("The Senkou Span B of prev period is ${ic.ssb[1]}")
```

```console
The Senkou Span B of last period is 2043.52
The Senkou Span B of prev period is 2043.52
```

More? see [Investopedia](https://www.investopedia.com/terms/s/senkouspanb.asp)