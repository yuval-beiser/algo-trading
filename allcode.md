//@version=31323-2
Inputs:
maximumloss(80), //120
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
Mingap1 (0.01),
Maxgap (0.25), //0.O5
Maxgap1 (0.667), //0.2 //0.02
Maxgap2 (0.05), //0.2
maxgap3 (0.09),
maxgap4 (0.26),

MinProfit (0.00625),
smallbaseProfit (0.03), //0.035 //0.19 //0.02 //0.1
SmallMinProfit (0.1), //after 12 pips start trail of 4 pips //0.075 with stochastic //0.0925 //0.25 //0.2 //0.05
SmallMinProfit1 (0.05), 
largeMinProfit (0.04375), //after 10 pips start trail of 8 pips //0.09375
SmallMinProfitPart1 (0.05), //after 3 pips limit 3 at the middle of the chanel //0.05
SmallMinProfitPart2 (0.0375), //after 6 pips limit at the other side of the channel
MinProfitforadd (0.01),
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
maxpositions (6),
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
os1 (0.0133), //0.03 - offset 
os2 (0.01),
os3 (0.0133), // 2$ - 0.133 precent 

PForDay (1500), //1500 //1950 //100 //800
LForDay (-200), //-1100 //-500 //-50

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

//Zscore
longminzscore (-2),
shortminzscore (2);

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

//exit
lastExitPrice (0),

//stop
startlongSL(maximumloss),
updatedlongSL(maximumloss),
startshortSL (maximumloss),
updatedshortSL(maximumloss),
longSL (0),
shortSL (0);

//[IntrabarOrderGeneration = True] //trade intra-bar

//when no position reset CurShares - number of micro positions in same time 
if marketposition = 0
then
CurShares = 0;

//when no position use close bar
if marketposition = 0
then
[IntrabarOrderGeneration = true] //trade intra-bar


emaFast = XAverage(close,FastLength);
emaMid = XAverage(close,MidLength);
emaSlow = XAverage(close,SlowLength);
emafast1 = XAVERAGE(XAVERAGE(close,FastLength),FastLength);
demafast = emaFast * 2 - emafast1  ;    
emaverySlow = XAverage(close,VerySlowLength);
//ema2Fast = XAverage(close,FastLength) of data2;
//ema2Slow = 0;//XAverage(close ,slowLength) of data2;
//ema2verySlow = XAverage(close,VerySlowLength)of data2;
//ema2mid = XAverage(close,MidLength) of data2;
adxcalc = ADX(adxperiod);
longbuyingPower = 2 ;//(AccountBalance/Close)*PctPerTrade/100; // the amount of shares i can buy //1 //3
longbuyingPower1 = 1; // scale in-out
longbuyingPower2 = 3;
shortbuyingPower = 2 ; //3
shortbuyingPower1 = 1 ; // scale in-out
shortbuyingPower2 = 3 ;


CurShares = GetPositionQuantity (getsymbolname, GetAccountID);

// long stoploss
if 
CurShares = 1 
then 
longSL = startlongSL
else 
longSL = updatedlongSL;

// short stoploss
if 
CurShares = 1
then 
shortSL = startshortSL
else 
shortSL = updatedshortSL;


//TakeProfitAmt = AccountBalance*PctPerTrade/100*TakeProfitPct/100;
//StopAmt = AccountBalance*PctPerTrade/100*StopPct/100;
valsdbg = "close=" + NumToStr(close ,2) + " dailyhigh=" + NumToStr(dailyhigh ,2) + " dailylow =" + NumToStr(dailylow ,2); // + " close =" + NumToStr(close ,2) + " close =" + NumToStr(close ,2) + " close =" + NumToStr(close ,2) + " close =" + NumToStr(close ,2) + " close =" + NumToStr(close ,2);
//print(Date, Time, "bar=", BarNumber, marketposition, valsdbg ); 


//BB HLOC 21
vBubHLOC = BollingerBand(HLOC ,BUpperBandHLOC,BStedDevHLOC);
vBlbHLOC = BollingerBand(HLOC ,BLowerBandHLOC, - BStedDevHLOC);
vBmbHLOC = (vBubHLOC+vBlbHLOC)/2;
HLOC = (HIGH+LOW+OPEN+CLOSE)/4;

emaHLOC = XAverage (HLOC , BUpperBandHLOC);
stdHLOC = StdDev(HLOC , BUpperBandHLOC);

