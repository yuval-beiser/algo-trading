// CONDITIONS FOR OPEN LONG POSITION 

//Conditions Entry Long
if marketposition = 0  
and
(
(PLTarget < PForDay) and (PLTarget > LForDay)
) 
//and
//(Time > 940.00 and Time < 1525.00) //Increase from 9:35 to filter noise at the open ("no trade zone") //2 
and
zscore < longminzscore 
and
close > open
and
close > close[1] //or (close [1] > close[2])) //B
and
close < vBlb1
and
close <= DonchianMid
and
close > emafast
and
Histogram > 0
and
close > high5

then 
Begin
buy Floor(buyingPower) Shares next bar at market  ;
End;


//Short
//Conditions Entry Short 
// CONDITIONS FOR OPEN SHORT POSITION 

if marketposition = 0  
and 
( 
(PLTarget < PForDay) and (PLTarget > LForDay)
)  
//and
//(Time > 940.00 and Time < 1525.00) //Increase from 9:35 to filter noise at the open("no trade zone") //2     
and
zscore > shortminzscore 
and
close < open
and
close < close[1] 
and 
((open[1] <= Close [1]) or (open [2] <= Close [2]) )
and
close > vBub1
and
close >= DonchianMid
and
close < emafast
and
Histogram < 0
and
close < low5

then 
Begin
sellshort Floor(buyingPower) Shares next bar at market;
End;

//End;


// START--  EXIT LONG BASE OF PRECENT -------------------------------------------------------


if 
marketposition = 1
then
[IntrabarOrderGeneration = True] //trade intra-bar - check every second and not 1 min
// false means check only for the close position 
//close long position with trail start moving after minimum profit 

if marketposition = 1 //there is long position open
and
(Close/entryprice-1)*100 >= SmallMinProfit 
and
barssinceentry <= 1 //  number of bars from begining . 
then 
begin
valuePercentTrail = ((entryprice * SmallTrailStop ) /100);
trailProfit = Highest(high , Barssinceentry); 
trailExit = trailProfit + valuePercentTrail; //          
sell next bar at trailExit  stop;
end;

// END - EXIT LONG BASE OF PRECENT -------------------------------------------------------




// START - EXIT LONG BASE ON CROSS PREVEVIOS LOW -------------------------------------------------------
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


// END - EXIT LONG BASE ON CROSS PREVEVIOS LOW -------------------------------------------------------
{
//close 2st long position with trail start moving cross back
if marketposition = 1 //there is long position open
and
(close/entryprice-1)*100 >= SmallbaseProfit1 
and
barssinceentry > 1
//and
//Close < longStop * (1-os1/100)
and
close cross below emaMid 
//and
//close > lastExitPrice 
Then
begin
Sell Next Bar at Market;
end;
}


// START--  EXIT SHORT BASE OF PRECENT -------------------------------------------------------

if marketposition = -1
then
[IntrabarOrderGeneration = True] //trade intra-bar



//close short position with trail start moving after minimum profit
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


// END--  EXIT SHORT BASE OF PRECENT -------------------------------------------------------

// START - EXIT SHORT BASE ON CROSS PREVEVIOS High -------------------------------------------------------


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
Close cross above shortStop * (1+os1/100)
Then
begin
buytocover Next Bar at Market;
end;




// END - EXIT SHORT BASE ON CROSS PREVEVIOS High -------------------------------------------------------


// START - Exit on first stop loss -------------------------------------------------------
{
if marketposition = -1
then
begin
SetStopLoss(shortSL);
end;
}

// END - Exit on first stop loss -------------------------------------------------------


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


