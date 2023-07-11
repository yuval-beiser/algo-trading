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
SmallMinProfit (0.1), //1.4 //1.5
smallbaseProfit (0.03),
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
LForDay (-50), //-1100
longSL(200), //
shortSL(200), //300
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
