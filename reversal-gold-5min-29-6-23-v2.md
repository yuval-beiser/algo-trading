//@version=31323-2

Inputs:

maximumloss(0.06),//160 //1300 //0.143 //0.12 //0.0695 //0.05

FastLength(9),

MidLength(21), //20

MidLength1(30),

SlowLength(50),

MFILength (14),

AssetMultiplier (20),

length (5),

VerySlowLength (200),

stdDevMultiplier2 (2),

RsiSlowLength(10),

RsiFastLength(8),

TLength (21),

SLength (21),

MinGapSlowToMid(0.1),

RsiMinForLong(30), 

RsiMaxForShort(70), //80

MomentumLength(14),

Longminmom (-0.3),

Shortmaxmom (0.3),

ExitBarNum1(12),

ExitBarNum2(24),

ExitBarNum3(36),

MinBarsAfterCloseToEntry (3), //1 //3 //20

//ExitBarNum (5),

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

mingap2 (0.4),

mingap3 (0.1469), //0.16 //0.3

mingap4 (0.08),
mingap5 (0.02),

mingap6 (0.02),

mingap7 (0.01),

mingap8 (0.02),

Maxgap (0.2), //0.O5  //0.12

Maxgap1 (0.2), //0.2 //0.02 //0.2 // 0.05  //0.05

Maxgap2 (0.15), //0.2 // 0.15

maxgap3 (0.09),

maxgap4 (0.26),

maxgap5 (0.2), //0.13 // 0.2

maxgap6 (0.01),

maxgap7 (0.1541), //8 points //0.06






MinProfit (0.00625),

smallbaseProfit (0.0267), //0.035 //0.19 //0.02 //0.1 //0.5 //CROSS1:0.033 (5P) //0.033

smallbaseProfit1 (0.02), //0.035 //0.19 //0.02 //0.1 //0.5 //CROSS2:0.059 (9P)

SmallMinProfit (0.02), //after 12 pips start trail of 4 pips //0.075 with stochastic //0.1 //0.08

//TRAIL PCT FROM 5P //0.033 //0.133  //0.033 //0.066 //0.0533 //0.0333 //0.0533

SmallMinProfit1 (0.0333),

largeMinProfit (0.44), //after 10 pips start trail of 8 pips //0.09375

SmallMinProfitPart1 (0.033), //after 3 pips limit 3 at the middle of the chanel //0.05

Smallbaseloss (0.03),

SmallMinProfitPart2 (0.0375), //after 6 pips limit at the other side of the channel

MinProfitforadd (0.01),

MaxProfitForAdd (0.1),

FastMinProfit (0.0625), //0.1125

MinBaseProfit (0.03),

MinLossForAdd (0.1), //0.1

SmallTrail (0.01), //0.04375 with stochastic //0.00625 //0.0125 //0.025 //0.01875 //TRAIL SPREAD: 0.5P //0.0033 //0.02

largeTrail (0.09),

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

AtrMin(2), //0.6

Atrmax (21), //15 //23 //8




ANGLE_MA1(130),

ANGLE_MA2(180),

//ANGLE_MA3(85),







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

os4 (0.0167),

minatrpart (45),

maxatrpart (55),




PForDay (300), //1500 //1950 //100 //800 //15000 //600

LForDay (-300), //-1100 //-500 //-50 //-2000 //-400




//Donchian

DonchianLength (20), // 20




//macd

macdFastLength( 12 ),

macdSlowLength( 26 ),

MACDlineLength( 9 ) ,




//BB

BStedDev1(1),

BStedDev2(2), //1.5

BStedDev3(3),

BUpperBand(200), //26

BLowerBand(200), //26

MinFromBB (0.24),

MaxFromBB (0.8),




//BB HLOC

BStedDevHLOC (2),

BUpperBandHLOC(21), //39

BLowerBandHLOC(21), //39

BBpart4long (28),

BBpart4short (28),


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


double AccountBalance(10000), // Account balance 10,000 $

PctPerTrade(50),

TakeProfit (200),

TakeProfitPct (6.5),

StopPct (0.025),




//Zscore

longminzscore (-2), //-2

shortminzscore (2), //2




//Alerts

MaxAlertsPerBar (1),




minHistogram (-0.1),

maxHistogram (0.1),

minvol (30),
maxvol (200),

bodypartlong (25),
bodypartshort (25);



vars:

shortStop (9999999),

longstop (-9999999),

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

longbuyingPower2 (0),

longbuyingPower3 (0),

shortbuyingPower1 (0),

shortbuyingPower2 (0),