EHLOCupband = emaHLOC + stdHLOC ;
EHLOCdownband = emaHLOC  - stdHLOC ;
EHLOCmidband = (EHLOCupband+EHLOCdownband)/2;
EHLOCqtr1band = EHLOCdownband+((EHLOCupband-EHLOCdownband)/4);
EHLOCqtr3band = EHLOCupband-((EHLOCupband-EHLOCdownband)/4);

//BB 200 Regular
vBub1= BollingerBand(close,BUpperBand,BStedDev1);
vBlb1= BollingerBand(close,BLowerBand, - BStedDev1);
  
vBub2= BollingerBand(close,BUpperBand,BStedDev2);
vBlb2= BollingerBand(close,BLowerBand, - BStedDev2);

vBub3= BollingerBand(close,BUpperBand,BStedDev3);
vBlb3= BollingerBand(close,BLowerBand, - BStedDev3);


//BB 200 Exponencial
stdclose = StdDev (close, VerySlowLength);
evBub2 = emaverySlow + (stdDevMultiplier2 * stdclose) ;
evBlb2 = emaverySlow - (stdDevMultiplier2 * stdclose) ;

{
//VWAP crossing
vwap = Average(HLOC * Volume, vwapLength ) / Average(Volume, vwapLength );
}
//macd
vMacd = MACD( Close, macdFastLength, macdSlowLength ) ; // Fast line MACD
vMacdAvg = XAverage( vMacd , MACDlineLength) ; // Slow line MACD
vDiff = vMacd - vMacdAvg ; // Histogram

//Keltner
vKeltUp = KeltnerChannel(HLOC ,KUpperBand,KStdAtr);
vKeltDown = KeltnerChannel(HLOC ,KLowerBand,-KStdAtr);

//ATR
atr =  AvgTrueRange (AtrLength);

// Calculate a switch for identify long or short (for the connection with VXX)
if symbol = "SOXS" or symbol = "LABD" or symbol = "SQQQ" then
is_long_symbol = False;

//volume calc
//vTicks = Ticks ;
vAvgTicks= AverageFC( Ticks, AvgVolumeLength) ;

//Zaviot
MAValue1 = XAverage( Close, FastLength ) ; 
MASlope1 = ( MAValue1 - MAValue1[1] );// * (Minmove/Pricescale);  // SLOPE = Shipooaa 
MAAngle1 = ArcTangent( MASlope1 ) ; // ZAVIT = Press F1 to see explain
         
MAValue2 = XAverage( Close,MidLength  ) ; 
MASlope2 = ( MAValue2 - MAValue2[1]);// * (Minmove/Pricescale)  ; 
MAAngle2 = ArcTangent( MASlope2 ) ; 
         
MAValue3 = XAverage( Close, SlowLength ) ; 
MASlope3 = ( MAValue3 - MAValue3[1] );// * (Minmove/Pricescale)  ; 
MAAngle3 = ArcTangent( MASlope3 ) ; 

BullAngle = ((MAValue1 > MAValue2) And (MAValue2 > MAValue3)) ;//And (Close Crosses Over  MAValue1);
BearAngle = ((MAValue1 < MAValue2) And (MAValue2 < MAValue3)) ; //And (Close Crosses Under  MAValue1);
AngleLong  = (( MAAngle1 > ANGLE_MA1) And (MAAngle1 < ANGLE_MA2 ));
AngleShort = (( MAAngle1 < ANGLE_MA1 * (-1)) And (MAAngle1 > ANGLE_MA2 * (-1)) );

//Donchian
DonchianUp = HighestFC (h, DonchianLength );
DonchianDown = LowestFC (l, DonchianLength );

//Stoch
stochData1  = Stochastic( H, L, C, StochPiriod1, StochLength1, StochLength2, 1, 
oData1FastK, oData1FastD, oData1SlowK, oData1SlowD ) ; 

//RSI
vRSI = RSI (close, RsiFastLength);

//Triangle
//The upper boundary or resistance level of the ascending triangle pattern
THign = Highest(High, TLength);

//The lower boundary or support level of the ascending triangle pattern
TLow = Lowest(low, TLength);

//breakout level
LTBreak = THign  + (TLow - THign)* LTpct;
STBreak = THign  + (TLow - THign)* STpct;

