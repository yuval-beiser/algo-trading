//@version=31323-2
Inputs:
maximumloss(0.14), //120 //160 //1300 //0.143
FastLength(9),
MidLength(20),
MidLength1(26),
SlowLength(50),
AssetMultiplier (20),
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
Mingap (0.2), //0.06 was too tight according to 8.3.23 , 3:03 AM //0.15
Mingap1 (0.01),
Maxgap (0.12), //0.O5
Maxgap1 (0.2), //0.2 //0.02 //0.2
Maxgap2 (0.05), //0.2
maxgap3 (0.09),
maxgap4 (0.26),
maxgap5 (0.13),


MinProfit (0.00625),
smallbaseProfit (0.033), //0.035 //0.19 //0.02 //0.1 //0.5 //CROSS1:0.033 (5P)
smallbaseProfit1 (0.059), //0.035 //0.19 //0.02 //0.1 //0.5 //CROSS2:0.059 (9P)
SmallMinProfit (0.0334),//after 12 pips start trail of 4 pips //0.075 with stochastic //0.1 //TRAIL PCT FROM 5P //0.033
SmallMinProfit1 (0.0629),
largeMinProfit (0.44), //after 10 pips start trail of 8 pips //0.09375
SmallMinProfitPart1 (0.05), //after 3 pips limit 3 at the middle of the chanel //0.05
Smallbaseloss (0.03),
SmallMinProfitPart2 (0.0375), //after 6 pips limit at the other side of the channel
MinProfitforadd (0.01),
MaxProfitForAdd (0.1),
FastMinProfit (0.0625), //0.1125
MinBaseProfit (0.03),
MinLossForAdd (0.1), //0.1
SmallTrail (0.0033),//0.04375 with stochastic //0.00625 //0.0125 //0.025 //0.01875 //TRAIL SPREAD: 0.5P //0.0033
largeTrail (0.09),
MinSQQQTQQQGap (0.09),
Minbarsfortake (5), //2
MinBarsAfterCloseToEntry (1),
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
Atrmax (15),
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

PForDay (6000), //1500 //1950 //100 //800 //15000
LForDay (-800), //-1100 //-500 //-50 //-2000

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
IntrabarPersist ExitBarNum (0),
intrabarpersist LastMarketPosition(0),
intrabarpersist tmpTrailExit (0),
intrabarpersist rtPosition(0), // F1 Update on every tick


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
PrevMACD (0),
MACDGradient (0),


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

IntrabarPersist crossind1 (false),
IntrabarPersist crossind2 (false),
IntrabarPersist crossind3 (false),


//stop
startlongSL(maximumloss),
updatedlongSL(maximumloss),
startshortSL (maximumloss),
updatedshortSL(maximumloss),
longSL (0),
shortSL (0),

IntrabarPersist alertsGenerated(0),
IntrabarPersist lastPrintBar(0),
IntrabarPersist lastAlertBar1(0);


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
emaMid30 = XAverage(close,MidLength1);
emaSlow = XAverage(close,SlowLength);
emafast1 = XAVERAGE(XAVERAGE(close,FastLength),FastLength);
demafast = emaFast * 2 - emafast1  ;    
emaverySlow = XAverage(close,VerySlowLength);
//ema2Fast = XAverage(close,FastLength) of data2;
//ema2Slow = 0;//XAverage(close ,slowLength) of data2;
//ema2verySlow = XAverage(close,VerySlowLength)of data2;
//ema2mid = XAverage(close,MidLength) of data2;
adxcalc = ADX(adxperiod);
longbuyingPower = 4 ;//(AccountBalance/Close)*PctPerTrade/100; // the amount of shares i can buy //1 //3
longbuyingPower1 = 2; // scale in-out
longbuyingPower2 = 2;
shortbuyingPower = 4; //3
shortbuyingPower1 = 2 ; // scale in-out
shortbuyingPower2 = 2 ;


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

PrevMACD = MACD(Close, 12, 26)[1];
MACDGradient = MACDLine - PrevMACD;

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

high9 = maxlist (close [1] , open [1], close [2] , open [2], close [3] , open [3], close [4] ,
open [4], close [5] , open [5], close [6] , open [6], close [7] , open [7], close [8] , open [8], close [9] , open [9]  );

low9 = minlist (close [1] , open [1], close [2] , open [2], close [3] , open [3], close [4] ,
open [4], close [5] , open [5], close [6] , open [6], close [7] , open [7], close [8] , open [8], close [9] , open [9]  );

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

//reset alertsGenerated when not in possition
if marketposition = 0 and rtPosition= 0
then
alertsGenerated = 0;



