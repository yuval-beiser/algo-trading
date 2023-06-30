if marketposition = 0 //Conditions Entry Long
//and
//(
//(PLTarget < PForDay) and (PLTarget > LForDay) //1
//)  
//and
//(Time > 0700.00 and Time < 2200.00) //2
and
close > Open //3
//and
//(close-open) >(close[1]-open[1])* 1.3
and
close > high5 //5 open and close of 5 previus bars
and
close > high [1] //high previuos bar
and
close > emaMid //20
and
close > emaverySlow //200

//and
//emaMid >= emaverySlow * (1+Mingap/100) //from 10 
//and
//emaMid <= emaverySlow * (1+Maxgap/100) //till 10 
//and
//close <= emaverySlow * (1+Maxgap1/100) //till 8 


then 
begin
buy longbuyingPower Shares next bar at market  ;
end;



if         
marketposition = 0 //Conditions Entry short
and
//(
//(PLTarget < PForDay) and (PLTarget > LForDay) //1
//)  
//and
(Time > 0700.00 and Time < 2200.00) //1
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
//and
//emaMid <= emaverySlow * (1-Mingap/100) //till 10 
//and
//emaMid >= emaverySlow * (1-Maxgap/100) //till 10 
//and
//close >= emaverySlow * (1-Maxgap1/100) //till 8

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




//close long position 
if marketposition = 1 //there is long position open
and
close < close [1]
and
(close/entryprice-1)*100 >= SmallMinProfit 

then 
begin
sell next bar at market;
end;

//close long position 
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
if marketposition = -1 //there is long position open
and
close > close [1]
and
(1-Close/entryprice)*100 >= SmallMinProfit 
then 
begin
buytocover Next Bar at Market;
end;


//close short position 
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