//high and low level
high5 = maxlist(close [1] , open [1], close [2] , open [2], close [3] , open [3], close [4] , open [4], close [5] , open [5] );
low5 = minlist (close [1] , open [1], close [2] , open [2], close [3] , open [3], close [4] , open [4], close [5] , open [5] );

high9 = maxlist(close [1] , open [1], close [2] , open [2], close [3] , open [3], close [4] , 
open [4], close [5] , open [5], close [6] , open [6], close [7] , open [7], close [8] , open [8], close [9] , open [9] );

low9 = minlist (close [1] , open [1], close [2] , open [2], close [3] , open [3], close [4] , 
open [4], close [5] , open [5], close [6] , open [6], close [7] , open [7], close [8] , open [8], close [9] , open [9] );


//Macd
MACDLine = MACD(Close, 12, 26); // Close price, short period, long period
SignalLine = XAverage(MACDLine, 9); // Signal line is a 9-period EMA of the MACD line
Histogram = MACDLine - SignalLine;

//PP
// Calculate Support and Resistance Levels
PP = 
(
HighestFC(high,ppLength) + LowestFC(low,ppLength) + Close[1] 
) /3;
S1 = (2 * PP) - HighestFC(high, ppLength);
S2 = PP - (HighestFC (high, ppLength) - LowestFC(low, ppLength));
S3 = LowestFC(low, ppLength) - 2 * (HighestFC (high, ppLength) - PP);
R1 = (2 * PP) - LowestFC(low, ppLength);
R2 = PP + (HighestFC(high, ppLength) - LowestFC(low, ppLength));
R3 = HighestFC(high, ppLength) + 2 * (PP - LowestFC (low, ppLength));

{
//Zcore - Ratio between 2 stocks
Ratio = close / close of data2;
MeanRatio = Average (Ratio , RatioLength);
DevRatio = StdDev (MeanRatio , RatioLength);
Zscore = (Ratio - MeanRatio) / DevRatio ;
}

//Exit
//lastExitPrice = ExitPrice (1); //Assign a value, indicating the exit price of the most recently closed position. 1 - the last position closed (one position back);


//PL for a day
if DATE <> DATE[1] 
then 
begin
NetProf = NetProf + NetProfit - NetProf[1];
end;
PLTarget = Netprofit - NetProf;


if marketposition = 0 //Conditions Entry Long
and
(
(PLTarget < PForDay) and (PLTarget > LForDay) //1
)  
and
//(
//(Time > 1400.00) or (Time < 1200.00 and Time > 430.00) or (Time < 1200.00 and Time < 300.00) //2
//)
//and
close > Open //3
//and
//(close-open) >(close[1]-open[1])* 1.3
and
close > high5
//and
//low5 < emaVerySlow *
//and
//close > maxlist (close [1], open [1]) //high

{
and
(
open [1] > emaverySlow and open [2] > emaverySlow 
and
Close [1] > emaverySlow and Close [2] > emaverySlow 
)
}
and
close > emaMid //20
and
close > emaverySlow * (1 + os3 /100)  //200

//and
//emaMid > emaVerySlow

//and
//emaMid >= emaverySlow * (1+Mingap/100) //from 10 
//and
//emaMid <= emaverySlow * (1+Maxgap/100) //*
and
close <= emaverySlow * (1+Maxgap1/100) //*
//and
//close < low5 * (1+maxgap4/100) *
//and
//close <= low * (1+maxgap3/100) *
//and
//close of data2 > ema2Fast
//and
//close of data2 > ema2mid 
//and
//Mom >= 0
//and
//low < low [1]

//and
//close cross above emaFast

//and
//close >= emaMid * (1+Mingap1/100) //till 8 
//and
//close <= emaMid * (1+Maxgap2/100) //till 8 

//and
//(
//(close cross above emaFast) or (close [1] cross above emaFast[1]) or  (close [2] cross above emaFast[2])
//)
//and
//Histogram > 0

then 
begin
buy longbuyingPower Shares next bar at market  ;
end;


{
if marketposition = 1 //Scale In  - Conditions Add Entry long
and
close > open
//and
//close [1] <= open [1]

//close > high [1]
//high5 < emaVerySlow
and
close cross above EHLOCupband
and
close cross above high9
//and
//close > emaVerySlow
//and
//close cross above emaFast
//and
//close >= DonchianUp
//and
//Histogram > 0
//and
//close cross above emaFast

//and
//close > emaMid
//and
//high5 < emaMid
//and
//low < low [1]
//and
//close < open [1]
//and
//close[1] >= open[1]
//and
//close < emaFast
//and
//(Close/entryprice-1)*100 > MinProfitforadd 
//and
//(1-close/entryprice)*100 > 0
//and
//barssinceentry > 20
and
CurShares < maxpositions 
then 
begin
buy longbuyingPower1 Shares next bar at market  ;
end;

}