//Reset MP
if marketposition = 0 and LastMarketPosition <> 0
then begin
ExitBarNum = BarNumber;
rtPosition = marketposition;
end;
LastMarketPosition = marketposition;


if marketposition = 0 //Conditions Entry Long
//and
//(
//(PLTarget < PForDay) and (PLTarget > LForDay) //1
//)  
and
//(
(Time > 600.00) and (Time < 2200.00) //long time
//)
and
close > Open //3
//and
//(close-open) >(close[1]-open[1])* 1.3
and
close > high9
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
//and
//(
//(close cross above emaFast) or (close cross above emaMid) or (close cross above emaVerySlow) //20
//)
and
close > emaverySlow * (1 + os3 /100)  //200

//and
//emaMid cross above emaVerySlow

//and
//emaMid >= emaverySlow * (1+Mingap/100) //from 10
and
emaMid <= emaverySlow * (1+Maxgap/100) //*
and
close <= emaverySlow * (1+Maxgap1/100) //*
//and
//emaMid > emaVerySlow
and
atr < Atrmax
and
close > lowD (0) * (1+Mingap/100)
and
DonchianDown > DonchianUp * (1-maxgap5/100)

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
and
Histogram > 0
//and
//MACDGradient > 0
//and
//BarNumber > ExitBarNum + MinBarsAfterCloseToEntry

then
begin
buy longbuyingPower Shares next bar at market  ;
Alert(text(" model=FISORA instrument=","NQ shares=",longbuyingPower ," type=BOUGHT LONG-", FormatDate("dd-MM-yyyy", DateToJulian(Date)),"ENTRY LONG"));
rtPosition=1;
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



if        
marketposition = 0 //Conditions Entry short
and
(
(PLTarget < PForDay) and (PLTarget > LForDay) //1
)  
and
//(
(Time > 600.00) and (Time < 2200.00) //long time
//)
and
close < Open //3
//and
//(close-open) >(close[1]-open[1])* 1.3
and
close < low9
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
//and
//(
//(close cross above emaFast) or (close cross above emaMid) or (close cross above emaVerySlow) //20
//)
and
close < emaverySlow * (1 - os3 /100)  //200

//and
//emaMid cross above emaVerySlow

//and
//emaMid >= emaverySlow * (1+Mingap/100) //from 10
and
emaMid >= emaverySlow * (1-Maxgap/100) //*
and
close >= emaverySlow * (1-Maxgap1/100) //*
//and
//emaMid > emaVerySlow
and
atr < Atrmax
//and
//close < HIGHD (0) * (1-Mingap/100)
and
DonchianDown > DonchianUp * (1-maxgap5/100)

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
and
Histogram < 0
//and
//BarNumber > ExitBarNum + MinBarsAfterCloseToEntry


then
begin
sellshort shortbuyingPower Shares next bar at market  ;
Alert(text(" model=FISORA instrument=","NQ shares=",shortbuyingPower," type=SOLD SHORT-", FormatDate("dd-MM-yyyy", DateToJulian(Date)),"ENTRY SHORT"));
rtPosition = -1;

end;



//close long position with trail
if marketposition = 1
then
[IntrabarOrderGeneration = True] //trade intra-bar


{
//close long position with trail start moving after small profit in the first bar from entry
if marketposition = 1 //there is long position open
and
(close/entryprice-1)*100 >= SmallMinProfit
and
barssinceentry <= 1
and
Time <> 1632.00
//and
//AngleLong = False
//entryprice >= vBlb2
then begin
valuePercentTrail = ((entryprice * SmallTrailStop) /100);
trailProfit = Highest(high , Barssinceentry);
tmpTrailExit = trailProfit - valuePercentTrail;     
if tmpTrailExit <> trailExit then begin
trailExit = tmpTrailExit;  
//sell  next bar at trailExit  stop;

//Alert("Momentum - SELL AT FAST TRAIL");
end;
end;

if marketposition = 1 and close cross below trailExit and rtPosition =1 
then begin 
sell  next bar at market;
Alert(text(" model=FISORA instrument=","NQ shares=",longbuyingPower ," type=SOLD LONG-", FormatDate("dd-MM-yyyy", DateToJulian(Date)), "EXIT ON TRAIL 3.1",rtPosition, marketposition, trailExit  ));
rtPosition = 0;
alertsGenerated = 0;
end;
}


//close short position with trail (based on low prev) start moving after the first bar from entry
if marketposition = 0
then
begin
longStop = -9999999;
end;

