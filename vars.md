vars:
shortStop (9999999),
longStop (-9999999),
smaFast(0),
smaMid(0),
ema3VerySlow (0),
emaVerySlow (0),
smaSlow(0),
emaSlow (0),
emaMid (0),
emaMid30 (0),
emaFast(0),
emafast1 (0),
demafast (0),
ema1preFast (0), 
ema2preFast (0), 
ema2Fast (0),
ema2Slow (0),
ema2verySlow (0),
ema2mid (0),
rsiSlow(0),
rsiFast(0),
AvgVolumeLength(50), //50
volumeUP (30), //10
mom (0),
//vwap(0), 
atr (0),
adxcalc (0),
longbuyingPower(0),
shortbuyingPower(0),
longbuyingPower1 (0),
shortbuyingPower1 (0),
longbuyingPower2 (0), 
shortbuyingPower2 (0),
curProfit(0),
TakeProfitAmt (0),
StopAmt (0),
SwitchLargeSmall (0),
buydbg(""),
selldbg(""),
valsdbg(""),
CurShares (0),

//macd
vMacd(0), 
vMacdAvg(0), 
vDiff(0) ,

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


//E-BB
stdclose (0),
evBub2 (0),
evBlb2 (0),

//BB HLOC
vBubHLOC (0),
vBlbHLOC (0),
HLOC  (0),
vBmbHLOC (0),
emaHLOC (0),
stdHLOC (0),
EHLOCupband  (0),
EHLOCdownband  (0),
EHLOCmidband (0),
EHLOCqtr1band (0),
EHLOCqtr3band (0),

//Keltner
vKeltUp(0),
vKeltDown(0),

//VOLUME
vVOL(0),
vAvgVol(0),
vTicks(0),
vAvgTicks(0),

//sqqq and tqqq gap
TQQQdaychange (0),
SQQQdaychange (0),
GapDAYTQQQSQQQ (0),
GapDAYSQQQTQQQ (0),

//PP
// Calculate Support and Resistance Levels
PP (0),
S1 (0),
S2 (0),
S3 (0),
R1 (0),
R2 (0),
R3 (0),

// Trailing
barCount(0), // count from the first bar
high1stBar(0), // Extreme high from a list 
low1stBar(0), // Extreme low from a list 
trailProfit(0),
SmallTrailStop(SmallTrail ), //4 pips 
LargeTrailStop(largeTrail ), //8 pips // 0.01875
FastTrailStop(0.34),
intrabarpersist trailExit(0), // F1 Update on every tick
valuePercentTrail(0),
is_long_symbol(true),

//PL for a day
NetProf(0),
PLTarget(0),

//RSI
vRSI (0), 

//Zaviot
MAValue1( 0 ),
MAValue2 ( 0 ),
MAValue3( 0 ), 
        
MASlope1( 0 ), // SHIPOOAA
MASlope2( 0 ), 
MASlope3( 0 ), 
        
MAAngle1( 0 ), // ZAVIT
MAAngle2( 0 ),
MAAngle3( 0 ),

AngleLong(FALSE),
AngleShort(FALSE),
BullAngle(FALSE), 
BearAngle(FALSE),         

//Donchian
DonchianUp (0),
DonchianDown (0),                 

//Stoch
oData1FastK( 0 ),
oData1FastD( 0 ), 
oData1SlowK( 0 ),
oData1SlowD( 0 ), 
stochData1(0),
stochData2(0),

//Macd
MACDLine (0),
SignalLine (0),
Histogram (0),

//Triangle
THign  (0),
TLow (0),
LTBreak (0),
STBreak (0),


//Extreme points
high5 (0),
low5 (0),
high9 (0),
low9 (0),

crossind1 (false),
crossind2 (false),

//exit
lastExitPrice (0),

crossind (false),

//stop
startlongSL(maximumloss),
updatedlongSL(maximumloss),
startshortSL (maximumloss),
updatedshortSL(maximumloss),
longSL (0),
shortSL (0);
