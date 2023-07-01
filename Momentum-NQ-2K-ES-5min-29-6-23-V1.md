if marketposition = 0 //Conditions Entry Long
and
(
(PLTarget < PForDay) and (PLTarget > LForDay) //1
)  
and
close > Open //3
and
close > open [1] //4
and
close < vBub3 //5
//and
//close <= LowD(0) *(1+MaxFromLH/100) //entry near to low of the day 
//and
//close > high [1]//2
and
close <= low *(1+MaxFromLH/100) //6
and
close >= DonchianUp
and
close cross above EHLOCupband //2
and
close of data2  cross above EHLOCupband2 
and
close of data3 cross above EHLOCupband3 
and
zscore <= longminzscore 
and
Zscore2 <= longminzscore
and
Histogram > 0 
then 
begin
buy buyingPower Shares next bar at market  ;
end;

if         
marketposition = 0 //Conditions Entry short
and
(
(PLTarget < PForDay) and (PLTarget > LForDay) //1
)  //1
and
close < Open //3
and
close < open [1] //4
and
close > vBlb3 //5
and
close >= high *(1-MaxFromLH/100) //6\
And
Close <=DonchianDown
and
close cross below EHLOCdownband //2
and
close of data2 cross below EHLOCdownband2 //2
and
close of data3 cross below EHLOCdownband3 //2
and
zscore >= shortminzscore 
and
zscore2 >= shortminzscore 
and
Histogram < 0 
then 
begin
sellshort buyingPower Shares next bar at market  ;
end;


//close long position with trail start moving after small profit when entry price less then 200-2 deviation 
if marketposition = 1 //there is long position open
and
(close/entryprice-1)*100 >= SmallMinProfit 
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

//take profit for a short position with trail start moving after small profit when entry price less then 200-2 deviation 
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

//take profit when zscore reach target
if marketposition = 1 //there is long position open
and
Zscore >= 0
then 
begin        
sell next bar at market;
end;

//take profit when zscore reach target
if marketposition = -1 //there is long position open
and
Zscore <= 0
then 
begin        
buytocover next bar at market;
end;

//SetProfitTarget(2000);
SetStopLoss(SL); //5 PIPS
