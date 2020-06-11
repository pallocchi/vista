# Vista, technical analysis

!> Vista is currently under heavy development 🛠

Vista is a technical analysis library for Kotlin, inspired in [Pine Script][ps] from TradingView.

```kotlin
val fast = sma(close, 9)
val slow = sma(close, 30)

when {
    fast crossOver slow -> print("I'm going long!")
    fast crossUnder slow -> print("I'm going short!")
}
```

# Loading the market data

All starts with... data! before using any indicator, you have to load the market data.

```kotlin
val data = Data()

data.add(
  Data.Bar(
    date = "05/29/2020",
    open = 2361.01,
    high = 2391.37,
    low = 2353.21,
    close = 2388.85,
    volume = 3648128.0
  )
)
```

Now you have your first bar! let's see what we can do with this in the next section.

# Working with series

Almost anything in Vista is a series, that's why it's the most important thing you need to learn. Series are structures that allow us to use the data in a more fashion way. 

Let's start with a simple series of numbers:

```kotlin
val series = seriesOf(1,2,3)
```

The `seriesOf` function is a simple way to create a series and it's enough for this example. 

## Accesing values

So, we have our series, let's try to get its values:

```kotlin
val lastValue = series[0]       // last value is 3
val previousValue = series[1]   // previous value is 2
val oldestValue = series[2]     // oldest value is 1
```

Since Vista is inspired in [Pine Script][ps], the way to get values from a series is pretty similar, using the array accesory `[]` and passing as an argument the number of periods to look back. Fortunately, since the last and previous values are frequently used, we provide a shortcut to get these values: `last` and `prev` fields.

```kotlin
val lastValue = series.last       // same as series[0]
val previousValue = series.prev   // same as series[1]
```

## Operators and series

Series can be operated just like numbers:

```kotlin
val x = seriesOf(1,2,3)
val y = seriesOf(2,4,6)

val sum = y + x // sum is (3,6,9)
val dif = y - x // dif is (1,2,3)
val mul = y * x // mul is (2,8,18)
val div = y / x // div is (2,2,2)
```

and it also works for numbers:

```kotlin
val x = seriesOf(1,2,3)

val sum = x + 1 // sum is (2,3,4)
```

## Working with previous periods

As you already know, using the `[]` accesory in a series you can get values from past periods, for instance, with `x[1]` you get the previous value of the `x` series. But now let's suppose we want to create a series which is the change between the value at a given period, and the previous one:

$change(x) = x - x_1$

> Note in this guide we use $x_1$ to represent the previous value

We need to create another series which is the original one ($x$) but delayed by 1 period.

#### Shifting series

Using the invoke operator like `(n)` we can delay a series by `n` periods.

```kotlin
val x = seriesOf(1,2,3) // x is (1,2,3)
val y = x(1)            // y is (1,2)

print("The last value in x is ${x.last}")
print("The last value in y is ${y.last}")
```
```output
The last value in x is 3
The last value in y is 2
```

So back to our example, we can implement the `change()` function in this way:

```kotlin
val x = seriesOf(1,3,6)

val change = x - x(1) // change is (2,3)
```