shortbuyingPower3 (0),

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

EHLOC4long (0),

EHLOC4short (0),





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

intrabarpersist trailExit(0),

intrabarpersist tmpTrailExit (0),

intrabarpersist rtPosition(0), // F1 Update on every tick

valuePercentTrail(0),

is_long_symbol(true),




//PL for a day

NetProf(0),

PLTarget(0),




//RSI

vRSI (0),




//MFI

VMFI (0),




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

DonchianMid (0),                




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

high2 (0),

low2 (0),

high3 (0),

low3 (0),

high5 (0),

low5 (0),

high9 (0),

low9 (0),

high26 (0),

low26 (0),




//exit

lastExitPrice (0),




//stop

startlongSL(maximumloss),

updatedlongSL(maximumloss),

startshortSL (maximumloss),

updatedshortSL(maximumloss),

longSL (0),

shortSL (0),




IntrabarPersist lastPrintBar(0),

IntrabarPersist lastAlertBar1(0),

IntrabarPersist crossind1 (false),

IntrabarPersist crossind2 (false),



//Alerts

IntrabarPersist alertsGenerated(0),




IntrabarPersist ExitBarNum (0),

intrabarpersist LastMarketPosition(0);




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

adxcalc = ADX(adxperiod);

longbuyingPower = 3;//(AccountBalance/Close)*PctPerTrade/100; // the amount of shares i can buy //1 //3

longbuyingPower1 = 2; // scale in-out

longbuyingPower2 = 1;

longbuyingPower3 = 1;

shortbuyingPower = 3; //3

shortbuyingPower1 = 2 ; // scale in-out

shortbuyingPower2 = 1 ;

shortbuyingPower3 = 1 ;


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




//BB HLOC 20

vBubHLOC = BollingerBand(HLOC ,BUpperBandHLOC,BStedDevHLOC);

vBlbHLOC = BollingerBand(HLOC ,BLowerBandHLOC, - BStedDevHLOC);

vBmbHLOC = (vBubHLOC+vBlbHLOC)/2;

HLOC = (HIGH+LOW+OPEN+CLOSE)/4;




emaHLOC = XAverage (HLOC , BUpperBandHLOC);

stdHLOC = StdDev(HLOC , BUpperBandHLOC);




EHLOCupband = emaHLOC + stdHLOC;

EHLOCdownband = emaHLOC  - stdHLOC ;

EHLOCmidband = (EHLOCupband+EHLOCdownband)/2;

EHLOCqtr1band = EHLOCdownband+((EHLOCupband-EHLOCdownband)/4);

EHLOCqtr3band = EHLOCupband-((EHLOCupband-EHLOCdownband)/4);

EHLOC4long = EHLOCdownband+((EHLOCupband-EHLOCdownband)*BBpart4long/100);

EHLOC4short = EHLOCupband-((EHLOCupband-EHLOCdownband)*BBpart4short/100);


//BB 200

vBub1= BollingerBand(close,BUpperBand,BStedDev1);

vBlb1= BollingerBand(close,BLowerBand, - BStedDev1);




vBub2= BollingerBand(close,BUpperBand,BStedDev2);

vBlb2= BollingerBand(close,BLowerBand, - BStedDev2);




vBub3= BollingerBand(close,BUpperBand,BStedDev3);

vBlb3= BollingerBand(close,BLowerBand, - BStedDev3);







//BB 20 Exponencial

stdclose = StdDev (close, MidLength);

evBub2 = emaverySlow + (stdDevMultiplier2 * stdclose) ;

evBlb2 = emaverySlow - (stdDevMultiplier2 * stdclose) ;




PrevMACD = MACD(Close, 12, 26)[1];

MACDGradient = MACDLine - PrevMACD;




//ATR

atr =  AvgTrueRange (AtrLength);




//volume calc

//vTicks = Ticks ;

vAvgTicks= AverageFC( Ticks, AvgVolumeLength) ;




//Donchian

DonchianUp = HighestFC (h, DonchianLength );

DonchianDown = LowestFC (l, DonchianLength );

DonchianMid = (DonchianUp + DonchianDown)/2;




//Stoch

stochData1  = Stochastic( H, L, C, StochPiriod1, StochLength1, StochLength2, 1,

oData1FastK, oData1FastD, oData1SlowK, oData1SlowD ) ;


//high and low level
high5 = maxlist(close [1] , open [1], close [2] , open [2], close [3] , open [3], close [4] , open [4], close [5] , open [5] );
low5 = minlist (close [1] , open [1], close [2] , open [2], close [3] , open [3], close [4] , open [4], close [5] , open [5] );



