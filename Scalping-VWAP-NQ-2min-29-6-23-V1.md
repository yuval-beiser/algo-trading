if marketposition = 0 //Conditions Entry Long
//and
//(
//(PLTarget < PForDay) and (PLTarget > LForDay) //1
//)  
and
(Time > 0700.00 and Time < 2200.00) //2
and
close > Open //3
and

////there is a support and check that there is a touch or cross of lower band 
(

(
vBlbVwap6 >= low 
and 
vBlbVwap6 <= minlist (close [1] , open [1], close [2], open [2])
)

or

(
vBlbVwap5  >= low 
and
vBlbVwap5 <= minlist (close [1] , open [1], close [2], open [2])
)

or

(
vBlbVwap4  >= low 
and
vBlbVwap4 <= minlist (close [1] , open [1], close [2], open [2])
)

or

(
vBlbVwap3  >= low 
and
vBlbVwap3 <= minlist (close [1] , open [1], close [2], open [2])
)

or

(
vBlbVwap2  >= low 
and
vBlbVwap2 <= minlist (close [1] , open [1], close [2], open [2])
)

or

(
vBlbVwap1  >= low 
and
vBlbVwap1 <= minlist (close [1] , open [1], close [2], open [2])
)

or

(
vBubVwap1  >= low
and
vBubVwap1 <= minlist (close [1] , open [1], close [2], open [2])
)

or

(
vBubVwap2  >=  low 
and
vBubVwap2 <= minlist (close [1] , open [1], close [2], open [2])
)

or

(
vBubVwap3  >=  low 
and
vBubVwap3 <= minlist (close [1] , open [1], close [2], open [2])
)

or

(
vBubVwap4  >= low 
and
vBubVwap4 <= minlist (close [1] , open [1], close [2], open [2])
)

or

(
vBubVwap5  >= low 
and
vBubVwap5 <= minlist (close [1] , open [1], close [2], open [2])
)

or

(
vBubVwap6  >= low 
and
vBubVwap6 <= minlist (close [1] , open [1], close [2], open [2])
)

)


and
close > maxlist(close [1] , open [1], close [2], open [2])
and
(
(close [1] <= open [2]) or (close [2] <= open [2])
)
and
close > high [1]
and
close < low * (1+maxgap/100)
and
close > emaFast
and
close > EHLOCqtr1band

//and
//close < vBub3

//and
//vBubVwap2 > vBubVwap1 * (1+MingapVwapVb/100)

//and
//(close-open) >(close[1]-open[1])* 1.3
//and
//close > high5
//and
//close > high [1]
{
and
(
open [1] > emaverySlow and open [2] > emaverySlow 
and
Close [1] > emaverySlow and Close [2] > emaverySlow 
)
}
//and
//open > emaMid //20
//and
//open > emaverySlow //20
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
and
////there is a ressitance and check that there is a touch or cross of higher band 
(
(
vBlbVwap6  <= high
and
vBlbVwap6  >= maxlist (close [1] , open [1], close [2], open [2])
)
or
(
vBlbVwap5  <= high
and
vBlbVwap5  >= maxlist (close [1] , open [1], close [2], open [2])
)
or
(
vBlbVwap4  <= high 
and
vBlbVwap4  >= maxlist (close [1] , open [1], close [2], open [2])
)
or
(
vBlbVwap3  <= high 
and
vBlbVwap3  >= maxlist (close [1] , open [1], close [2], open [2])
)
or
(
vBlbVwap2  <= high
and
vBlbVwap2  >= maxlist (close [1] , open [1], close [2], open [2])
)
or
(
vBlbVwap1  <= high 
and
vBlbVwap1  >= maxlist (close [1] , open [1], close [2], open [2])
)
or
(
vBubVwap1  <= high 
and
vBubVwap1  >= maxlist (close [1] , open [1], close [2], open [2])
)
or
(
vBubVwap2  <= high 
and
vBubVwap2  >= maxlist (close [1] , open [1], close [2], open [2])
)
or
(
vBubVwap3  <= high 
and
vBubVwap3  >= maxlist (close [1] , open [1], close [2], open [2])
)
or
(
vBubVwap4   <= high 
and
vBubVwap4  >= maxlist (close [1] , open [1], close [2], open [2])
)
or
(
vBubVwap5  <= high 
and
vBubVwap5  >= maxlist (close [1] , open [1], close [2], open [2])
)
or
(
vBubVwap6  <= high 
and
vBubVwap6  >= maxlist (close [1] , open [1], close [2], open [2])
)
)

and
close < minlist (close [1] , open [1], close [2], open [2])
and
(
(close [1] >= open [2]) or (close [2] >= open [2])
)
and
close < low [1]
and
close > high * (1-maxgap/100)
and
close < emaFast
//and
//vBubVwap2 > vBubVwap1 * (1+MingapVwapVb/100)
//and
//close > vBlb3
and
close > EHLOCqtr3band
then 
begin
sellshort shortbuyingPower Shares next bar at market  ;
end;

//close long position with trail start moving after small profit in the first bar from entry
if marketposition = 1 //there is long position open
and
(close/entryprice-1)*100 >= SmallMinProfit 
//and
//barssinceentry < 5
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

//close long position with trail start moving after small profit in the first bar from entry
if marketposition = 1 //there is long position open
and
(close/entryprice-1)*100 >= SmallMinProfit 
//and
//barssinceentry < 5
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

//take profit for a short position with trail start moving in the first bar from entry
if marketposition = -1 //there is short position open
and
(1-Close/entryprice)*100 >= SmallMinProfit 
//and
//barssinceentry < 5
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