if marketposition = 0
then
begin
shortStop = 9999999;
end;


//reset crossind
if marketposition = 0
then
begin
crossind1 = False;
end;

{
//reset crossind
if marketposition = 0
then
begin
crossind2 = False;
end;

//reset crossind
if marketposition = 0
then
begin
crossind3 = False;
end;
}

{
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
crossind1 = true;
Alert("Momentum - PARTIAL EXIT LONG AT CROSS 1");
end;
}

//close short position with take profit after small profit
if marketposition = 1 //there is long position open
and
(close/entryprice-1)*100 >= SmallMinProfit
//and
//barssinceentry <= 5
//and
//AngleLong = False
//entryprice >= vBlb2
then begin  
sell longbuyingPower1 Shares next bar at market;
crossind1 = true;

{
// Generate an intra-bar alert
if (alertsGenerated < MaxAlertsPerBar)
then
(alertsGenerated = alertsGenerated + 1);
Alert(text("-APEX REVERSAL-","NQ-",longbuyingPower ,"-SOLD-", FormatDate("dd-MM-yyyy", DateToJulian(Date)), "EXIT ON TAKE PROFIT"));
}
if alertsGenerated = 0 
then begin
Alert(text(" model=FISORA instrument=","NQ shares=",longbuyingPower1 ," type=SOLD LONG-", FormatDate("dd-MM-yyyy", DateToJulian(Date)), "EXIT ON TAKE PROFIT"));
alertsGenerated  =1;
end;
end;


{
// Generate an intra-bar alert
if (alertsGenerated < MaxAlertsPerBar)
then
(alertsGenerated = alertsGenerated + 1);
Alert(text("-APEX REVERSAL-","NQ-",longbuyingPower ,"-SOLD-", FormatDate("dd-MM-yyyy", DateToJulian(Date)), "EXIT ON TAKE PROFIT"));
end;
}


//close long position with trail start moving cross back
if marketposition = 1 //there is long position open
and
(close/entryprice-1)*100 >= SmallbaseProfit1
and
barssinceentry > 1
//and
//Close < longStop * (1-os1/100)
and
close cross below emaMid30
and
crossind1 = true
//and
//close > lastExitPrice

Then begin
Sell longbuyingPower1 Shares Next Bar at Market;
Alert(text(" model=FISORA instrument=","NQ shares=",longbuyingPower1 ," type=SOLD LONG-", FormatDate("dd-MM-yyyy", DateToJulian(Date)), "EXIT ON CROSS 2"));
alertsGenerated  =0;
rtPosition = 0;
end;



//close long position with trail start moving after large profit in the first bar from entry
if marketposition = 1 //there is long position open
and
(close/entryprice-1)*100 >= largeMinProfit
//and
//barssinceentry <= 1
//and
//crossind1 = true
//and
//AngleLong = False
//entryprice >= vBlb2
then begin
valuePercentTrail = ((entryprice * largeTrail) /100);
trailProfit = Highest(high , Barssinceentry);
tmpTrailExit = trailProfit - valuePercentTrail;     
if tmpTrailExit <> trailExit then begin
trailExit = tmpTrailExit;	       
//sell  next bar at trailExit  stop;
//Alert("Momentum - SELL AT LARGE TRAIL");
end;
end;

if marketposition = 1 and close cross below trailExit and rtPosition =1 
then begin 
sell  next bar at market;
Alert(text(" model=FISORA instrument=","NQ shares=",longbuyingPower ," type=SOLD LONG-", FormatDate("dd-MM-yyyy", DateToJulian(Date)), "EXIT ON TRAIL 3.2",rtPosition, marketposition, trailExit  ));
rtPosition = 0;
alertsGenerated = 0;
end;


//close long position after cross 1 and go break even
if marketposition = 1 //there is long position open
and
close < (entryprice * 1.000067)
and
barssinceentry > 3
//and
//Close < longStop * (1-os1/100)
and
crossind1 = true

//and
//close > lastExitPrice
Then begin
Sell Next Bar at Market;
if alertsGenerated >0 
then begin
if crossind1 = true and crossind2 = false then longbuyingPower2 =2;
Alert(text(" model=FISORA instrument=","NQ shares=",longbuyingPower2 ," type=SOLD LONG-", FormatDate("dd-MM-yyyy", DateToJulian(Date)), "EXIT ON BREAK EVEN"));
alertsGenerated = 0;
rtPosition = 0;
end;
end;



// START--  EXIT SHORT BASE OF PRECENT -------------------------------------------------------

if marketposition = -1
then
[IntrabarOrderGeneration = True] //trade intra-bar