Since `x(1)` returns a series, we are getting the difference between both series: the original and the [shifted](#shifting-series) one.

## Basic series

We saw the `seriesOf` function which is really useful to learn Vista, but it's more likely you use what we call the basic series, which are basically views of the [data](#data) you already know. These are the `open`, `high`, `low`, `close` and `volume` series, that can be created using the homonymous functions.

```kotlin
val open = open(data)       // series of close prices
val high = high(data)       // series of high prices
val low = low(data)         // series of low prices
val close = close(data)     // series of close prices
val volume = volume(data)   // series of volume prices
```

Based on the previous series, we can derive another one called the typical price.

$typical = \frac{\small close + high + low}{3}$

Since this series is widely used, we have the built-in function `typical()`.

```kotlin
val typical = typical(data) // series of typical prices
```

# Introduction to indicators

The core of the technical analysis are indicators. Vista has many common indicators out of the box that you can find in next sections of this guide, and many others are comming in next releases. But in any case you can always create your custom indicators in a really simple way, using the functions already supported by Vista. 

For instance, let's see how we can implement the classic MACD indicator, which is calculated by subtracting the 26-period exponential moving average (EMA) from the 12-period EMA. This is the Vista-way to create it:

```kotlin
fun macd(source: Series) = ema(source, 26) - ema(source, 12)
```

Simple, right? now you can use your new indicator just like `macd(close)`. Of course you don't actually need to implement this indicator since Vista has a built-in [function][macd] for that, but it's a great example of how you can create new indicators based on the already implemeted ones, thanks to the fluidity of working with series.

?> Vista only performs the calculation of the values when they are actually needed.

### Built-in indicators

| Name                                                     | Type       | Leading | Lagging | Since |
|----------------------------------------------------------|:----------:|:-------:|:-------:|:-----:|
| [Accumulation/Distribution (ADL)][adl]                   | Volume     | ✔       | -       | 0.0.1 |
| [Average True Range (ATR)][atr]                          | Volatility | -       | ✔       | 0.0.1 |
| [Awesome Oscillator (AO)][ao]                            | Momentum   | ✔       | -       | 0.1.0 |
| [Bollinger Bands®][bb]                                   | Volatility | -       | ✔       | 0.0.1 |
| [Chainkin Oscillator][chaikin]                           | Volume     | ✔       | -       | 0.0.1 |
| [Commodity Channel Index (CCI)][cci]                     | Momentum   | ✔       | -       | 0.0.1 |
| [Exponential Moving Average (EMA)][ema]                  | Trend      | -       | ✔       | 0.0.1 |
| [Hull Moving Average (HMA)][hma]                         | Trend      | -       | ✔       | 0.0.1 |
| [Momentum (MOM)][mom]                                    | Momentum   | ✔       | -       | 0.1.0 |
| [Moving Average Convergence/Divergence (MACD)][macd]     | Trend      | ✔       | -       | 0.0.1 |
| [On-Balance Volume (OBV)][obv]                           | Volume     | ✔       | -       | 0.0.1 |
| [Relative Strength Index (RSI)][rsi]                     | Momentum   | ✔       | -       | 0.0.1 |
| [Simple Moving Average (SMA)][sma]                       | Trend      | -       | ✔       | 0.0.1 |
| [Standard Deviation][stdev]                              | Volatility | -       | ✔       | 0.0.1 |
| [Stochastic Oscillator][stoch]                           | Momentum   | ✔       | -       | 0.0.1 |
| [Stochastic RSI][stochrsi]                               | Momentum   | ✔       | -       | 0.1.0 |
| [Volume Rate of Change (VROC)][vroc]                     | Volume     | -       | ✔       | 0.0.1 |
| [Volume Weighted Moving Average (VWMA)][vwma]            | Trend      | -       | ✔       | 0.1.0 |
| [Weighted Moving Average (WMA)][wma]                     | Trend      | -       | ✔       | 0.0.1 |
| [Williams %R][williams]                                  | Momentum   | ✔       | -       | 0.1.0 |

# About rules and strategies

Rules are the way to detect entry and exit signals. Let's suppose we want to implement a classic strategy of moving average crossovers. This strategy uses two simple moving averages (SMA) with different periods (slow and fast), and we want to go long whenever the 9-period SMA crosses over the 30-period SMA, and go short when the frist one crosses under the other. In order to do that, we have the `crossOver` and `crossUnder` rules, which are available in any series and we can use that in this way:

```kotlin
val fast = sma(close, 9)
val slow = sma(close, 30)

when {
    fast crossOver slow -> print("I'm going long!")
    fast crossUnder slow -> print("I'm going short!")
}
```

Amazing! we've just implemented our very basic strategy.

If you are familiar with [Pine Script][ps], you can also use the `crossover()` and `crossunder()` functions and it works in the same way (actually those functions use the previous ones under the covers). Take a look at the KDoc.

[ps]: https://www.tradingview.com/pine-script-docs/en/v4/Introduction.html

[adl]: volume?id=accumulationdistribution-adl
[atr]: volatility?id=average-true-range-atr
[ao]: momentum?id=awesome-oscillator-ao
[bb]: volatility?id=bollinger-bands®
[chaikin]: volume?id=chainkin-oscillator
[cci]: momentum?id=commodity-channel-index-cci
[ema]: trend?id=exponential-moving-average-ema
[hma]: trend?id=hull-moving-average-hma
[macd]: trend?id=moving-average-convergencedivergence-macd
[mom]: momentum?id=momentum-indicator-mom
[obv]: volume?id=on-balance-volume-obv
[rsi]: momentum?id=relative-strength-index-rsi
[sma]: trend?id=simple-moving-average-sma
[stdev]: volatility?id=standard-deviation
[stoch]: momentum?id=stochastic-oscillator
[stochrsi]: momentum?id=stochastic-rsi-stochrsi
[vroc]: volume?id=volume-rate-of-change-vroc
[vwma]: trend?id=volume-weighted-moving-average-vwma
[wma]: trend?id=weighted-moving-average-wma
[williams]: momentum?id=williams-r