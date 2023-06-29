// not in use

{
//close long position with trail start moving after small profit in the first bar from entry
if marketposition = 1 //there is long position open
and
(close/entryprice-1)*100 >= SmallMinProfit 
and
barssinceentry < 3
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
}

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
and
(close/entryprice-1)*100 >= SmallMinProfit 
and
barssinceentry >= 3
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
(close/entryprice-1)*100 >= SmallMinProfit 
and
barssinceentry >= 3
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

{
//close long position at the EOD
if marketposition = 1
and Time = 2300.00 
then 
begin
sell next bar at market;
end;
}

{
//take profit for a short position with trail start moving in the first bar from entry
if marketposition = -1 //there is short position open
and
(1-Close/entryprice)*100 >= SmallMinProfit 
and
barssinceentry < 3
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
}

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
and
(1-Close/entryprice)*100 >= SmallMinProfit 
and
barssinceentry >= 3
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
barssinceentry >= 3
and
Close > shortStop 
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

// not in use - end