//RSI

vRSI = RSI (close, RsiFastLength);




//MFI

VMFI = MFI (MFILength );

                                           

//Macd

MACDLine = MACD(Close, 12, 26); // Close price, short period, long period

SignalLine = XAverage(MACDLine, 9); // Signal line is a 9-period EMA of the MACD line

Histogram = MACDLine - SignalLine;




//Zcore - Ratio between 2 stocks

Ratio = close / close of data2;

MeanRatio = Average (Ratio , RatioLength);

DevRatio = StdDev (MeanRatio , RatioLength);

Zscore = (Ratio - MeanRatio) / DevRatio ;




//PL for a day

if DATE <> DATE[1]

then

begin

NetProf = NetProf + NetProfit - NetProf[1];

end;

PLTarget = Netprofit - NetProf;




//Trail Alerts

{

if marketposition = -1 and close cross above trailExit and rtPosition =-1 

then begin 

Alert(text("-APEX TEST-","NQ-",shortbuyingPower ,"-BOUGHT SHORT-", FormatDate("dd-MM-yyyy", DateToJulian(Date)), "EXIT ON TRAIL 4", rtPosition, marketposition, trailExit  ));

rtPosition= 0;

end;




if marketposition = 1 and close cross below trailExit and rtPosition =1 

then begin 

Alert(text("-APEX TEST-","NQ-",longbuyingPower ,"-SOLD LONG-", FormatDate("dd-MM-yyyy", DateToJulian(Date)), "EXIT ON TRAIL 3",rtPosition, marketposition, trailExit  ));

rtPosition = 0;

end;

}

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

//reset crossind
if marketposition = 0
then
begin
crossind1 = False;
end;

//reset crossind
if marketposition = 0
then
begin
crossind2 = False;
end;

//close on cross back
if marketposition = 0
then
begin
shortStop = 9999999;
end;

//close on cross back
if marketposition = 0
then
begin
longStop = -9999999;
end;


if marketposition = 0 //Conditions Entry Long
and
PLTarget < PForDay
and 
PLTarget > LForDay
and
Time >= 0100.00 and Time <= 2230.00 //open hours
and
close > Open //* (1*mingap5/100) 
and
close [1] < open [1] 
and
close > close [1] //* (1+mingap8/100)
and
close > low
and
close < emaMid 
and
DonchianDown < DonchianUp * (1-mingap3/100)
and
close < low * (1+maxgap7/100)
and
close <= EHLOC4long 
and 
BarNumber > ExitBarNum + MinBarsAfterCloseToEntry 
and
zscore < longminzscore
and
atr < Atrmax
and
atr > atrmin
and
Histogram < 0

//and
//(
//(Time < 1500.00) or (Time > 1700.00) //trading day start and high volatility in US-EAST hours 
//))
//and
//(
//(close > low[1]) or  (close > close [1])
//)
//price was short but go long 

//* (1-mingap6/100)  //) or 
//(close [2] < open [2]* (1-mingap6/100) )
//) 

//and
//close > low [1]
{
and
(close - low) >= atr * minatrpart/100
and
(close - low) <= atr * maxatrpart/100
}
//and
//low [1] < close [1] * (1-mingap7/100)

//and
//close > close [1]
//and
//close > vBlb2
//and
//vRSI < RsiMinForLong



//and
//Histogram > minHistogram


//and
//vrsi < RsiMinForLong


 //A
//and

//low [1] < low [2]

//and

//(

//(close [1] < open [1])or (close [2] < open [2])

//)




//and

//vRSI < 40

then begin
buy longbuyingPower Shares next bar at market  ;
Alert(text(" model=RITMIC instrument=","NQ shares=",longbuyingPower," type=BOUGHT LONG-", FormatDate("dd-MM-yyyy", DateToJulian(Date)), "-ENTRY LONG",rtPosition, marketposition ));
rtPosition=1;
end;




if marketposition = 0 //Conditions Entry short
and
//(
Time >= 0100.00 and Time <= 2230.00 //open hours
and
PLTarget < PForDay
and 
PLTarget > LForDay
and
close < Open //* (1-mingap5/100) 
and
//oposite
close [1] > open [1] //* (1+mingap6/100)) // or 
and
close < close [1] //* (1-mingap8/100)
and
close < high 
and
close > emaMid
and
DonchianDown < DonchianUp * (1-mingap3/100)
and
close > high * (1-maxgap7/100)
and
close >= EHLOC4short 
and
zscore > shortminzscore
and
BarNumber > ExitBarNum + MinBarsAfterCloseToEntry
and
atr < Atrmax
and
atr > atrmin
and
Histogram > 0

