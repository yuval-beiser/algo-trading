//@version=Reversal Strategy ETF 5423-1
Inputs:
FastLength(9),
MidLength(20),
SlowLength(50), //50
VerySlowLength(200),
MidLength1(30),
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
SmallMinProfit (0.12), //1.4 //1.5
smallbaseProfit (0.05),
smallbaseProfit1 (0.05), //0.035 //0.19 //0.02 //0.1 //0.5 //CROSS2:0.059 (9P) 
LargeMinProfit (2.5),
SmallTrail (0.05), //0.04375 with stochastic //0.00625 //0.3
largeTrail (1.6),
FastTrail (0.22),
os1 (0.0133),
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
SL(200),
PForDay (2000), //1500
LForDay (-50), //-1100
longSL(150), //240
shortSL(150), //240


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
emaMid30 (0),
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
buyingPower1 (0),
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

crossind1 (false),
crossind2 (false),
crossind3 (false),

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

//vars:
longStop (-9999999);


if marketposition = 0
then
[IntrabarOrderGeneration = true] //trade intra-bar
                        
smaFast = Average(close,FastLength);
smaMid = Average(close,MidLength);
//ema3VerySlow = XAverage(close,VerySlowLength) of data3;
smaSlow = Average(close,SlowLength);
emaSlow = XAverage(close,SlowLength);
emaverySlow = XAverage(close,VerySlowLength);
emaFast = XAverage(close,FastLength);
emaMid30 = XAverage(close,MidLength1);


emafast1 = XAVERAGE(XAVERAGE(close,FastLength),FastLength);
demafast = emaFast * 2 - emafast1  ;    

ema2Fast = XAverage(close,FastLength)of data2;
ema2Slow = XAverage(close,SlowLength)of data2;
ema2verySlow = XAverage(close,VerySlowLength)of data2;
rsiSlow = rsi(close,RsiSlowLength);
rsiFast = rsi(close,RsiFastLength);
mom = Momentum(close, MomentumLength);
adxcalc = ADX(adxperiod);
buyingPower = 3;//(AccountBalance/Close)*PctPerTrade/100; // the amount of shares i can buy
buyingPower1 = 1;
TakeProfitAmt = AccountBalance*PctPerTrade/100*TakeProfitPct/100;
StopAmt = AccountBalance*PctPerTrade/100*StopPct/100;
valsdbg = "close=" + NumToStr(close ,2) + " dailyhigh=" + NumToStr(dailyhigh ,2) + " dailylow =" + NumToStr(dailylow ,2); // + " close =" + NumToStr(close ,2) + " close =" + NumToStr(close ,2) + " close =" + NumToStr(close ,2) + " close =" + NumToStr(close ,2) + " close =" + NumToStr(close ,2);
//print(Date, Time, "bar=", BarNumber, marketposition, valsdbg ); 

//BB
vBub1= BollingerBand(close,BUpperBand,BStedDev1);
vBlb1= BollingerBand(close,BLowerBand, - BStedDev1);
  
vBub2= BollingerBand(close,BUpperBand,BStedDev2);
vBlb2= BollingerBand(close,BLowerBand, - BStedDev2);

vBub3= BollingerBand(close,BUpperBand,BStedDev3);
vBlb3= BollingerBand(close,BLowerBand, - BStedDev3);

//VWAP crossing
vwap = Average(close * Volume, vwapLength ) / Average(Volume, vwapLength );

//Macd
MACDLine = MACD(Close, 12, 26); // Close price, short period, long period
SignalLine = XAverage(MACDLine, 9); // Signal line is a 9-period EMA of the MACD line
Histogram = MACDLine - SignalLine;

//ATR
atr =  AvgTrueRange (AtrLength);

//volume calc
//vTicks = Ticks ;
vAvgTicks= AverageFC( Ticks, AvgVolumeLength) ;

//Stoch
stochData1  = Stochastic( H, L, C, StochPiriod1, StochLength1, StochLength2, 1, 
oData1FastK, oData1FastD, oData1SlowK, oData1SlowD ) ; 

//Donchian
DonchianUp = HighestFC (h, DonchianLength );
DonchianDown = LowestFC (l, DonchianLength );
DonchianMid = (DonchianUp + DonchianDown)/2;

//RSI
vRSI = RSI (close, RsiFastLength);

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


