//@version=Reversal Strategy ETF 5423-1
Inputs:
FastLength(9),
MidLength(20),
SlowLength(50), //50
VerySlowLength(200),
RatioLength (200),
RsiSlowLength(14),
RsiFastLength(14),
MinGapSlowToMid(1.4),//1.1 before change //0.5 //2.4
RsiMinForLong(40),
RsiMaxForShort(60),
MomentumLength(14),
Longminmom (-0.3),
Shortmaxmom (0.3),
ExitBarNum1(12),
ExitBarNum2(24),
ExitBarNum3(36),
ExitBarNum (5),
AtrLength (14),
MinProfitAfter1Hour(100),
MinProfitAfter2Hours(150),
MinProfitAfter3Hours(180),
CloseAfter1Hour(20),
CloseAfter2Hour(20),
CloseAfter3Hour(40),
MinFrom200 (0.2), //0.4 befoere change
MinProfitForTheDay(200),
MaxFromLH(2.3), //change to 4.5 just for testing. 3.6 seems too much. change to 2.2 (31.3.23). //2.2
MinFromLH (0.6),
MaxFromLHEntry (1.2),
MinFromLHEntry (0.15),
MinEMAGap (0.16), // 11.2.23, Increased from 0.16 for filtering false cross // decrease from 0.24 to 0.16 (31.3.23)           
MaxEMAGap (0.8), // check if need to deacrease for Intrabar !!!  0.8, change to 1.5 just for testing
Mingap (1),
MinFromCloseD1 (1),
SmallMinProfit (0.03), //1.4 //1.5 //0.1
smallbaseProfit (0.2),
LargeMinProfit (2.5),
SmallTrail (0.01875), //0.04375 with stochastic //0.00625 //0.3
largeTrail (1.6),
FastTrail (0.22),

MinBaseProfit (1.5), //
MinBaseProfit1 (2), 
CrossEMAos (0.27),
FastMinProfit (1.8), //1
Minbarsfortake (2), //1
MinOpenGapPct (2),
ExitCrossOS (0.16),
StopLossOS (0.16),
adxperiod (14),
vwapLength (20), //20
adxmin(20),
MinBarsForMove(46), //50 //10
AvgVolumeLength(30), //20 previus
volumeUP (10), //10 previus
double AccountBalance(40000), // Account balance 10,000 //80000
PctPerTrade(50),
LongMultiplierPower (1),
TakeProfit (200),
TakeProfitPct (6),
StopPct (2.1), //30.4.23, Change from 2.5% 
SL(240),
PForDay (2000), //1500
LForDay (-180), //-1100
longSL(220), //
shortSL(220), //300
os1 (0.0133), //0.03 - offset 
os2 (0.01),
os3 (0.0133), // 2$ - 0.133 precent 



//BB
BStedDev1(1),
BStedDev2(2),
BStedDev3(3),
BUpperBand(200),
BLowerBand(200),
MinFromBB (0.24),
MaxFromBB (0.8),


//Stoch
StochPiriod1( 5 ), //14
//StochPiriod2( 14 ),
StochLength1( 3 ), 
StochLength2( 3 ),
StochOverBot(74), //78
StochOverSold(26), //22
stochmid (50),


//RSI
RSIOverbot (60),
RSIoversold (40),

//Zscore
longminzscore (-2),
shortminzscore (2);


vars:
smaFast(0),
smaMid(0),
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


shortStop (9999999),
longStop (-9999999),

//Extreme points
high5 (0),
low5 (0),
high9 (0),
low9 (0);