//and
//(
//(Time < 1500.00) or (Time > 1700.00) //trading day start and high volatility in US-EAST hours 
//))

//(close [2] > open [2]* (1+mingap6/100) )
//and
//close < high [1]

//and
//(high - close) >= atr * minatrpart/100
//and
//(high - close) <= atr * maxatrpart/100


//and
//close > vBub1 
//and
//close < vBub2
//and
//vRSI > RsiMaxForShort

//and
//Histogram < maxHistogram


//and
//vrsi > RsiMaxForShort


//and

//high [1] > high [2]


//and

//(

//(close [1] > open [1])or (close [2] > open [2])

//)


//and

//MACDLine > 0

//and

//SignalLine > 0


then begin
sellshort shortbuyingPower Shares next bar at market  ;
Alert(text(" model=RITMIC instrument=","NQ shares=",shortbuyingPower ," type=SOLD SHORT-", FormatDate("dd-MM-yyyy", DateToJulian(Date)), "-ENTRY SHORT",rtPosition , marketposition ));
rtPosition = -1;
end;


//close long position with trail
if marketposition = 1
then
[IntrabarOrderGeneration = True] //trade intra-bar

//close short position with trail (based on low prev) start moving after the first bar from entry

{
//reset crossind
if marketposition = 0
then
begin
crossind1 = False;
end;

//close on cross back
if marketposition = 0
then
begin
longStop = -9999999;
end;

//reset crossind
if marketposition = 0
then
begin
crossind2 = False;
end;
}


//close long position with take profit after small profit
if marketposition = 1 //there is long position open
and
rtPosition =1 
and
(close/entryprice-1)*100 >= SmallMinProfit 
then begin  
sell  longbuyingPower1 Shares next bar at market;
crossind1 = true;
// Generate an intra-bar alert
if alertsGenerated = 0
then begin
Alert(text(" model=RITMIC instrument=","NQ shares=",longbuyingPower1 ," type=SOLD LONG-", FormatDate("dd-MM-yyyy", DateToJulian(Date)), "EXIT ON TAKE PROFIT",rtPosition, marketposition));
alertsGenerated  =1;
end;
end;


if marketposition = 1 //there is long position open
and
(close/entryprice-1)*100 >= SmallMinProfit 
and
barssinceentry > 1
and
crossind1 = true
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
(close/entryprice-1)*100 >= SmallMinProfit 
and
barssinceentry > 1
and
Close < longStop * (1-os1/100) //<
and
crossind1 = true
then begin
Sell longbuyingPower2 Shares Next Bar at Market;
crossind2 = true;

// Generate an intra-bar alert
if alertsGenerated = 0
then begin
Alert(text(" model=RITMIC instrument=","NQ shares=",longbuyingPower2 ," type=SOLD LONG-", FormatDate("dd-MM-yyyy", DateToJulian(Date)), "EXIT ON CROSS 2",rtPosition, marketposition));
alertsGenerated  =1;
end;
end;


 //close long position after cross 1 and go break even
if marketposition = 1 //there is long position open
and
close < (entryprice * 1.000067)
and
barssinceentry > 1
//and
//Close < longStop * (1-os1/100)
and
crossind1 = true
//and
//close > lastExitPrice
Then
begin
Sell Next Bar at Market;

// Generate an intra-bar alert
if alertsGenerated >0 
then begin
if crossind1 = true and crossind2 = false then longbuyingPower3 =1;
//else if crossind1 = true and crossind2 = true then longbuyingPower3 =1;
Alert(text(" model=RITMIC instrument=","NQ shares=",longbuyingPower3 ," type=SOLD LONG-", FormatDate("dd-MM-yyyy", DateToJulian(Date)), "EXIT ON BREAK EVEN"));
alertsGenerated = 0;
rtPosition = 0;
end;
end;

 

// START--  EXIT SHORT BASE OF PRECENT -------------------------------------------------------
if marketposition = -1
then
[IntrabarOrderGeneration = True] //trade intra-bar

// START - EXIT SHORT BASE ON CROSS PREVEVIOS High -------------------------------------------------------
//close short position with trail (based on low prev) start moving after the first bar from entry

{
//reset crossind
if marketposition = 0
then
begin
crossind1 = False;
end;
	
//close on cross back
if marketposition = 0
then
begin
shortStop = 9999999;
end;

//reset crossind
if marketposition = 0
then
begin
crossind2 = False;
end;
}
																			
