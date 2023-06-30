// START - PL for a day - CHECK IF PROFIT OR LOSS FOR THE DAY 
if DATE <> DATE[1] 
then begin
NetProf = NetProf + NetProfit - NetProf[1];
end;
PLTarget = Netprofit - NetProf;

// END - PL for a day - CHECK IF PROFIT OR LOSS FOR THE DAY 


// START -CONDITIONS FOR OPEN LONG POSITION 


//Conditions Entry Long
if marketposition = 0 
and( (PLTarget < PForDay) and (PLTarget > LForDay) ) 
and(Time > 940.00 and Time < 1525.00) //Increase from 9:35 to filter noise at the open ("no trade zone") //2 
and zscore < longminzscore 
and close > open
and close > maxlist (open [1], close [1], open [2], close [2], open [3], close [3])
and close < vBlb1
and close <= DonchianMid
and close > emafast
and Histogram > 0
then Begin
buy Floor(buyingPower) Shares next bar at market  ;
End;

// END -CONDITIONS FOR OPEN LONG POSITION 


//Conditions Entry Short 
// START -CONDITIONS FOR OPEN SHORT POSITION 

if marketposition = 0  and ( (PLTarget < PForDay) and (PLTarget > LForDay))  
and (Time > 940.00 and Time < 1525.00) //Increase from 9:35 to filter noise at the open("no trade zone") //2     
and zscore > shortminzscore 
and close < open
and close < minlist (open [1], close [1], open [2], close [2], open [3], close [3])
and ((open[1] <= Close [1]) or (open [2] <= Close [2]) )
and close > vBub1
and close >= DonchianMid
and close < emafast
and Histogram < 0
then Begin
sellshort Floor(buyingPower) Shares next bar at market;
End;



// END - CONDITIONS FOR OPEN SHORT POSITION 


// START--  EXIT LONG BASE OF PRECENT -------------------------------------------------------


if marketposition = 1
then
[IntrabarOrderGeneration = True] //trade intra-bar - check every second and not 1 min
// false means check only for the close position 
//close long position with trail start moving after minimum profit 
if marketposition = 1 //there is long position open
and (Close/entryprice-1)*100 >= SmallMinProfit 
and barssinceentry <= 1 //  number of bars from begining . 
 
then begin
valuePercentTrail = ((entryprice * SmallTrailStop ) /100);
trailProfit = Highest(high , Barssinceentry); 
trailExit = trailProfit + valuePercentTrail; //          
sell next bar at trailExit  stop;
end;

// END - EXIT LONG BASE OF PRECENT -------------------------------------------------------


// START - EXIT LONG BASE ON CROSS PREVEVIOS LOW -------------------------------------------------------
//  initilias longStop
if marketposition = 0
then begin
longStop = -9999999;
end;

if marketposition = 1 //there is long position open
and (close/entryprice-1)*100 >= smallbaseProfit 
and barssinceentry > 1

then begin
// Calculate the trailing stop price
if low [1] > longStop 
then begin
longStop = low[1];
end;
end;

//close long position with trail start moving aafter the first bar from entry
if marketposition = 1 //there is long position open
and (close/entryprice-1)*100 >= smallbaseProfit 
and barssinceentry > 1
and Close < longStop 
Then begin
Sell Next Bar at Market;
end;

// END - EXIT LONG BASE ON CROSS PREVEVIOS LOW -------------------------------------------------------



// START--  EXIT SHORT BASE OF PRECENT -------------------------------------------------------

if marketposition = -1
then
[IntrabarOrderGeneration = True] //trade intra-bar


//close short position with trail start moving after minimum profit
if marketposition = -1 //there is long position open 
and (1-Close/entryprice)*100 >= SmallMinProfit 
and barssinceentry <= 1
then begin
valuePercentTrail = ((entryprice * SmallTrail) /100);
trailProfit = Lowest(low , Barssinceentry); 
trailExit = trailProfit + valuePercentTrail; //          
buytocover next bar at trailExit  stop;
end;


// END--  EXIT SHORT BASE OF PRECENT -------------------------------------------------------

// START - EXIT SHORT BASE ON CROSS PREVEVIOS High -------------------------------------------------------


//close short position with trail start moving after the first bar from entry
if marketposition = 0
then begin
shortStop = 9999999;
end;

if marketposition = -1 //there is long position open
and (1-Close/entryprice)*100 >= smallbaseProfit 
and barssinceentry > 1
then begin
// Calculate the trailing stop price
if High[1] < shortStop 
then begin
shortStop = High[1];
end;
end;

//close short position with trail start moving aafter the first bar from entry
if marketposition = -1 //there is long position open
and (1-Close/entryprice)*100 >= smallbaseProfit 
and barssinceentry > 1
and Close > shortStop 
Then begin
buytocover Next Bar at Market;
end;

// END - EXIT SHORT BASE ON CROSS PREVEVIOS High -------------------------------------------------------


// START - Exit long on first stop loss -------------------------------------------------------

if marketposition = 1
then begin
SetStopLoss(longSL);
end;

// END - Exit on first stop loss -------------------------------------------------------

// START - Exit short on first stop loss -------------------------------------------------------

if marketposition = -1
then begin
SetStopLoss(shortSL);
end;

// END - Exit on first stop loss -------------------------------------------------------