{
if marketposition = 1 //Scale In x3 - Conditions Add Entry long
//and
//close > emaMid
and
high5 < emaMid
and
close [1] <= open [1]
and
low < low [1]
and
close cross above emaMid
and
close cross above emaVerySlow
//and
//close < open [1]
//and
//close[1] >= open[1]
//and
//close < emaFast
//and
//(Close/entryprice-1)*100 > MinProfitforadd 
//and
//(1-close/entryprice)*100 > 0
//and
//barssinceentry > 20
and
CurShares < maxpositions 
then 
begin
buy longbuyingPower2 Shares next bar at market  ;
end;
}

{
if         
marketposition = 0 //Conditions Entry short
and
//(
//(PLTarget < PForDay) and (PLTarget > LForDay) //1
//)  
//and
//(
//(Time > 1400.00) or (Time < 1200.00 and Time > 430.00) or (Time < 1200.00 and Time < 300.00) //2
//)
//and
close < Open //3
//and
//(close-open) >(close[1]-open[1])* 1.3
and
close < low5
//and
//high5 > emaVerySlow
//and
//close < minlist (close [1], open [1]) //low
and
close < emaMid //20
and
close < emaverySlow * (1 - os3 /100) // ema 200 - with offset of 2$ 
//and
//emaMid < emaVerySlow
//and
//emaMid <= emaverySlow * (1-Mingap/100) //till 10 
//and
//emaMid >= emaverySlow * (1-Maxgap/100) //till 10 
//and
//close >= emaverySlow * (1-Maxgap1/100) //till 8
//and
//close > high5 * (1-maxgap4/100)
//and
//close of data2 < ema2mid 
//and
//close >= high *(1-maxgap3/100) 
//and
//Mom <= 0

//and
//high > high [1]

//and
//close <= emaMid * (1-Mingap1/100) //till 8 
//and
//close >= emaMid * (1-Maxgap2/100) //till 8 
//and
//close cross below emaFast
//and
//
//(close cross below emaFast) or (close [1] cross below emaFast[1]) or  (close [2] cross below emaFast[2])
//)
//and
//Histogram < 0

then 
begin
sellshort shortbuyingPower Shares next bar at market  ;
end;
}

{
if marketposition = -1 //Scale In  - Conditions Add Entry Short
and
close < Open
//and
//close [1] >= open [1]

//and
//close < low [1]
//and
//close < emaMid
//and
//low5 > emaVerySlow
and
close cross below EHLOCdownband
//and
//close cross below emaFast
and
close cross below low9
and
close < emaVerySlow


//and
//Histogram < 0
//and
//close cross below emaFast


//and
//close < open [1]
//and
//close[1] >= open[1]
//and
//close < emaFast
//and
//(1-Close/entryprice)*100 > MinProfitforadd 
//and
//(1-close/entryprice)*100 > 0
//and
//barssinceentry > 20
and
CurShares < maxpositions 
then 
begin
sellshort shortbuyingPower1 Shares next bar at market  ;
end;

{
if marketposition = -1 //Scale In x3 - Conditions Add Entry short
//and
//close > emaMid
and
low5 > emaMid
and
close [1] >= open [1]
and
high > high [1]
and
close cross below emaMid
and
close cross below emaVerySlow
//and
//close < open [1]
//and
//close[1] >= open[1]
//and
//close < emaFast
//and
//(Close/entryprice-1)*100 > MinProfitforadd 
//and
//(1-close/entryprice)*100 > 0
//and
//barssinceentry > 20
and
CurShares < maxpositions 
then 
begin
sellshort shortbuyingPower2 Shares next bar at market  ;
end;
}

}

{

if marketposition = -1 //add for short position
and
(1-Close/entryprice)*100 >= SmallMinProfitforadd 
then 
begin
sellshort buyingPower Shares next bar at market  ;
end;
}

{
//sell more after fast minimum profit
if marketposition = -1 //there is long position open
and
(1-Close/entryprice)*100 >= SmallMinProfitforadd 
and
barssinceentry < MaxBarsforadd
and
MarketPosition_at_Broker < maxpositions 
//and
//AngleLong = False
//entryprice >= vBlb2
then 
begin
sellshort buyingPower Shares next bar at market  ;
end;
}