if marketposition = 0 then 
begin
//Long Prints - No position - dbug tag
buydbg= "";
if (
(PLTarget < PForDay) and (PLTarget > LForDay)
)  then 
buydbg = buydbg + "1" else buydbg = buydbg + "X";
if (Time > 940.00 and Time < 1525.00) then 
buydbg = buydbg + "2" else buydbg = buydbg + "X";
if zscore < longminzscore then 
buydbg = buydbg + "3" else buydbg = buydbg + "X";
if close > open then 
buydbg = buydbg + "4" else buydbg = buydbg + "X";
if close > close[1]   then 
buydbg = buydbg + "5" else buydbg = buydbg + "X";
if close < vBlb1 then
buydbg = buydbg + "6" else buydbg = buydbg + "X";
if close <= DonchianMid then
buydbg = buydbg + "7" else buydbg = buydbg + "X";
if close cross above emafast then
buydbg = buydbg + "8" else buydbg = buydbg + "X";

{
//Short Prints - No position - dbug tag
selldbg = "";
if (
(PLTarget < PForDay) and (PLTarget > LForDay)
)  then
selldbg = selldbg + "1" else selldbg = selldbg + "X" ;
if (Time > 940.00 and Time < 1525.00) then
selldbg = selldbg + "2" else selldbg = selldbg + "X" ;
if emaverySlow < emaFast * (1-MinGapSlowToMid/100) then
selldbg = selldbg + "4" else selldbg = selldbg + "X" ;
if close > High *(1-MaxFromLHEntry/100) then
selldbg = selldbg + "6" else selldbg = selldbg + "X" ;
if close >= emaFast * (1-MaxEMAGap/100) then
selldbg = selldbg + "7" else selldbg = selldbg + "X" ;
if close <= emaFast * (1-MinEMAGap/100) then
selldbg = selldbg + "8" else selldbg = selldbg + "X" ;  
if ((Close[1] >= emaFast [1]) or (Close[2] >= emaFast [2]))  then
selldbg = selldbg + "9" else selldbg = selldbg + "X" ; 
if ((High >= emaFast)  or (high [1] >= emaFast [1]))    then
selldbg = selldbg + "A" else selldbg = selldbg + "X";
if close < close[1] then
selldbg = selldbg + "B" else selldbg = selldbg + "X";
if close < low [1] then
selldbg = selldbg + "C" else selldbg = selldbg + "X";
if ((open[1] <= Close [1]) or (open [2] <= Close [2]) or (open [3] <= Close [3]))  then
selldbg = selldbg + "D" else selldbg = selldbg + "X";
if close < vwap  then
selldbg = selldbg + "E" else selldbg = selldbg + "X";
if 
(
stochData1 = 1 //F
and
oData1FastK < oData1SlowD 
//and
//oData1FastK < StochOverBot 
and
oData1FastK < StochOverBot
and  
(
(oData1FastK [1] > oData1SlowD [1]) or (oData1FastK [2] > oData1SlowD [2]) or (oData1FastK [3] > oData1SlowD [3])
)  
and
(
(oData1FastK [1] > StochOverBot) or (oData1FastK [2] > StochOverBot) or(oData1FastK [3] > StochOverBot) 
)
)
then                                                                                                                                                                                                                                                                                                                  
selldbg = selldbg + "F" else selldbg = selldbg + "X";
if Close > vBub1     then                                                                                                                                                                                                                                                                                                               
selldbg = selldbg + "G" else selldbg = selldbg + "X";
if DonchianDown < DonchianUp * (1-Mingap/100)  then                                                                                                                                                                                                                                                                                                                 
selldbg = selldbg + "H" else selldbg = selldbg + "X";
}


