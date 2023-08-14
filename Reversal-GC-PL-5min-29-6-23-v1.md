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
buy Floor(longbuyingPower) Shares next bar at market  ;
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
sellshort Floor(shortbuyingPower ) Shares next bar at market;
Alert("MGC Reversal Long Model");
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
barssinceentry <= 1
then 
begin
valuePercentTrail = ((entryprice * SmallTrailStop ) /100);
trailProfit = Highest(high , Barssinceentry); 
trailExit = trailProfit + valuePercentTrail; //          
sell next bar at trailExit  stop;
Alert("MGC Reversal Model - Exit Long");
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
Sell longbuyingPower1 Shares Next Bar at Market;
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
crossind1 = true
and
crossind2 = true

//and
//close > lastExitPrice 
Then
begin
Sell longbuyingPower Shares Next Bar at Market;
crossind3 = true;

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
then 
begin
valuePercentTrail = ((entryprice * largeTrail) /100);
trailProfit = Highest(high , Barssinceentry); 
trailExit = trailProfit - valuePercentTrail;        
sell  next bar at trailExit  stop;
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
barssinceentry <= 1
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
end;

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

Then
begin
buytocover shortbuyingPower1 Shares Next Bar at Market;
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
crossind1 = true
and
crossind2 = true

//and
//close > lastExitPrice 
Then
begin
buytocover Next Bar at Market;
crossind3 = true;
end;

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
trailExit = trailProfit - valuePercentTrail;        
buytocover  next bar at trailExit  stop;
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

