
//PL for a day - CHECK IF PROFIT OR LOSS FOR THE DAY 
if DATE <> DATE[1] 
then 
begin
NetProf = NetProf + NetProfit - NetProf[1];
end;
PLTarget = Netprofit - NetProf;


// CONDITIONS FOR OPEN LONG POSITION 

//calc a switch for identify long or short (for the connection with VXX)
if symbol = "SOXS" or symbol = "LABD" or symbol = "SQQQ" then
is_long_symbol = False;

//Conditions Entry Long
if marketposition = 0  
and
(
(PLTarget < PForDay) and (PLTarget > LForDay)
) 
and
(Time > 940.00 and Time < 1525.00) //Increase from 9:35 to filter noise at the open ("no trade zone") //2 
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
then 
Begin
buy Floor(buyingPower) Shares next bar at market  ;
End;


//Short
//Conditions Entry Short 
// CONDITIONS FOR OPEN SHORT POSITION 

if marketposition = 0  and ( (PLTarget < PForDay) and (PLTarget > LForDay))  
and
(Time > 940.00 and Time < 1525.00) //Increase from 9:35 to filter noise at the open("no trade zone") //2     
and
zscore > shortminzscore 
and
close < open
and
close < close[1] 
and ((open[1] <= Close [1]) or (open [2] <= Close [2]) )
and
close > vBub1
and
close >= DonchianMid
and
close < emafast
and
Histogram < 0
then 
Begin
sellshort Floor(buyingPower) Shares next bar at market;
End;

End;


// START--  EXIT LONG BASE OF PRECENT -------------------------------------------------------


if marketposition = 1
then
[IntrabarOrderGeneration = True] //trade intra-bar - check every second and not 1 min
// false means check only for the close position 
//close long position with trail start moving after minimum profit 
if marketposition = 1 //there is long position open
and
(Close/entryprice-1)*100 >= SmallMinProfit 
and
barssinceentry <= 2 //  number of bars from begining . 
 
then 
begin
valuePercentTrail = ((entryprice * SmallTrailStop ) /100);
trailProfit = Highest(high , Barssinceentry); 
trailExit = trailProfit + valuePercentTrail; //          
sell next bar at trailExit  stop;
end;

// END - EXIT LONG BASE OF PRECENT -------------------------------------------------------




// START - EXIT LONG BASE ON CROSS PREVEVIOS LOW -------------------------------------------------------
//  initilias longStop
if marketposition = 0
then
begin
longStop = -9999999;
end;

if marketposition = 1 //there is long position open
and
(close/entryprice-1)*100 >= smallbaseProfit 
and 
barssinceentry > 2

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
(close/entryprice-1)*100 >= smallbaseProfit 
and
barssinceentry > 2
and
Close < longStop 
Then
begin
Sell Next Bar at Market;
end;

// END - EXIT LONG BASE ON CROSS PREVEVIOS LOW -------------------------------------------------------



// START--  EXIT SHORT BASE OF PRECENT -------------------------------------------------------

if marketposition = -1
then
[IntrabarOrderGeneration = True] //trade intra-bar


//close short position with trail start moving after minimum profit
if marketposition = -1 //there is long position open
and
(1-Close/entryprice)*100 >= SmallMinProfit 
and 
barssinceentry <= 2
then 
begin
valuePercentTrail = ((entryprice * SmallTrail) /100);
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
(1-Close/entryprice)*100 >= smallbaseProfit 
and
barssinceentry > 2
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
(1-Close/entryprice)*100 >= smallbaseProfit 
and
barssinceentry > 2
and
Close > shortStop 
Then
begin
buytocover Next Bar at Market;
end;

// END - EXIT SHORT BASE ON CROSS PREVEVIOS High -------------------------------------------------------


// START - Exit on first stop loss -------------------------------------------------------

if marketposition = -1
then
begin
SetStopLoss(shortSL);
end;

// END - Exit on first stop loss -------------------------------------------------------