{
//close short position with trail start moving after small profit in the first bar from entry
if marketposition = -1 //there is long position open
and
(1-close/entryprice)*100 >= SmallMinProfit
and
barssinceentry <= 1
and
Time <> 1632.00

//and
//AngleLong = False
//entryprice >= vBlb2
then
begin
valuePercentTrail = ((entryprice * SmallTrailStop) /100);
trailProfit = lowest(low , Barssinceentry);
tmpTrailExit = trailProfit - valuePercentTrail;     
if tmpTrailExit <> trailExit then begin
trailExit = tmpTrailExit;
//Alert("Momentum - BUY TO COVER AT FAST TRAIL");
end;
end;

if marketposition = -1 and close cross above trailExit and rtPosition =-1 
then begin 
buytocover  next bar at market;
Alert(text(" model=FISORA instrument=","NQ shares=",shortbuyingPower ," type=BOUGHT SHORT-", FormatDate("dd-MM-yyyy", DateToJulian(Date)), "EXIT ON TRAIL 4.1", rtPosition, marketposition, trailExit  ));
rtPosition= 0;
alertsGenerated = 0;
end;
}


// END--  EXIT SHORT BASE OF PRECENT -------------------------------------------------------


// START - EXIT SHORT BASE ON CROSS PREVEVIOS High -------------------------------------------------------
//close short position with trail (based on low prev) start moving after the first bar from entry
if marketposition = 0
then
begin
shortStop = 9999999;
end;

//reset crossind
if marketposition = 0
then
begin
crossind1 = False;
end;


{
if marketposition = -1 //there is short position open
and
(1-close/entryprice)*100 >= SmallbaseProfit
and
barssinceentry > 1
then
begin
// Calculate the trailing stop price
if high [1] < shortStop
then
begin
shortStop = high[1];
end;
end;


//close 1st short position with trail start moving cross back
if marketposition = -1 //there is long position open
and
(1-close/entryprice)*100 >= SmallbaseProfit
and
barssinceentry > 1
and
Close > shortStop * (1+os1/100)
Then
begin
buytocover shortbuyingPower1 Shares Next Bar at Market;
crossind1 = true;
Alert("Momentum - PARTIAL EXIT SHORT AT CROSS 1");
end;
}

//close short position with take profit after small profit
if marketposition = -1 //there is long position open
and
(1-close/entryprice)*100 >= SmallMinProfit
//and
//barssinceentry <= 5
//and
//AngleLong = False
//entryprice >= vBlb2
then
begin  
buytocover shortbuyingPower1 Shares next bar at market;
crossind1 = true;
{
// Generate an intra-bar alert
if (alertsGenerated < MaxAlertsPerBar)
then
(alertsGenerated = alertsGenerated + 1);
Alert(text("-APEX REVERSAL-","NQ-",longbuyingPower ,"-SOLD-", FormatDate("dd-MM-yyyy", DateToJulian(Date)), "EXIT ON TAKE PROFIT"));
}


if alertsGenerated = 0 
then begin
Alert(text(" model=FISORA instrument=","NQ shares=",shortbuyingPower1 ," type=BOUGHT SHORT-", FormatDate("dd-MM-yyyy", DateToJulian(Date)), "EXIT ON CROSS 1"));
alertsGenerated  =1;
end;
end;

{
// Generate an intra-bar alert
if (alertsGenerated < MaxAlertsPerBar)
then
(alertsGenerated = alertsGenerated + 1);
Alert(text("-APEX REVERSAL-","NQ-",longbuyingPower ,"-BUY TO COVER-", FormatDate("dd-MM-yyyy", DateToJulian(Date)), "EXIT ON TAKE PROFIT"));
end;
}

// END - EXIT SHORT BASE ON CROSS PREVEVIOS High -------------------------------------------------------

//close long position with trail start moving cross back
if marketposition = -1 //there is long position open
and
(1-close/entryprice)*100 >= SmallbaseProfit1
and
barssinceentry > 1
//and
//Close < longStop * (1-os1/100)
and
close cross above emaMid30
and
crossind1 = true
//and
//close > lastExitPrice

Then begin
buytocover shortbuyingPower1 Shares Next Bar at Market;
//Alert("Momentum - PARTIAL EXIT SHORT AT CROSS 2");

if alertsGenerated >0 
then begin
Alert(text(" model=FISORA instrument=","NQ shares=",shortbuyingPower1 ," type=BOUGHT SHORT-", FormatDate("dd-MM-yyyy", DateToJulian(Date)), "EXIT ON CROSS 2"));
alertsGenerated  =0;
rtPosition = 0;

