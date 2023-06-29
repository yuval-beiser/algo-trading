// LOGS 


if marketposition = 0 then 
begin
//Long Prints - No position - dbug tag
buydbg= "";
if (
(PLTarget < PForDay) and (PLTarget > LForDay)
)  then 
buydbg = buydbg + "1" else buydbg = buydbg + "X"; // PROFIT OR LOSS IN DAY RANGE
if (Time > 940.00 and Time < 1525.00) then 
buydbg = buydbg + "2" else buydbg = buydbg + "X"; // IN TIME RAGE 
if zscore < longminzscore then  
buydbg = buydbg + "3" else buydbg = buydbg + "X"; // CLOSE > OPEN OR CLOSE < OPEN
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

//Short Prints - No position - dbug tag
// CONDITIONS FOR OPEN SHORT POSISION 
// LOGS 

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

