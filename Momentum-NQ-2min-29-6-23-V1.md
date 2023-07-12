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

//close long position with trail start moving aafter the first bar from entry
if marketposition = 1 //there is long position open
and
(close/entryprice-1)*100 >= SmallbaseProfit 
and
barssinceentry > 1
and
Close < longStop * (1-os1/100)
Then
begin
Sell Next Bar at Market;
end;

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