//close short position with take profit after small profit
if marketposition = -1 //there is short position open
and
rtPosition =-1 
and
(1-close/entryprice)*100 >= SmallMinProfit
//and alertsGenerated = 0
then begin  
buytocover shortbuyingPower1 shares  next bar at market;
crossind1 = true;

// Generate an intra-bar alert
if alertsGenerated = 0
then begin
Alert(text(" model=RITMIC instrument=","NQ shares=",shortbuyingPower1," type=BOUGHT SHORT-", FormatDate("dd-MM-yyyy", DateToJulian(Date)),"EXIT ON TAKE PROFIT",rtPosition, marketposition));
alertsGenerated  =1;
end;
end;


if marketposition = -1 //there is short position open
and
(1-close/entryprice)*100 >= SmallMinProfit
and
barssinceentry > 1
and
crossind1 = true
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
(1-close/entryprice)*100 >= SmallMinProfit
and
barssinceentry > 1
and
Close > shortStop * (1+os1/100) //>
and
crossind1 = true
Then
begin
buytocover shortbuyingPower2 Shares Next Bar at Market;
crossind2 = true;

// Generate an intra-bar alert
if alertsGenerated = 0 
then begin
Alert(text(" model=RITMIC instrument=","NQ shares=",shortbuyingPower2 ," type=BOUGHT SHORT-", FormatDate("dd-MM-yyyy", DateToJulian(Date)), "EXIT ON CROSS 2"));
alertsGenerated  =1;
end;
end;


//close long position after cross 1 and go break even	
if marketposition = -1//there is long position open
and
close > entryprice * 0.999933
and
barssinceentry > 1
//and
//(
//(crossind1 = true) or (crossind2= true)
//)
and
crossind1 = true
Then
begin
buytocover Next Bar at Market;

// Generate an intra-bar alert
if alertsGenerated  > 0
then begin
if crossind1 = true and crossind2 = false then shortbuyingPower3 =1;
Alert(text(" model=MOMENTUM instrument=","NQ shares=",shortbuyingPower3 ," type=BOUGHT SHORT-", FormatDate("dd-MM-yyyy", DateToJulian(Date)), "EXIT ON BREAK EVEN"));
alertsGenerated  =0;
rtPosition = 0;
end;
end;



//SetStopLoss;
if marketposition = 1 and (1-close/entryprice)*100 >= maximumloss and rtPosition =1
then begin
//SetStopLoss(close*AssetMultiplier *maximumloss/100*longbuyingPower );
sell next bar at market;
Alert(text(" model=RITMIC instrument=","NQ shares=",longbuyingPower ," type=SOLD LONG-", FormatDate("dd-MM-yyyy", DateToJulian(Date)), "EXIT ALL LONG ", rtPosition , marketposition ));
rtPosition = 0;
end;

if marketposition = -1 and (close/entryprice-1)*100 >= maximumloss and rtPosition =-1
then begin 
print("exit buy short - EXIT ALL 2");
//SetStopLoss(close*AssetMultiplier *maximumloss/100*shortbuyingPower );
buytocover  next bar at market;
Alert(text(" model=RITMIC instrument=","NQ shares=",shortbuyingPower ," type=BOUGHT SHORT-", FormatDate("dd-MM-yyyy", DateToJulian(Date)), "EXIT ALL SHORT", rtPosition , marketposition  ));
rtPosition = 0;
end;


// CLOSE POSITION AT THE END OF THE DAY
if marketposition = 1
and Time = 2250.00 
then begin
sell next bar at market;
if crossind1 = false then  longbuyingPower3 = 3
else if crossind1 = true and crossind2 = false then longbuyingPower2 =1;
Alert(text(" model=RITMIC instrument=","NQ shares=",longbuyingPower3 ," type=SOLD LONG-", FormatDate("dd-MM-yyyy", DateToJulian(Date)), "EXIT ALL LONG EOD", rtPosition , marketposition ));
alertsGenerated  =0;
rtPosition = 0;
end;

if marketposition = -1
and Time = 2250.00 
then begin
buytocover next bar at market;
if crossind1 = false then  shortbuyingPower3 = 3
else if crossind1 = true and crossind2 = false then shortbuyingPower3 =1;
Alert(text(" model=RITMIC instrument=","NQ shares=",shortbuyingPower3 ," type=BOUGHT SHORT-", FormatDate("dd-MM-yyyy", DateToJulian(Date)), "EXIT ALL SHORT EOD", rtPosition , marketposition  ));
alertsGenerated  =0;
rtPosition = 0;
end;