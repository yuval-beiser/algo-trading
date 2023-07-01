
if marketposition = 0 //Conditions Entry Long
and
(
(PLTarget < PForDay) and (PLTarget > LForDay) //1
)  
and
//(Time > 0700.00 and Time < 2200.00) 
close > Open //3
and
close > high5 //5 open and close of 5 previus bars
and
close > high [1] //high previuos bar
and
close > emaMid //20
and
close > emaverySlow //200
and
emaMid > emaverySlow 
//and
//(
//(close cross above emaFast) or (close[1] cross above  emaFast[1])
//)
//and
//emaMid >= emaverySlow * (1+Mingap/100) //from 10 
//and
//emaMid <= emaverySlow * (1+Maxgap/100) //till 10 
and
close <= emaverySlow * (1+Maxgap1/100) //till 8 
and 
(
(close cross above emaFast) or (close [1] cross above emaFast[1]) or  (close [2] cross above emaFast[2])
)
then 
begin
buy longbuyingPower Shares next bar at market  ;
end;


if         
marketposition = 0 //Conditions Entry short
and
(
(PLTarget < PForDay) and (PLTarget > LForDay) //1
)  
//and
//(Time > 0700.00 and Time < 2200.00) //1
and
close < Open //3
//and
//(close-open) >(close[1]-open[1])* 1.3
and
close < low5
and
close < low [1]
and
close < emaMid //20
and
close < emaverySlow //200
and
emaMid < emaverySlow 
//and
//(
//(close cross below emaFast) or (close[1] cross below emaFast[1])
//)

//and
//emaMid <= emaverySlow * (1-Mingap/100) //till 10 
//and
//emaMid >= emaverySlow * (1-Maxgap/100) //till 10 
and
close >= emaverySlow * (1-Maxgap1/100) //till 8
and
(
(close cross below emaFast) or (close [1] cross below emaFast[1]) or  (close [2] cross below emaFast[2])
)

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

//close long position with trail
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
end;

//close long position with cross previous low
if marketposition = 0
then
begin
longStop = -9999999;
end;

if marketposition = 1 //there is long position open
and
(close/entryprice-1)*100 >= smallbaseProfit 
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

if marketposition = 1 //there is long position open
and
(close/entryprice-1)*100 >= smallbaseProfit 
and
barssinceentry > 1
and
Close < longStop 
Then
begin
Sell Next Bar at Market;
end;

//close long position after 3 down
if marketposition = 1 //there is long position open
and
(
(close [1] <= open [1]) and (close [2] <= open [2]) and (close [3] <= open [3])
)
and
(close/entryprice-1)*100 >= SmallMinProfit 
then 
begin
sell next bar at market;
end;


//close short position
if marketposition = -1
then
[IntrabarOrderGeneration = True] //trade intra-bar


//close short position with trail start moving after minimum profit
if marketposition = -1 //there is long position open
and
(1-Close/entryprice)*100 >= SmallMinProfit 
and 
barssinceentry <= 1
then 
begin
valuePercentTrail = ((entryprice * SmallTrailStop ) /100);
trailProfit = Lowest(low , Barssinceentry); 
trailExit = trailProfit + valuePercentTrail; //          
buytocover next bar at trailExit  stop;
end;

//close short position with cross previous high
if marketposition = 0
then
begin
shortStop = 9999999;
end;

if marketposition = -1 //there is long position open
and
(1-Close/entryprice)*100 >= smallbaseProfit 
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

//close short position 
if marketposition = -1 //there is long position open
and
(1-Close/entryprice)*100 >= smallbaseProfit 
and
barssinceentry > 1
and
Close > shortStop 
Then
begin
buytocover Next Bar at Market;
end;


//close short position after 3 up
if marketposition = -1 //there is long position open
and
(
(close [1] >= open [1]) and (close [2] >= open [2]) and (close [3] >= open [3])
)
and
(1-Close/entryprice)*100 >= SmallMinProfit 
then 
begin
buytocover Next Bar at Market;
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

