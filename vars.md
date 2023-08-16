vars:
smaFast(0),
smaMid(0),
emaMid30 (0),
ema3VerySlow (0),
emaVerySlow (0),
smaSlow(0),
emaSlow (0),
emaFast(0),
emafast1 (0),
demafast (0),
ema1preFast (0), 
ema2preFast (0), 
ema2Fast (0),
ema2Slow (0),
ema2verySlow (0),
rsiSlow(0),
rsiFast(0),
mom (0),
vwap(0), 
adxcalc (0),
buyingPower(0),
longbuyingPower (0),
longbuyingPower1 (0),
shortbuyingPower (0),
shortbuyingPower1 (0),

curProfit(0),
TakeProfitAmt (0),
StopAmt (0),
SwitchLargeSmall (0),
buydbg(""),
selldbg(""),
valsdbg(""),

//Donchian 
DonchianLength (21), 

//VOLUME
vVOL(0),
vAvgVol(0),
vTicks(0),
vAvgTicks(0),

//BB
vStd(0),
vBub1(0),
vBlb1(0),
vBub2(0),
vBlb2(0),
vBub3(0),
vBlb3(0),

//Satistical Arbitrage
Ratio (0),
MeanRatio (0),
devRatio (0),
Zscore (0),

// Trailing
barCount(0), // count from the first bar
high1stBar(0), // Extreme high from a list 
low1stBar(0), // Extreme low from a list 
trailProfit(0),
SmallTrailStop(SmallTrail ), //0.8
LargeTrailStop(largeTrail ),
FastTrailStop(FastTrail ), //0.38
intrabarpersist trailExit(0), // F1 Update on every tick
valuePercentTrail(0),

is_long_symbol(true),

//Macd
MACDLine (0),
SignalLine (0),
Histogram (0),

//PL for a day
NetProf(0),
PLTarget(0),

atr (0),

//Stoch
oData1FastK( 0 ),
oData1FastD( 0 ), 
oData1SlowK( 0 ),
oData1SlowD( 0 ), 
stochData1(0),
stochData2(0),

//Donchian
DonchianUp (0),
DonchianDown (0),
DonchianMid (0),

//RSI
vRSI (0),

crossind1 (false),
crossind2 (false),
crossind3 (false),

//vars:
longStop (-9999999);

