//@version=31323-2

Inputs: // *** Parameters ***
maximumloss(130), //initial stop loss 
MidLength(30), //number of bars for 30 ema calc
VerySlowLength (200), //number of previous bars for 200 ema calc
Mingap (0.2),  //minimum gap between close and the low the day in pct
Maxgap (0.12), //maximum gap between ema 20 and ema 200 in pct 
Maxgap1 (0.2), //maximum gap between close and ema 200 in pct 
Mingap (0.2),  //minimum gap between close and the low the day in pct
SmallMinProfit (0.1), //minimum porfit fot start moving the trail stop in pct
SmallTrail (0.01875),  //trail stop gap in pct
AtrLength (14), //number of previous bars for ATR calculation
Atrmax (15),//max atr for enter 
os1 (0.0133),//off set for crossing ema200 in pct
PForDay (1500), //maximum profit in usd  
LForDay (-200), //maximum loss in usd  

//macd
macdFastLength( 12 ), 
macdSlowLength( 26 ), 
MACDlineLength( 9 ) ;

vars: //*** Calc Variable ***
emaVerySlow (0),
emaMid (0),
emaMid30 (0),
atr (0),
longbuyingPower(0),
buydbg(""),
selldbg(""),
valsdbg(""),

//macd
vMacd(0), 
vMacdAvg(0), 
vDiff(0) ,

// Trailing
barCount(0), // count from the first bar
high1stBar(0), // Extreme high from a list 
low1stBar(0), // Extreme low from a list 
trailProfit(0),
SmallTrailStop(SmallTrail ), 
FastTrailStop(0.34),
intrabarpersist trailExit(0), // F1 Update on every tick
valuePercentTrail(0),
is_long_symbol(true),

//PL for a day
NetProf(0),
PLTarget(0),
        
//Macd
MACDLine (0),
SignalLine (0),
Histogram (0),

//Extreme points
high9 (0);

// *** Formula ***

[IntrabarOrderGeneration = true] //trade intra-bar

emaMid30 = XAverage(close,MidLength); 
emaverySlow = XAverage(close,VerySlowLength);
longbuyingPower = 2 ;//(AccountBalance/Close)*PctPerTrade/100; // the amount of shares to buy 

//macd
vMacd = MACD( Close, macdFastLength, macdSlowLength ) ; // Fast line MACD
vMacdAvg = XAverage( vMacd , MACDlineLength) ; // Slow line MACD
vDiff = vMacd - vMacdAvg ; // Histogram

//ATR
atr =  AvgTrueRange (AtrLength);

//high and low level
high9 = maxlist (close [1] , open [1], close [2] , open [2], close [3] , open [3], close [4] , 
open [4], close [5] , open [5], close [6] , open [6], close [7] , open [7], close [8] , open [8], close [9] , open [9]  );

//Macd
MACDLine = MACD(Close, 12, 26); // Close price, short period, long period
SignalLine = XAverage(MACDLine, 9); // Signal line is a 9-period EMA of the MACD line
Histogram = MACDLine - SignalLine;

//PL for a day
if DATE <> DATE[1] 
then 
begin
NetProf = NetProf + NetProfit - NetProf[1];
end;
PLTarget = Netprofit - NetProf;

//*** Conditions Entry Long ***

if marketposition = 0 
and
(
(PLTarget < PForDay) and (PLTarget > LForDay) //p&l for a day limits
)  
and
(
(Time > 600.00) and (Time < 2200.00) //long momentum time
)
and
close > Open //3
and
close > high9
and
close > emaverySlow * (1 + os1 /100)  //200
and
emaMid <= emaverySlow * (1+Maxgap/100) //*
and 
close <= emaverySlow * (1+Maxgap1/100) //*
and 
atr < AtrMax
and
close > lowD (0) * (1+Mingap/100)
and
Histogram > 0
then 
begin
buy longbuyingPower Shares next bar at market  ;
end;

//***Exit Conditions***

//close long position with trail start moving after small profit 
if marketposition = 1 //there is long position open
and
(close/entryprice-1)*100 >= SmallMinProfit 
and
barssinceentry <= 1
then 
begin
valuePercentTrail = ((entryprice * SmallTrailStop) /100);
trailProfit = Highest(high , Barssinceentry); 
trailExit = trailProfit - valuePercentTrail;        
sell  next bar at trailExit  stop;
end;

//Set initial stop
if marketposition = 1
then
begin
SetStopLoss(maximumloss);
end;

//*** Prints ***
if marketposition = 0 then 

//Long Prints - No position - build dbug tag
buydbg= ""; 
if 
(
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


//no position prints
if marketposition = 0  
and
ELDateToString(date) = "07/13/2023" 
then
print ( "MOM  > symbol=" , symbol," ", "islong=", is_long_symbol,  "no position","  ",
 ELDateToString(date),"Time=", time,"buydbg=", buydbg, "  ", "selldbg=", selldbg,
 "     ","bar=", BarNumber,
"entryprice=","xxxx.xx", 
"close=", close, 
"Close[1]=", Close[1], "Close[2]=", Close[2],
"open=", Open, "open[1]=", Open[1], "open[2]=", Open[2],
"low=", low, "low[1]=", Low[1], "low[2]=", Low[2],
"high=", high, "high[1]=", high[1], "high[2]=", High[2],
"openD0=", OpenD(0), "closeD1=", CloseD(1));


//long position prints
if marketposition = 1 
and ELDateToString(date) = "07/13/2023" 
then 
print ( "MOM   > symbol=" , symbol," ",  "in long", "      "
,ELDateToString(date),"Time=", time,"buydbg=", buydbg, "     ","bar=", BarNumber,
"entryprice=",entryprice, 
"close=", close, 
"Close[1]=", Close[1], "Close[2]=", Close[2],
"open=", Open, "open[1]=", Open[1], "open[2]=", Open[2],
"low=", low, "low[1]=", Low[1], "low[2]=", Low[2],
"high=", high, "high[1]=", high[1], "high[2]=", High[2],
"openD0=", OpenD(0), "closeD1=", CloseD(1));