if marketposition = 0  
and
ELDateToString(date) = "06/27/2023" //and symbol = "soxs" //and Time = 1300
//and (close cross over emaFast  or close cross below emaFast )
then
//Long Prints - but No position
print ( "ARB> symbol=" , symbol," ", "islong=", is_long_symbol,  "no position","  ", ELDateToString(date),"Time=", time,"buydbg=", buydbg, "  ", "selldbg=", selldbg,
 "     ","bar=", BarNumber,
"entryprice=","xxxx.xx", 
"close=", close, 
"zscore=", Zscore ,
"emaFast=" , emaFast,
"PLTarget=", PLTarget,
"vwap=", vwap,
"demaFast =", demafast , "emaslow=", emaSlow,
"emaverySlow =", emaverySlow , "ema3verySlow=" , ema3VerySlow , 
"close2=", close of data2, "ema2=",ema2Slow , "emaVerySlow=", ema3VerySlow, 
"Close[1]=", Close[1], "Close[2]=", Close[2],
"open=", Open, "open[1]=", Open[1], "open[2]=", Open[2],
"low=", low, "low[1]=", Low[1], "low[2]=", Low[2],
"high=", high, "high[1]=", high[1], "high[2]=", High[2],
"openD0=", OpenD(0), "closeD1=", CloseD(1),
"LowD(0)=", LowD(0), "HighD(0)=", HighD(0),  
"adxcalc =", adxcalc ,"adxmin=", adxmin , "MinProfit =",SmallMinProfit
 ,"MinEMAGap=" , MinEMAGap,"MaxEMAGap=" , MaxEMAGap,
 "smaFast=", smaFast, "smaMid=", smaMid, "smaSlow =", smaSlow ,
  "MinGapSlowToMid=", MinGapSlowToMid,  
"TakeProfitPct =", TakeProfitPct , "StopPct=", StopPct);


//calc a switch for identify long or short (for the connection with VXX)
if symbol = "SOXS" or symbol = "LABD" or symbol = "SQQQ" then
is_long_symbol = False;

//Conditions Entry Long
if marketposition = 0  
and
(
(PLTarget < PForDay) and (PLTarget > LForDay)
)  //and PLTarget > PLForDay and ) //1
//and
//(Time > 940.00 and Time < 1525.00) //Increase from 9:35 to filter noise at the open ("no trade zone") //2 

and zscore < longminzscore 
and close > open
and close > maxlist (open [1], close [1], open [2], close [2], open [3], close [3])
and close < vBlb1
and close <= DonchianMid
and close > emafast
and Histogram > 0

//(close cross above emafast) or 
//(close [1] cross above emafast [1]) or 
//(close [2] cross above emafast [2]) or
//(close [3] cross above emafast [3])
//)
//and
//atr < 1.4
//and
//close > maxlist (open [1], close [1] , open [2] , close [2])

