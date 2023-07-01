if marketposition = 0 //Conditions Entry Long
and
(
(PLTarget < PForDay) and (PLTarget > LForDay) 
)  
and
(Time > 1500.00 and Time < 2300.00) 
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
and
close cross above EHLOCdownband 
and
close of data2  cross above EHLOCupband2 
and
EHLOCupband > EHLOCdownband * (1+Mingap/100)
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
and
(Time > 1500.00 and Time < 2200.00) 
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
and
close cross below EHLOCupband //2
and
close of data2 cross below EHLOCdownband2 
and
EHLOCupband > EHLOCdownband * (1+Mingap/100)
then
begin
sellshort shortbuyingPower Shares next bar at market  ;
end;

//close long position with trail start moving after small profit in the first bar from entry
if marketposition = 1 //there is long position open
and
(close/entryprice-1)*100 >= SmallMinProfit 
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

//take profit for a short position with trail start moving in the first bar from entry
if marketposition = -1 //there is short position open
and
(1-Close/entryprice)*100 >= SmallMinProfit 
then 
begin
valuePercentTrail = ((entryprice * SmallTrailStop) /100);
trailProfit = Lowest(low , Barssinceentry); 
trailExit = trailProfit + valuePercentTrail; //          
buytocover next bar at trailExit  stop;
end;

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


