//@version=Reversal Strategy ETF 5423-1
Inputs:
FastLength(9),
MidLength(20),
maxpositions (500),
MinLossForAdd (0.3),
SlowLength(50), //50
VerySlowLength(200),
RsiSlowLength(14),
RsiFastLength(14),
MinGapSlowToMid(2.1),//1.1 before change //0.5 //3.5.23 decrease from 2.4
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
MinFrom200 (0.2), //0.4 befoere change
MinProfitForTheDay(200),
MaxFromLH(4.5), //change to 4.5 just for testing. 3.6 seems too much. 31.3.23, change to 2.3. 3.5.23, change to 4.5 (improve on backtest).
MinFromLH (0.6), 
MaxFromLHEntry (1.2), 
MinFromLHEntry (0.15),
MinEMAGap (0.1), // 11.2.23, Increased from 0.16 for filtering false cross // 31.3.23, decrease from 0.24 to 0.16 
// 7.5.23, increase from 0.16           //0.45  
MaxEMAGap (1.35), // check if need to deacrease for Intrabar !!!  0.8, change to 1.5 just for testing
 // 7.5.23, increase from 0.8
Mingap (2), //1
MinFromCloseD1 (1),
MinGapboll (6.4),
SmallMinProfit (0.6), //1.4 //1.5 //1.6 //7.5.23, increase from 1.2 //9.5.23 decrease from 2 //1.5
LargeMinProfit (2.5), //2.5
SmallTrail (0.25), //0.04375 with stochastic //0.00625 //0.3 //0.2 //decrese from 0.4
largeTrail (1.6), //1.6
FastTrail (0.22),
MinBaseProfit (0.5), //
MinBaseProfit1 (0.5), //2 //1.6
CrossEMAos (0.1), //0.27 //0.25
FastMinProfit (1.8), //1
Minbarsfortake (2), //1
MinOpenGapPct (2),
ExitCrossOS (0.16),
StopLossOS (0.16),
adxperiod (14),
vwapLength (20), //20
adxmin(20),
MinBarsForMove(46), //50 //10 //46
MaxBarsForMove(2),
minbarsforcrossback (10), //12
AvgVolumeLength(30), //20 previus
volumeUP (10), //10 previus
double AccountBalance(40000), // Account balance 10,000 //80000
PctPerTrade(50),
Pctforadd (25),
TakeProfit (200),
TakeProfitPct (12),
StopPct (1.7), //30.4.23, Change from 2.5% //1.85
SL(200),
PForDay (50), //1500 //2000
LForDay (-50), //-1100 //-100
RatioLength (200),

//macd
macdFastLength( 12 ), 
macdSlowLength( 26 ), 
MACDlineLength( 9 ) ,

//BB
BStedDev1(1),
BStedDev2(2),
BStedDev3(3),
BStedDev5(5),
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