{
(
(open[1] >= Close [1]) or (open [2] >= Close [2])
)
and
(
(close [3] cross above emaFast [3]) or
(close [4] cross above emaFast [4]) or
(close [5] cross above emaFast [5]) or
(close [6] cross above emaFast [6]) or
(close [7] cross above emaFast [7]) or //or (close[1] cross above emaFast [1] )
(close [8] cross above emaFast [8]) or
(close [9] cross above emaFast [9])
}
//)        

//and
//(Time > 940.00 and Time < 1525.00) //Increase from 9:35 to filter noise at the open ("no trade zone") //2 
//and
//((close of data2 > ema2Fast and is_long_symbol = False)  //and close of data2 > ema2Slow//3 
//or
//(close of data2 < ema2Fast and is_long_symbol = True))//and close of data2 < ema2Slow //market regime - there is fear /0

//and
//adxcalc >= adxmin //1
//and 
//mom >= Longminmom//4
//and
//smaFast < smaSlow //2
//and
//emaverySlow > emaFast *(1+MinGapSlowToMid/100) //4 //
//and
//close <= HighD(0) * (1-MinFromLH/100) //3
//and
//close <= LowD(0)of data3 *(1+MaxFromLH/100) //5
//and
//close < Low *(1+MaxFromLHEntry/100) //6
//and
//close >= Low *(1+MinFromLHEntry/100) 
//and
//close <= emaFast * (1+MaxEMAGap/100) //7 //delete just for backtest
//and
//close >= emaFast * (1+MinEMAGap/100)//8
//and
//((Close[1] <= emaFast [1]) or (Close[2] <= emaFast [2])) //9
//and
//((low <= emaFast) or (low [1] <= emaFast [1])) //A //checked if better with previous candle
//and
//close > close[1] //or (close [1] > close[2])) //B
//and
//close > high [1] //C
//and
//low >= low[1] //
//and
//((open[1] >= Close [1]) or (open [2] >= Close [2]) or (open [3] >= Close [3])) //D
//and
//close < smaSlow //C
//and
//Close  < CloseD(1) of data3  * (1-MinFromCloseD1/100) //min gap //
//and
//close < closed (1) of data3 //filter enter into momentum //
//and
//Close < ema3VerySlow * (1-MinFrom200/100)  //A
//and
//((Ticks > vAvgTicks * (1+volumeUP/100)) or (Ticks [1] > vAvgTicks [1] * (1+volumeUP/100))) //A
//and
//close > vwap //or (close[1] > vwap [1])) //B //7323 check if to delete !!! //30.4.23 return VWAP //E
//and
//Close <= vBlb1 //F
//and
//Close > vBlb3 //

//and
//(
//stochData1 = 1  //5
//and
//oData1FastK > oData1SlowD 
//and
//oData1FastK > StochOverSold 
//and
//oData1FastK > StochOverSold
//and  
//(
//(oData1FastK [1] < oData1SlowD [1]) or (oData1FastK [2] < oData1SlowD [2]) or (oData1FastK [3] < oData1SlowD [3])
//) 
//and
//(
//(oData1FastK [1] < StochOverSold) or (oData1FastK [2] < StochOverSold) or (oData1FastK [3] < StochOverSold) 
//)
//)

//and
//(
// (vRSI[1] < RSIOversold) or (vRSI[2] < RSIOversold) or (vRSI[3] < RSIOversold)
//)
//and
//DonchianDown < DonchianUp * (1-Mingap/100) //H
//and
//((close cross above emaFast of data3) or (close[1] cross above emaFast [1] of data3))  //I


then 
Begin
buy Floor(buyingPower) Shares next bar at market  ;
End;


//Short
//Conditions Entry Short 
if marketposition = 0  
and
(
(PLTarget < PForDay) and (PLTarget > LForDay)
)  //and PLTarget > PLForDay) //and ) //1
//and
//(Time > 940.00 and Time < 1525.00) //Increase from 9:35 to filter noise at the open ("no trade zone") //2     

and zscore > shortminzscore 
and close < open
and close < minlist (open [1], close [1], open [2], close [2], open [3], close [3])
and ((open[1] <= Close [1]) or (open [2] <= Close [2]) )
and close > vBub1
and close >= DonchianMid
and close < emafast
and Histogram < 0

//and
//(
//(close cross below emafast) or 
//(close [1] cross below emafast [1]) or 
//(close [2] cross below emafast [2]) or
//(close [3] cross below emafast [3])

//)
//and
//atr < 1.4
//and
//close < minlist (open [1], close [1] , open [2] , close [2])


//((close of data2 < ema2Fast //and close of data2 < ema2Slow  //3
//and is_long_symbol = False) 
//or 
//(close of data2 > ema2Fast // and close of data2 > ema2Slow 
//and is_long_symbol = True)) 
//and
//adxcalc >= adxmin //1
//and
//emaverySlow < emaFast * (1-MinGapSlowToMid/100) //4 //
//and
//close >= LowD(0) * (1+MinFromLH/100) //
//and
//close >= HighD(0)of data3 * (1-MaxFromLH/100) //5
//and
//close > High *(1-MaxFromLHEntry/100) //6
//and
//close <= High *(1-MinFromLHEntry/100) 
//and
//close >= emaFast * (1-MaxEMAGap/100) //7 //delete just for backtest
//and
//close <= emaFast * (1-MinEMAGap/100) //8 
//and
//((Close[1] >= emaFast [1]) or (Close[2] >= emaFast [2])) //9
//and
//((High >= emaFast)  or (high [1] >= emaFast [1])) //A //checked if better with previous candle
//and
//close < close[1] //or (Close [1] < Close [2])) //B
//and
//close < low [1] //C
//and
//high <= high [1] //
//and
//((open[1] <= Close [1]) or (open [2] <= Close [2]) or (open [3] <= Close [3])) //D
//and
//close > smaSlow //C
//and
//Close > CloseD (1) of data3  * (1+MinFromCloseD1/100) //min gap //
//and
//close > closed (1) of data3 //filter enter into momentum  /
//and
//Close > ema3VerySlow * (1+MinFrom200/100) //
//and
//((Ticks > vAvgTicks * (1+volumeUP/100)) or (Ticks [1] > vAvgTicks [1] * (1+volumeUP/100)))  //A
//and
//close < vwap //or (close[1] < vwap [1])) //7323 check if to delete !!! //E //30.4.23 return VWAP //E
//and
//Close >= vBub1 //F
//and
//Close < vBub3 //C
//and
//(
//stochData1 = 1 //F
//and
//oData1FastK < oData1SlowD 
//and
//oData1FastK < StochOverBot 
//and
//oData1FastK < StochOverBot
//and  
//(
//(oData1FastK [1] > oData1SlowD [1]) or (oData1FastK [2] > oData1SlowD [2]) or (oData1FastK [3] > oData1SlowD [3])
//)  
//and
//(
//(oData1FastK [1] > StochOverBot) or (oData1FastK [2] > StochOverBot) or(oData1FastK [3] > StochOverBot) 
//)
//)
//and
//(
 //(vRSI[1] > RSIOverbot) or (vRSI[2] > RSIOverbot) or (vRSI[3] > RSIOverbot)
//)

//and
//DonchianDown < DonchianUp * (1-Mingap/100) //H
//and
//((close cross below emaFast of data3) or (close[1] cross below emaFast of data3 [1]))  //I
then 
Begin
sellshort Floor(buyingPower) Shares next bar at market;
End;


End;

if marketposition = 1
then
[IntrabarOrderGeneration = True] //trade intra-bar

//close long position with trail start moving after minimum profit 
if marketposition = 1 //there is long position open
and
(Close/entryprice-1)*100 >= SmallMinProfit 
and
barssinceentry <= 2
then 
begin
valuePercentTrail = ((entryprice * SmallTrailStop ) /100);
trailProfit = Highest(high , Barssinceentry); 
trailExit = trailProfit + valuePercentTrail; //          
sell next bar at trailExit  stop;
end;



//close short position with trail start moving after the first bar from entry
if marketposition = 0
then
begin
longStop = -9999999;
end;


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

//reset crossind 
if marketposition = 0
then
begin
crossind3 = False;
end;


if marketposition = 1 //there is long position open
and
(close/entryprice-1)*100 >= smallbaseProfit 
and 
barssinceentry > 1
//and
//barssinceentry >= 5
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
Sell buyingPower1 Shares Next Bar at Market;
crossind1 = true;
end;


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

Then
begin
Sell buyingPower1 Shares Next Bar at Market;
crossind2 = true;
end;
	

	
//close long position after cross ema 200-1
if marketposition = 1 //there is long position open
and
(close/entryprice-1)*100 >= SmallbaseProfit 
and
barssinceentry > 1
//and
//Close < longStop * (1-os1/100)
and
close cross below vBub1 
and
(
(crossind1 = true)
or
(crossind2 = true)
)

//and
//close > lastExitPrice 
Then
begin
Sell buyingPower Shares Next Bar at Market;
crossind3 = true;
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
(
(crossind1 = true)
or
(crossind2 = true)
or
(crossind3 = true)
)
//and
//close > lastExitPrice 
Then
begin
Sell Next Bar at Market;
end;

{
//close long position with trail start moving after large profit 
if marketposition = 1 //there is long position open
and
(close/entryprice-1)*100 >= largeMinProfit 
and
(
(close of data2 >= ema2verySlow  and is_long_symbol = False) //there is a fear
or
(close of data2 <= ema2verySlow          and is_long_symbol = True)
) 
then 
begin
valuePercentTrail = ((entryprice * LargeTrailStop ) /100);
trailProfit = Highest(high of data3, Barssinceentry); 
trailExit = trailProfit - valuePercentTrail;        
sell  next bar at trailExit  stop;
end;
}

{
//close long position with trail when moving fast and vix doesn't cross his ema 200 
if marketposition = 1 //there is long position open
and
(close/entryprice-1)*100 >= FastMinProfit 
and
barssinceentry <= Minbarsfortake 
//and
//(
//(close of data2 <= ema2verySlow  and is_long_symbol = False) 
//or
//(close of data2 >= ema2verySlow          and is_long_symbol = True)
//)
then 
begin
valuePercentTrail = ((entryprice * FastTrailStop) /100);
trailProfit = Highest(high of data3, Barssinceentry); 
trailExit = trailProfit - valuePercentTrail;        
sell  next bar at trailExit  stop;
end;
}

{
//close long position after cross ema back
if marketposition = 1 //there is long position open
and
(close/entryprice-1)*100 >= MinBaseProfit1 
and
Close cross below emaFast * (1-CrossEMAos/100)
then 
begin
sell  next bar at market;
end;
}

{
//there is long position open and pass too much time without profit
if marketposition = 1
and
(close/entryprice-1)*100 <= MinBaseProfit 
and 
barssinceentry > MinBarsForMove 
then
sell next bar at low [1]  stop;
}

{
//close long position when touch ema 200 
if marketposition = 1 //there is long position open
and
(emaverySlow/entryprice-1)*100 >=  SmallMinProfit 
then 
begin
sell next bar at emaVerySlow limit;
end;
}

{
//close long position at the EOD
if marketposition = 1
and Time = 1600.00 
then sell next bar at market;
}
{
//long position prints
if marketposition = 1 
//and ELDateToString(date) = "05/02/2023" //and symbol = "soxs" //and Time = 1300
then 
print ( "ARB> symbol=" , symbol," ",  "in long", "      ",ELDateToString(date),"Time=", time,"buydbg=", buydbg, "     ","bar=", BarNumber,
"entryprice=",entryprice, 
"close=", close, 
"zscore=", Zscore ,
"emaFast=" , emaFast,
"PLTarget=", PLTarget,
"vwap=", vwap,
"demaFast =", demafast , "emaslow=", emaSlow,
"emaverySlow =", emaverySlow , "ema3verySlow=" , ema3VerySlow , 
"close2=", close of data2, "ema2=",ema2Slow , "emaVerySlow=", ema3VerySlow, 
"Close[1]=", Close[1], "Close[2]=", Close[2],
"open=", Open, "open[1]=", Open[1], "open[2]=", Open[2],
"low=", low, "low[1]=", Low[1], "low[2]=", Low[2],
"high=", high, "high[1]=", high[1], "high[2]=", High[2],
"openD0=", OpenD(0), "closeD1=", CloseD(1),
"LowD(0)=", LowD(0), "HighD(0)=", HighD(0),  
"adxcalc =", adxcalc ,"adxmin=", adxmin , "MinProfit =",SmallMinProfit
 ,"MinEMAGap=" , MinEMAGap,"MaxEMAGap=" , MaxEMAGap,
 "smaFast=", smaFast, "smaMid=", smaMid, "smaSlow =", smaSlow ,
  "MinGapSlowToMid=", MinGapSlowToMid,  
"TakeProfitPct =", TakeProfitPct , "StopPct=", StopPct);
}

if marketposition = -1
then
[IntrabarOrderGeneration = True] //trade intra-bar


//close short position with trail start moving after minimum profit
if marketposition = -1 //there is long position open
and
(1-Close/entryprice)*100 >= SmallMinProfit 
and 
barssinceentry <= 2
//and
//close of data2 < ema2Fast
//and
//close of data2 > ema2verySlow
//and
//(
//(close of data2 > ema2verySlow  and is_long_symbol = False) //there is a fear
//or
//(close of data2 < ema2verySlow          and is_long_symbol = True)
//) 
//and
//barssinceentry > MinBarsForMove
//and
//barssinceentry > Minbarsfortake
then 
begin
valuePercentTrail = ((entryprice * SmallTrailStop ) /100);
trailProfit = Lowest(low , Barssinceentry); 
trailExit = trailProfit + valuePercentTrail; //          
buytocover next bar at trailExit  stop;
end;


vars:
shortStop (9999999);

//close short position with trail start moving after the first bar from entry
if marketposition = 0
then
begin
shortStop = 9999999;
end;

if marketposition = -1 //there is long position open
and
(1-Close/entryprice)*100 >= smallbaseProfit 
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
buytocover buyingPower1 Shares Next Bar at Market;
crossind1 = true;
end;

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

Then
begin
buytocover buyingPower1 Shares Next Bar at Market;
crossind2 = true;
end;
	

	
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
(
(crossind1 = true)
or
(crossind2 = true)
)

//and
//close > lastExitPrice 
Then
begin
buytocover Next Bar at Market;
crossind3 = true;
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
(
(crossind1 = true) or (crossind2= true) or (crossind3=true)
)
//and
//close > lastExitPrice 
Then
begin
buytocover Next Bar at Market;
end;


{
//close short position with trail start moving after large profit 
if marketposition = -1 //there is long position open
and
(1-Close/entryprice)*100 >= LargeMinProfit 
and
(
(close of data2 <= ema2verySlow  and is_long_symbol = False)  //no fear
or
(close of data2 >= ema2verySlow          and is_long_symbol = True)
) 
then 
begin
valuePercentTrail = ((entryprice * LargeTrailStop ) /100);
trailProfit = Lowest(low of data3, Barssinceentry); 
trailExit = trailProfit + valuePercentTrail; //          
buytocover next bar at trailExit  stop;
end;
}

{
//close short position with trail when moving fast and vix doesn't cross his ema 200 
if marketposition = -1 //there is long position open
and
(1-close/entryprice)*100 >= FastMinProfit 
and
barssinceentry <= Minbarsfortake 
//and
//(
//(close of data2 >= ema2verySlow  and is_long_symbol = False) 
//or
//(close of data2 <= ema2verySlow          and is_long_symbol = True)
//)
then 
begin
valuePercentTrail = ((entryprice * FastTrailStop) /100);
trailProfit = Lowest(low of data3, Barssinceentry); 
trailExit = trailProfit + valuePercentTrail; //          
buytocover next bar at trailExit  stop;
end;
}

{
//close short position after cross ema back
if marketposition = -1 //there is long position open
and
(1-Close/entryprice)*100 >= MinBaseProfit1 
and
Close cross above emaFast * (1+CrossEMAos/100)
then 
begin
buytocover next bar at market;
end;
}

{
if marketposition = -1 //there is short position opens and pass too much time without profit
and
(1-Close/entryprice)*100 <= MinBaseProfit 
and
barssinceentry > MinBarsForMove 
then
buytocover next bar at High [1] stop;
}


//close short position for a Small reversal
//if marketposition = -1 //there is short position opens
//and 
//(HighD(0)/CloseD(1)-1)*100 < MinOpenGapPct
//and
//(1-Close/entryprice)*100 >= SmallMinProfit
//and
//high[1] < high[2]
//then 
//buytocover next bar at Close[1]*(1+StopLossOS/100) stop;

{
//close short position when touch ema 200 
if marketposition = -1 //there is short position open
and
(1-emaverySlow/entryprice)*100 >=  SmallMinProfit 
then 
begin
buytocover next bar at emaVerySlow limit;
end;
}
       
//close short position at the EOD
//if marketposition = -1
//and Time = 1600.00 
//then buytocover next bar at market;
  
{
//short position prints       
if marketposition = -1 
//and ELDateToString(date) = "05/02/2023" //and symbol = "soxs"//and Time = 1300
then 
print ( "ARB> symbol=" , symbol," ", "in short","     ", ELDateToString(date),"Time=", time,"selldbg=", selldbg , "     ","bar=", BarNumber,
"entryprice=",entryprice, 
"close=", close, 
"zscore=", Zscore ,
"emaFast=" , emaFast,
"PLTarget=", PLTarget,
"vwap=", vwap,
"demaFast =", demafast , "emaslow=", emaSlow,
"emaverySlow =", emaverySlow , "ema3verySlow=" , ema3VerySlow , 
"close2=", close of data2, "ema2=",ema2Slow , "emaVerySlow=", ema3VerySlow, 
"Close[1]=", Close[1], "Close[2]=", Close[2],
"open=", Open, "open[1]=", Open[1], "open[2]=", Open[2],
"low=", low, "low[1]=", Low[1], "low[2]=", Low[2],
"high=", high, "high[1]=", high[1], "high[2]=", High[2],
"openD0=", OpenD(0), "closeD1=", CloseD(1),
"LowD(0)=", LowD(0), "HighD(0)=", HighD(0),  
"adxcalc =", adxcalc ,"adxmin=", adxmin , "MinProfit =",SmallMinProfit
 ,"MinEMAGap=" , MinEMAGap,"MaxEMAGap=" , MaxEMAGap,
 "smaFast=", smaFast, "smaMid=", smaMid, "smaSlow =", smaSlow ,
  "MinGapSlowToMid=", MinGapSlowToMid,  
"TakeProfitPct =", TakeProfitPct , "StopPct=", StopPct);
}
{
//Take profit for Long
if marketposition = 1
then
SetProfitTarget(TakeProfitAmt);
}
//Take profit for Short
//if marketposition = -1
//then
//SetProfitTarget(TakeProfitAmt);

{
//Initial Stop Loss for Long
if marketposition = 1
then
SetStopLoss(StopAmt);
}
//Initial Stop Loss for Short
//if marketposition = -1
//then
//SetStopLoss(StopAmt);

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