//close long position with trail
if marketposition = 1
then
[IntrabarOrderGeneration = True] //trade intra-bar

//close long position with trail start moving after small profit in the first bar from entry
if marketposition = 1 //there is long position open
and
(close/entryprice-1)*100 >= SmallMinProfit 
and
barssinceentry <= 1
//and
//AngleLong = False
//entryprice >= vBlb2
then 
begin
valuePercentTrail = ((entryprice * SmallTrailStop) /100);
trailProfit = Highest(high , Barssinceentry); 
trailExit = trailProfit - valuePercentTrail;        
sell  next bar at trailExit  stop;
end;




//close short position with trail start moving after the first bar from entry
if marketposition = 0
then
begin
longStop = -9999999;
end;

if marketposition = 1 //there is long position open
and
(close/entryprice-1)*100 >= SmallbaseProfit 
and
barssinceentry > 1
then
begin
// Calculate the trailing stop price
if low [1] > longStop 
then
begin
longStop = low[1];
end;
end;

//close 1st long position with trail start moving cross back
if marketposition = 1 //there is long position open
and
(close/entryprice-1)*100 >= SmallbaseProfit 
and
barssinceentry > 1
and
Close < longStop * (1-os1/100)
Then
begin
Sell longbuyingPower1 Shares Next Bar at Market;
end;


//close 2st long position with trail start moving cross back
if marketposition = 1 //there is long position open
and
(close/entryprice-1)*100 >= SmallbaseProfit 
and
barssinceentry > 1
and
Close < longStop * (1-os1/100)
and
close > lastExitPrice 
Then
begin
Sell longbuyingPower1 Shares Next Bar at Market;
end;


{
//close 2 out long position after cross with stop
if marketposition = 1 //there is long position open
and
CurShares = longbuyingPower1 
and
barssinceentry > 1
Then
begin
Sell longbuyingPower1 Shares Next Bar at (entryprice + Close)/2  stop;
end;
}

{
//close 2 out long position after cross with trail
if marketposition = 1 //there is long position open
and
(close/entryprice-1)*100 >= SmallbaseProfit 
and
CurShares = longbuyingPower1 
and
barssinceentry > 1
and
Close < longStop * (1-os1/100)
and
close > lastExitPrice 
Then
begin
Sell longbuyingPower1 Shares Next Bar at Market;
end;
}

{
//close long position when cross above ema200
if marketposition = 1 //there is long position open
and
close cross below emaVerySlow * (1-os2/100)
Then
begin
Sell Next Bar at Market;
end;
}

{
//close long position when cross below min of 5 open-close
if marketposition = 1 //there is long position open
and
Close < low5 
Then
begin
Sell Next Bar at Market;
end;
}

{
//close long position when there is 3 bars short
if marketposition = 1 //there is long position open
and
(
(close <= open ) and (close [1] <= open [1]) and (close [2] <= open [2])
)
Then
begin
Sell Next Bar at Market;
end;
}

{
//close long position when there is 20 dolar profit
if marketposition = 1 //there is long position open
and
(close/entryprice-1)*100 >= SmallMinProfit1 
Then
begin
Sell Next Bar at Market;
end;
}

{
//close long position when cross below ema 200
if marketposition = 1 //there is long position open
and
close cross below emaVerySlow
Then
begin
Sell Next Bar at Market;
end;
}



{
//close long position if cross 200 EMA
if marketposition = 1
and
close < (emaVerySlow * (1- os1/100))
then 
begin
sell next bar at market;
end;
}

{
//close long position if reach 10 points
if marketposition = 1
and
(close/entryprice-1)*100 >= smallbaseProfit 
then 
begin
sell next bar at market;
end;
}

{
//close long position if reach up boll 21
if marketposition = 1
and
close >= EHLOCupband
then 
begin
sell next bar at market;
end;
}

{
//close long position at the EOD
if marketposition = 1
and Time = 2300.00 
then 
begin
sell next bar at market;
end;
}

//close long position with trail
if marketposition = -1
then
[IntrabarOrderGeneration = True] //trade intra-bar