end;
end;


{
//close long position after cross ema 200-1
if marketposition = -1 //there is long position open
and
(1-close/entryprice)*100 >= SmallbaseProfit
and
barssinceentry > 1
//and
//Close < longStop * (1-os1/100)
and
close cross above vBlb1
and
crossind1 = true
and
crossind2 = true

//and
//close > lastExitPrice
Then
begin
buytocover Next Bar at Market;
crossind3 = true;
Alert("Momentum - PARTIAL EXIT SHORT AT CROSS 3");
end;
}
//close short position with trail start moving after large profit in the first bar from entry
if marketposition = -1 //there is long position open
and
(1-close/entryprice)*100 >= largeMinProfit
//and
//barssinceentry <= 2
//and
//AngleLong = False
//entryprice >= vBlb2
then
begin
valuePercentTrail = ((entryprice * largeTrail) /100);
trailProfit = lowest(low , Barssinceentry);
tmpTrailExit = trailProfit - valuePercentTrail;     
if tmpTrailExit <> trailExit then begin
trailExit = tmpTrailExit;	       
end;
end;


if marketposition = -1 and close cross above trailExit and rtPosition =-1 
then begin 
buytocover  next bar at market;
Alert(text(" model=FISORA instrument=","NQ shares=",shortbuyingPower ," type=BOUGHT SHORT-", FormatDate("dd-MM-yyyy", DateToJulian(Date)), "EXIT ON TRAIL 4.2", rtPosition, marketposition, trailExit  ));
rtPosition= 0;
alertsGenerated  =0;
end;


//close long position after cross 1 and go break even
if marketposition = -1//there is long position open
and
close > entryprice * 0.999933
and
barssinceentry > 3
//and
//Close < longStop * (1-os1/100)
and
crossind1 = true
//and
//close > lastExitPrice
Then
begin
buytocover Next Bar at Market;
if alertsGenerated  > 0
then begin
if crossind1 = true and crossind2 = false then shortbuyingPower2 =2;
Alert(text(" model=FISORA instrument=","NQ shares=",shortbuyingPower2 ," type=BOUGHT SHORT-", FormatDate("dd-MM-yyyy", DateToJulian(Date)), "EXIT ON BREAK EVEN"));
alertsGenerated  =0;
rtPosition = 0;
end;
end;



//SetProfitTarget;
if marketposition = 1 and (1-close/entryprice)*100 >= maximumloss and rtPosition = 1
then begin
//SetStopLoss(close*AssetMultiplier *maximumloss/100*longbuyingPower );
sell next bar at market;
Alert(text(" model=FISORA instrument=","NQ shares=",longbuyingPower ," type=SOLD LONG-", FormatDate("dd-MM-yyyy", DateToJulian(Date)), "EXIT ALL 1", rtPosition , marketposition ));
rtPosition = 0;
end;

if marketposition = -1 and (close/entryprice-1)*100 >= maximumloss and rtPosition = -1
then begin 
//SetStopLoss(close*AssetMultiplier *maximumloss/100*shortbuyingPower );
buytocover  next bar at market;
Alert(text(" model=FISORA instrument=","NQ shares=",shortbuyingPower ," type=BOUGHT SHORT-", FormatDate("dd-MM-yyyy", DateToJulian(Date)), "EXIT ALL 2", rtPosition , marketposition  ));
alertsGenerated  =0;
rtPosition = 0;
end;



// CLOSE POSITION AT THE END OF THE DAY
if marketposition = 1
and Time = 2250.00 
then begin
sell next bar at market;
if crossind1 = false then  longbuyingPower2 = 4
else if crossind1 = true then longbuyingPower2 =2;
Alert(text(" model=FISORA instrument=","NQ shares=",longbuyingPower2 ," type=SOLD LONG-", FormatDate("dd-MM-yyyy", DateToJulian(Date)), "EXIT ALL LONG EOD", rtPosition , marketposition ));
alertsGenerated  =0;
rtPosition = 0;
end;

if marketposition = -1
and Time = 2250.00 
then begin
buytocover next bar at market;
if crossind1 = false then  shortbuyingPower2 = 4
else if crossind1 = true  then shortbuyingPower2 =2;
Alert(text(" model=FISORA instrument=","NQ shares=",shortbuyingPower2 ," type=BOUGHT SHORT-", FormatDate("dd-MM-yyyy", DateToJulian(Date)), "EXIT ALL SHORT EOD", rtPosition , marketposition  ));
alertsGenerated  =0;
rtPosition = 0;
end;
