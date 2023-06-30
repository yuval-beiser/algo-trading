//@version=31323-2
Inputs:

FastLength(9),
MidLength(20),
SlowLength(50),
length (5),
VerySlowLength (200),
stdDevMultiplier2 (2),
RsiSlowLength(10),
RsiFastLength(8),
TLength (21),
SLength (21),
MinGapSlowToMid(0.1),
RsiMinForLong(40),
RsiMaxForShort(60),
MomentumLength(14),
Longminmom (-0.3),
Shortmaxmom (0.3),
ExitBarNum1(12),
ExitBarNum2(24),
ExitBarNum3(36),
ExitBarNum (5),
MinProfitAfter1Hour(100),
MinProfitAfter2Hours(150),
MinProfitAfter3Hours(180),
CloseAfter1Hour(20),
CloseAfter2Hour(20), 
CloseAfter3Hour(40),
MinProfitForTheDay(200),
MaxFromLH(0.2), //0.16875
MinFromLH (0.12),
MaxFromSR (0.2),
MaxFromLHEntry (0.75),
MinFromLHentry (0.15),
MinKeltnerCross (0.08),
MinemaGap (0.0005), // 0.01875
MaxemaGap (0.025), //0.22  
Mingap (0.05), //0.06 was too tight according to 8.3.23 , 3:03 AM //0.15
Maxgap (0.05), //
Maxgap1 (0.06), //0.2
MinProfit (0.00625),
smallbaseProfit (0.03125), //0.035
SmallMinProfit (0.03125), //after 12 pips start trail of 4 pips //0.075 with stochastic //0.0925 //0.25 //0.2
largeMinProfit (0.04375), //after 10 pips start trail of 8 pips //0.09375
SmallMinProfitPart1 (0.05), //after 3 pips limit 3 at the middle of the chanel
SmallMinProfitPart2 (0.0375), //after 6 pips limit at the other side of the channel
MinProfitforadd (0.07),
MaxProfitForAdd (0.1),
FastMinProfit (0.0625), //0.1125
MinBaseProfit (0.03),
MinLossForAdd (0.1), //0.1
SmallTrail (0.01875), //0.04375 with stochastic //0.00625 //0.0125 //0.025
largeTrail (0.025),
MinSQQQTQQQGap (0.09),
Minbarsfortake (5), //2
MinBarsForMove (30), //12
MaxBarsforadd (1),
maxpositions (3),
MinbarsHL (5),
ExitCrossOS (0.14),
StopLossOS (0.01875),
adxperiod (14),
adxmin(25),
vwapLength (20),
SQQQTQQQGap(0.15),
AtrLength (14),
AtrMin(15), //0.6
Atrmax (1.8),
ANGLE_MA1( 8), //25
ANGLE_MA2( 60 ),
ANGLE_MA3( 70 ), 
TailHammerRatio (7),
MinChanel (3),
MaxChanel (10),
Hlocpartlong (2),
Hlocpartshort (2),
LTpct (0.3),
STpct (0.3),
RatioLength (200),
ppLength (5),
os1 (0.015),

PForDay (400), //1500 //1950 //100 //800
LForDay (-60), //-1100 //-500 //-50

//Donchian 
DonchianLength (20), 

//macd
macdFastLength( 12 ), 
macdSlowLength( 26 ), 
MACDlineLength( 9 ) ,

//BB
BStedDev1(1),
BStedDev2(1.5), //1.5
BStedDev3(3),
BUpperBand(200),
BLowerBand(200),
MinFromBB (0.24),
MaxFromBB (0.8),

//BB HLOC
BStedDevHLOC (2), 
BUpperBandHLOC(21), //39
BLowerBandHLOC(21), //39

//Keltner
KStdAtr(1.5),
KUpperBand(43),
KLowerBand(43),


//Stoch
StochPiriod1( 5 ), //14
//StochPiriod2( 14 ),
StochLength1( 5 ), 
StochLength2( 4 ),
StochOverBot(74), //76
StochOverSold(26), //14
stochmid (50),

//RSI
RSIOverbot (70),
RSIoversold (46),

double AccountBalance(10000), // Account balance 10,000 $
PctPerTrade(50),
TakeProfit (200),
TakeProfitPct (6.5),
StopPct (0.025),
longSL(50), //180 with stochastic //140 //80 //450 //400 //300
shortSL(50), //300

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
emaMid (0),
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
AvgVolumeLength(50), //50
volumeUP (30), //10
mom (0),
vwap(0), 
atr (0),
adxcalc (0),
longbuyingPower(0),
shortbuyingPower(0),
longbuyingPower1 (0),
shortbuyingPower1 (0),
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

longStop (-9999999),
shortStop (9999999);
