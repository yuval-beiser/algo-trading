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
close < vBlb2
and
close <= DonchianMid
and
close cross above emaFast
and
Histogram > 0
and
close > high5

then 
Begin
buy longbuyingPower Shares next bar at market  ;
Alert("MNQ Reversal Model - Entry Long 3");
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
close > vBub2
and
close >= DonchianMid
and
close cross below emaFast
and
Histogram < 0
and
close < low5

then 
Begin
sellshort shortbuyingPower Shares next bar at market;
Alert("MNQ Reversal Model - Entry Short 3");
End;

//End;


// START--  EXIT LONG BASE OF PRECENT -------------------------------------------------------


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
Alert("MNQ Reversal Model - Exit Long");
end;


//close short position with trail (based on low prev) start moving after the first bar from entry
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
crossind1 = true;
Sell longbuyingPower1 Shares Next Bar at Market;
Alert("MNQ Reversal Model - Exit Long 1");
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
crossind2 = true;
Sell longbuyingPower1 Shares Next Bar at Market;
Alert("MNQ Reversal Model - Exit Long 1");
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
Sell Next Bar at Market;
crossind3 = true;
Alert("MNQ Reversal Model - Exit Long 1");
end;

//close long position with trail start moving after large profit 
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
(crossind1 = true) or (crossind2= true) or (crossind3= true)
)

//and
//close > lastExitPrice 
Then
begin
Sell Next Bar at Market;
Alert("MNQ Reversal Model - Exit Long");
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

//close short position with trail start moving after small profit in the first bar from entry
if marketposition = -1 //there is long position open
and
(1-close/entryprice)*100 >= SmallMinProfit 
and
barssinceentry <= 1
//and
//AngleLong = False
//entryprice >= vBlb2
then 
begin
valuePercentTrail = ((entryprice * SmallTrailStop) /100);
trailProfit = lowest(low , Barssinceentry); 
trailExit = trailProfit - valuePercentTrail;        
buytocover  next bar at trailExit  stop;
Alert("MNQ Reversal Model - Exit Short");
end;
// END--  EXIT SHORT BASE OF PRECENT -------------------------------------------------------

// START - EXIT SHORT BASE ON CROSS PREVEVIOS High -------------------------------------------------------
//close short position with trail (based on low prev) start moving after the first bar from entry
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
crossind1 = true;
buytocover shortbuyingPower1 Shares Next Bar at Market;
Alert("MNQ Reversal Model - Exit Short 1");
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
crossind2 = true;
buytocover shortbuyingPower1 Shares Next Bar at Market;
Alert("MNQ Reversal Model - Exit Short 1");
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
Alert("MNQ Reversal Model - Exit Short 1");
end;

//close short position with trail start moving after large profit 
if marketposition = -1 //there is long position open
and
(1-close/entryprice)*100 >= largeMinProfit 
//and
//barssinceentry <= 1
//and
//AngleLong = False
//entryprice >= vBlb2
then 
begin
valuePercentTrail = ((entryprice * largeTrail) /100);
trailProfit = lowest(low , Barssinceentry); 
trailExit = trailProfit - valuePercentTrail;        
buytocover  next bar at trailExit  stop;
Alert("MNQ Reversal Model - Exit Short");
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
(crossind1 = true) or (crossind2= true) or  (crossind3= true)
)
//and
//close > lastExitPrice 
Then
begin
buytocover Next Bar at Market;
Alert("MNQ Reversal Model - Exit Short");

end;

//SetProfitTarget;
if marketposition = 1
then
begin
SetStopLoss(close*AssetMultiplier *maximumloss/100*longbuyingPower );
end;


if marketposition = -1
then
begin
SetStopLoss(close*AssetMultiplier *maximumloss/100*shortbuyingPower );
end;

