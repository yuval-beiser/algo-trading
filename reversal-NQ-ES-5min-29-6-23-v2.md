
if marketposition = 0 //Conditions Entry Long
and
(
(PLTarget < PForDay) and (PLTarget > LForDay) 
)  
//and
//(Time > 1500.00 and Time < 2300.00) 
and
close > Open 
and
(
(close > open [1]) or (close > open [2]) 
)
and
(
(close[1] <= open [1]) or (close[2] <= open [2])
)
//and
//close < vBub3 //5
//and
//close >= DonchianUp
and
close cross above EHLOCdownband 
and
close of data2  cross above EHLOCupband2 
and
EHLOCupband > EHLOCdownband * (1+Mingap/100)
{
and
close of data3 cross above EHLOCupband3 
and
close of data4 cross above EHLOCupband4 
and
close of data5 cross above EHLOCupband5 
}

then 
begin
buy longbuyingPower Shares next bar at market  ;
end;



if         
marketposition = 0 //Conditions Entry short
and
(
(PLTarget < PForDay) and (PLTarget > LForDay) 
)  
//and
//(Time > 1500.00 and Time < 2200.00) 
and
close < Open 
and
(
(close < open [1]) or (close < open [2]) 
)
and
(
(close[1] >= open [1]) or (close[2] >= open [2])
)

//and
///close <= DonchianDown
and
close cross below EHLOCupband //2
and
close of data2 cross below EHLOCdownband2 
and

EHLOCupband > EHLOCdownband * (1+Mingap/100)

{
and
close of data3 cross below  EHLOCdownband3 
and
close of data4 cross below  EHLOCdownband4 
and
close of data5 cross below  EHLOCdownband5
}

then
begin
sellshort shortbuyingPower Shares next bar at market  ;
end;


{
if marketposition = -1 //Scale In - Conditions Add Entry Short
and
close < Open
and
close < open [1]
//and
//close[1] >= open[1]
and
close < emaFast
and
(close/entryprice-1)*100 > MinProfitforadd 
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


//close long position with trail start moving after small profit in the first bar from entry
if marketposition = 1 //there is long position open
and
(close/entryprice-1)*100 >= SmallMinProfit 
//and
//barssinceentry < 2
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


//close long position at the EOD
if marketposition = 1
and Time = 2300.00 
then 
begin
sell next bar at market;
end;

{
vars:
longStop (-9999999);

//close short position with trail start moving after the first bar from entry
if marketposition = 0
then
begin
longStop = -9999999;
end;

if marketposition = 1 //there is long position open
//and
//(close/entryprice-1)*100 >= SmallMinProfit 
and
barssinceentry >= 2
then
begin
// Calculate the trailing stop price
if low [1] > longStop 
then
begin
longStop = low[1];
end;
end;
}

{
//close long position with trail start moving aafter the first bar from entry
if marketposition = 1 //there is long position open
and
(close/entryprice-1)*100 >= SmallMinProfit 
and
barssinceentry >= 2
and
Close < longStop 
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


//take profit for a short position with trail start moving in the first bar from entry
if marketposition = -1 //there is short position open
and
(1-Close/entryprice)*100 >= SmallMinProfit 
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

{
vars:
shortStop (9999999);

//close short position with trail start moving after the first bar from entry
if marketposition = 0
then
begin
shortStop = 9999999;
end;

if marketposition = -1 //there is long position open
//and
//(1-Close/entryprice)*100 >= SmallMinProfit 
and
barssinceentry >= 2
then
begin
// Calculate the trailing stop price
if High[1] < shortStop 
then
begin
shortStop = High[1];
end;
end;
}

{
//close short position with trail start moving aafter the first bar from entry
if marketposition = -1 //there is long position open
and
(1-Close/entryprice)*100 >= SmallMinProfit 
and
barssinceentry >= 2
and
Close > shortStop 
Then
begin
buytocover Next Bar at Market;
end;

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


//close short position at the EOD
if marketposition = -1
and Time = 2300.00 
then
begin
buytocover next bar at market;
end;


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