//take profit for a short position with trail start moving in the first bar from entry
if marketposition = -1 //there is short position open
and
(1-Close/entryprice)*100 >= SmallMinProfit 
and
barssinceentry <= 1
//and
//AngleShort = False
//and
//entryprice <= vBub2
then 
begin
valuePercentTrail = ((entryprice * SmallTrailStop) /100);
trailProfit = Lowest(low , Barssinceentry); 
trailExit = trailProfit + valuePercentTrail; //          
buytocover next bar at trailExit  stop;
end;


//close short position with trail start moving after the first bar from entry
if marketposition = 0
then
begin
shortStop = 9999999;
end;

if marketposition = -1 //there is long position open
and
(1-Close/entryprice)*100 >= SmallbaseProfit 
and
barssinceentry > 1
then
begin
// Calculate the trailing stop price
if High[1] < shortStop 
then
begin
shortStop = High[1];
end;
end;

//close short position with trail start moving aafter the first bar from entry
if marketposition = -1 //there is long position open
and
(1-Close/entryprice)*100 >= SmallbaseProfit 
and
barssinceentry > 1
and
Close > shortStop * (1+os1/100)
Then
begin
buytocover Next Bar at Market;
end;

{
//close short position when cross above ema200
if marketposition = -1 //there is long position open
and
Close cross above emaVerySlow * (1+os2/100)
Then
begin
buytocover Next Bar at Market;
end;
}

{
//close short position when cross above min of 5 open-close
if marketposition = -1 //there is long position open
and
Close > high5 
Then
begin
buytocover Next Bar at Market;
end;
}

{
//close short position when there is 20 dolar profit
if marketposition = -1 //there is long position open
and
(1-Close/entryprice)*100 >= SmallMinProfit1 
Then
begin
buytocover Next Bar at Market;
end;
}

{
//close short position when cross above ema 200
if marketposition = -1 //there is long position open
and
close cross above emaVerySlow
Then
begin
buytocover Next Bar at Market;
end;
}

{
//close short position when there is 3 bars long
if marketposition = -1 //there is long position open
and
(
(close >= open ) and (close [1] >= open [1]) and (close [2] >= open [2])
)
Then
begin
buytocover Next Bar at Market;
end;
}
{
//close short position if reach down boll 21
if marketposition = -1
and
close <= EHLOCdownband
then 
begin
buytocover next bar at market;
end;
}

{
//close short position if cross 200 EMA
if marketposition = -1
and
close > (emaVerySlow * (1+ os1/100))
then 
begin
buytocover next bar at market;
end;
}

{
//close short position if reach 10 points
if marketposition = -1
and
(1-entryprice/Close)*100 >= smallbaseProfit 
then 
begin
buytocover next bar at market;
end;
}

{
//close short position at the EOD
if marketposition = -1
and Time = 2300.00 
then
begin
buytocover next bar at market;
end;
}

//SetProfitTarget;
if marketposition = 1
then
begin
SetStopLoss(longSL);
end;


if marketposition = -1
then
begin
SetStopLoss(shortSL);
end;

{
if marketposition = 0 then 
begin
//Long Prints - No position - dbug tag
buydbg= ""; 
if (
(PLTarget < PForDay) and (PLTarget > LForDay) 
)  
 then
 buydbg = buydbg + "1" else buydbg = buydbg + "X" ;
if 
(
(Time > 1400.00) or (Time < 1200.00 and Time > 430.00) or (Time < 1200.00 and Time < 300.00) 
)
 then
 buydbg = buydbg + "2" else buydbg = buydbg + "X" ;
if close > Open  then
 buydbg = buydbg + "3" else buydbg = buydbg + "X" ;
if close > high5 then
 buydbg = buydbg + "4" else buydbg = buydbg + "X" ;
 if low5 < emaVerySlow then
 buydbg = buydbg + "5" else buydbg = buydbg + "X" ; 
if close > emaMid then
 buydbg = buydbg + "6" else buydbg = buydbg + "X" ;
if close > emaverySlow   
then buydbg = buydbg + "7" else buydbg = buydbg + "X" ;
if emaMid <= emaverySlow * (1+Maxgap/100)   
then buydbg = buydbg + "8" else buydbg = buydbg + "X" ;
if close <= emaverySlow * (1+Maxgap1/100) 
then buydbg = buydbg + "9" else buydbg = buydbg + "X" ;
if close cross above emaFast
then buydbg = buydbg + "A" else buydbg = buydbg + "X" ;
}

