Support and Resistance levels with Brakes, Bear and Bull wick 4.0 by LuxAlgo
```
// This work is licensed under a Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0) https://creativecommons.org/licenses/by-nc-sa/4.0/
// © LuxAlgo

//@version = 4
study(title=" Support and Resistance Levels with Breaks",shorttitle = " Support and Resistance Levels with Breaks", overlay = true ,  max_bars_back=1000)
//
toggleBreaks  = input(true, title = "Show Breaks" )
leftBars  = input(15, title = "Left Bars ")
rightBars  = input(15, title = "Right Bars")
volumeThresh  = input(20, title = "Volume Threshold")
//
highUsePivot = fixnan(pivothigh(leftBars, rightBars)[1])
lowUsePivot = fixnan(pivotlow(leftBars, rightBars)[1])
r1 = plot(highUsePivot, color=change(highUsePivot) ? na : #FF0000,  linewidth=3, offset=-(rightBars+1), title="Resistance")
s1 = plot(lowUsePivot, color=change(lowUsePivot) ? na : #233dee,  linewidth=3, offset=-(rightBars+1), title="Support")

//Volume %
short = ema(volume, 5)
long = ema(volume, 10)
osc = 100 * (short - long) / long


//For breaks with volume
plotshape(toggleBreaks and crossunder(close,lowUsePivot) and not (open - close < high - open) and osc > volumeThresh, title = "Break", text = 'B', style = shape.labeldown, location = location.abovebar, color= color.red,textcolor = color.white, transp = 0, size = size.tiny)
plotshape(toggleBreaks and crossover(close,highUsePivot ) and not(open - low > close - open) and osc > volumeThresh, title = "Break", text = 'B', style = shape.labelup, location = location.belowbar, color= color.green,textcolor = color.white, transp = 0, size = size.tiny)

//For bull / bear wicks
plotshape(toggleBreaks and crossover(close,highUsePivot ) and open - low > close - open , title = "Break", text = 'Bull Wick', style = shape.labelup, location = location.belowbar, color= color.green,textcolor = color.white, transp = 0, size = size.tiny)
plotshape(toggleBreaks and crossunder(close,lowUsePivot) and open - close < high - open , title = "Break", text = 'Bear Wick', style = shape.labeldown, location = location.abovebar, color= color.red,textcolor = color.white, transp = 0, size = size.tiny)


alertcondition(crossunder(close,lowUsePivot) and osc > volumeThresh , title = "Support Broken" , message = "Support Broken")
alertcondition(crossover(close,highUsePivot) and osc > volumeThresh, title = "Resistance Broken" , message = "Resistance Broken")
```

SMA

```
study(title="Simple Moving Averages", shorttitle="SMA (7, 30, 50, 100, 200)", overlay=true)

outA = sma(close, 7)
outB = sma(close, 30)
outC = sma(close, 50)
outD = sma(close, 100)
outE = sma(close, 200)

plot(outA, color=yellow, title="SMA(7)")
plot(outB, color=fuchsia, title="SMA(30)")
plot(outC, color=lime, title="SMA(50)")
plot(outD, color=orange, title="SMA(100)")
plot(outE, color=red, title="SMA(200)")
```