{
//Short Prints - No position - dbug tag

selldbg = "";
if (
(PLTarget < PForDay) and (PLTarget > LForDay)
)  then
selldbg = selldbg + "1" else selldbg = selldbg + "X" ;
if (
(Time > 1400.00) or (Time < 1200.00 and Time > 430.00) or (Time < 1200.00 and Time < 300.00) //2
) then
selldbg = selldbg + "2" else selldbg = selldbg + "X" ;
if close < Open  then
selldbg = selldbg + "3" else selldbg = selldbg + "X" ;
if close < low5    then
selldbg = selldbg + "4" else selldbg = selldbg  + "X" ;
if high5 > emaVerySlow   then
selldbg = selldbg + "5" else selldbg = selldbg  + "X" ;
if close < emaMid
 then
selldbg = selldbg + "6" else selldbg = selldbg  + "X" ;
if close < emaverySlow   then
selldbg = selldbg + "7" else selldbg = selldbg  + "X" ;
if emaMid >= emaverySlow * (1-Maxgap/100)    then
selldbg = selldbg + "8" else selldbg = selldbg  + "X" ;
if close >= emaverySlow * (1-Maxgap1/100) then
selldbg = selldbg + "9" else selldbg = selldbg  + "X" ;
if close cross below emaFast
 then selldbg = selldbg + "A" else selldbg = selldbg  + "X" ;
}


if marketposition = 0  
and
ELDateToString(date) = "07/13/2023" //and symbol = "soxs" //and Time = 1300
//and (close cross over emaFast  or close cross below emaFast )
then
//Long Prints - but No position
print ( "MOMTEST  > symbol=" , symbol," ", "islong=", is_long_symbol,  "no position","  ",
 ELDateToString(date),"Time=", time,"buydbg=", buydbg, "  ", "selldbg=", selldbg,
 "     ","bar=", BarNumber,
"entryprice=","xxxx.xx", 
"close=", close, 
"longStop =", longStop ,
"lastExitPrice =", lastExitPrice ,
"shortStop =", shortStop  ,

"high5=", high5, "low5=", low5,
"S1=", S1, "S2=", S2, "S3=", S3, "R1=", R1,  "R2=", R2,  "R3=", R3, 
"EHLOCdownband =", EHLOCdownband ,
"EHLOCupband =", EHLOCupband ,
"PLTarget=", PLTarget,
"emaFast=" , emaFast, 
"LowD(0)=", LowD(0), "HighD(0)=", HighD(0), 
"dema=", demafast,
"vwap=", //vwap,
"vKeltUp  =", vKeltUp, "vKeltdown  =", vKeltDown, 
"vBlb1 =", vBlb1, "vBlb2 =", vBlb2,"vBlb3 =", vBlb3,
"vBub1 =", vBub1, "vBub2 =", vBub2,"vBub3 =", vBub3,
"AvgVolumeLength= ", AvgVolumeLength, "volumeUP =", volumeUP ,
"emaslow=", emaSlow, "emaverySlow =", emaverySlow , "ema3verySlow=" , ema3VerySlow , 
 "ema2=",ema2Slow , "emaVerySlow=", ema3VerySlow, 
"Close[1]=", Close[1], "Close[2]=", Close[2],
"open=", Open, "open[1]=", Open[1], "open[2]=", Open[2],
"low=", low, "low[1]=", Low[1], "low[2]=", Low[2],
"high=", high, "high[1]=", high[1], "high[2]=", High[2],
"openD0=", OpenD(0), "closeD1=", CloseD(1),
"adxcalc =", adxcalc ,"adxmin=", adxmin , "MinProfit =",SmallMinProfit
 ,"MinEMAGap=" , MinEMAGap,"MaxEMAGap=" , MaxEMAGap,
 "smaFast=", smaFast, "smaMid=", smaMid, "smaSlow =", smaSlow ,
  "MinGapSlowToMid=", MinGapSlowToMid,  
"TakeProfitPct =", TakeProfitPct , "StopPct=", StopPct);


//long position prints
if marketposition = 1 
and ELDateToString(date) = "07/13/2023" //and symbol = "soxs" //and Time = 1300
then 
print ( "MOMTEST   > symbol=" , symbol," ",  "in long", "      "
,ELDateToString(date),"Time=", time,"buydbg=", buydbg, "     ","bar=", BarNumber,
"entryprice=",entryprice, 
"close=", close, 
"longStop =", longStop ,
"lastExitPrice =", lastExitPrice ,
"shortStop =", shortStop  ,
"high5=", high5, "low5=", low5,
"S1=", S1, "S2=", S2, "S3=", S3, "R1=", R1,  "R2=", R2,  "R3=", R3, 
"EHLOCdownband =", EHLOCdownband ,
"EHLOCupband =", EHLOCupband ,
"PLTarget=", PLTarget,
"emaFast=" , emaFast, 
"LowD(0)=", LowD(0), "HighD(0)=", HighD(0), 
"dema=", demafast,
"vwap=", //vwap,
"vKeltUp  =", vKeltUp, "vKeltdown  =", vKeltDown, 
"vBlb1 =", vBlb1, "vBlb2 =", vBlb2,"vBlb3 =", vBlb3,
"vBub1 =", vBub1, "vBub2 =", vBub2,"vBub3 =", vBub3,
"AvgVolumeLength= ", AvgVolumeLength, "volumeUP =", volumeUP ,
"emaslow=", emaSlow, "emaverySlow =", emaverySlow , "ema3verySlow=" , ema3VerySlow , 
 "ema2=",ema2Slow , "emaVerySlow=", ema3VerySlow, 
"Close[1]=", Close[1], "Close[2]=", Close[2],
"open=", Open, "open[1]=", Open[1], "open[2]=", Open[2],
"low=", low, "low[1]=", Low[1], "low[2]=", Low[2],
"high=", high, "high[1]=", high[1], "high[2]=", High[2],
"openD0=", OpenD(0), "closeD1=", CloseD(1),
"adxcalc =", adxcalc ,"adxmin=", adxmin , "MinProfit =",SmallMinProfit
 ,"MinEMAGap=" , MinEMAGap,"MaxEMAGap=" , MaxEMAGap,
 "smaFast=", smaFast, "smaMid=", smaMid, "smaSlow =", smaSlow ,
  "MinGapSlowToMid=", MinGapSlowToMid,  
"TakeProfitPct =", TakeProfitPct , "StopPct=", StopPct);


{
//short position prints       
if marketposition = -1 
//and ELDateToString(date) = "06/14/2023" //and symbol = "soxs"//and Time = 1300
then 
print ("MOMTEST  > symbol=" , symbol," ", "in short","     ", ELDateToString(date),"Time=", time,"selldbg=", selldbg , "     ","bar=", BarNumber,
"entryprice=",entryprice, 
"close=", close, 
"shortStop =", shortStop  ,
"longStop =", longStop ,
"high5=", high5, "low5=", low5,
"S1=", S1, "S2=", S2, "S3=", S3, "R1=", R1,  "R2=", R2,  "R3=", R3, 
"EHLOCdownband =", EHLOCdownband ,
"EHLOCupband =", EHLOCupband ,
"PLTarget=", PLTarget,
"emaFast=" , emaFast, 
"LowD(0)=", LowD(0), "HighD(0)=", HighD(0), 
"dema=", demafast,
"vwap=", //vwap,
"vKeltUp  =", vKeltUp, "vKeltdown  =", vKeltDown, 
"vBlb1 =", vBlb1, "vBlb2 =", vBlb2,"vBlb3 =", vBlb3,
"vBub1 =", vBub1, "vBub2 =", vBub2,"vBub3 =", vBub3,
"AvgVolumeLength= ", AvgVolumeLength, "volumeUP =", volumeUP ,
"emaslow=", emaSlow, "emaverySlow =", emaverySlow , "ema3verySlow=" , ema3VerySlow , 
 "ema2=",ema2Slow , "emaVerySlow=", ema3VerySlow, 
"Close[1]=", Close[1], "Close[2]=", Close[2],
"open=", Open, "open[1]=", Open[1], "open[2]=", Open[2],
"low=", low, "low[1]=", Low[1], "low[2]=", Low[2],
"high=", high, "high[1]=", high[1], "high[2]=", High[2],
"openD0=", OpenD(0), "closeD1=", CloseD(1),
"adxcalc =", adxcalc ,"adxmin=", adxmin , "MinProfit =",SmallMinProfit
 ,"MinEMAGap=" , MinEMAGap,"MaxEMAGap=" , MaxEMAGap,
 "smaFast=", smaFast, "smaMid=", smaMid, "smaSlow =", smaSlow ,
  "MinGapSlowToMid=", MinGapSlowToMid,  
"TakeProfitPct =", TakeProfitPct , "StopPct=", StopPct);
}

