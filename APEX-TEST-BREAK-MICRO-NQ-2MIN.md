
	if marketposition = 0 //Conditions Entry Long
	//and
	//(
	//(PLTarget < PForDay) and (PLTarget > LForDay) //1
	//)  
	//and
	//(
	//(Time > 0000.00) and (Time < 1800.00) //long time
      //)
	and
	close > Open //3
	and
	close > close [1]
	and
	close > high5 * (1+os4 /100)
	//and
	//Histogram > 0
	and
	Histogram > Histogram [1]
	and
	MACDLine < 0
	and
	SignalLine < 0 
	and
	close < emaFast *(1+maxgap6/100)
	and
	close < low * (1+maxgap7/100)
	and
	close cross above emaFast
	and
	(
	(close[1] < EHLOCdownband) or (close[2] < EHLOCdownband) or (close[3] < EHLOCdownband) or (close[4] < EHLOCdownband)
	)
	//and
	//(
	//(close[1] < vBlbHLOC ) or (close[2] < vBlbHLOC ) or (close[3] < vBlbHLOC ) or (close[4] < vBlbHLOC )
	//)
	
	and
	atr > 6
	
	//and
	//close > vBub1
	//and
	//close < vBub2
	//and
	//close > high26
	//and
	//close > EHLOCqtr3band
	//and
	//BullAngle and AngleLong
	//and
	//(close-open) >(close[1]-open[1])* 1.3
	//*and
	//*close > high9
	
	//and
	//low5 < emaVerySlow *
	//and
	//close > maxlist (close [1], open [1]) //high

	{
	and
	(
	open [1] > emaverySlow and open [2] > emaverySlow 
	and
	Close [1] > emaverySlow and Close [2] > emaverySlow 
	)
	}
	//and
	//(
	//(close cross above emaFast) or (close cross above emaMid) or (close cross above emaVerySlow) //20
	//)
	//*and
	//close > emaverySlow * (1 + os3 /100)  //200

	//and
	//emaMid cross above emaVerySlow

	//and
	//emaMid >= emaverySlow * (1+Mingap/100) //from 10 
	//*and
	//emaMid <= emaverySlow * (1+Maxgap/100) //*
	//*and 
	//close <= emaverySlow * (1+Maxgap1/100) //*
	//and
	//emaMid > emaVerySlow
	//*and 
	//atr < Atrmax
	//and
	//atr > Atrmin

	//and
	//close > lowD (0) * (1+Mingap/100)
	//and
	//DonchianDown > DonchianUp * (1-maxgap5/100)
	//and
	//DonchianDown < DonchianUp * (1-mingap2/100)




	//and
	//close < low5 * (1+maxgap4/100) *
	//and
	//close <= low * (1+maxgap3/100) *
	//and
	//close of data2 > ema2Fast
	//and
	//close of data2 > ema2mid 
	//and
	//Mom >= 0
	//and
	//low < low [1]

	//and
	//close cross above emaFast

	//and
	//close >= emaMid * (1+Mingap1/100) //till 8 
	//and
	//close <= emaMid * (1+Maxgap2/100) //till 8 

	//and
	//(
	//(close cross above emaFast) or (close [1] cross above emaFast[1]) or  (close [2] cross above emaFast[2])
	//)
	//and
	//(
	//(close [1] < open [1]) or (close [2] < open [2])
	//)
		//and
	//VMFI > VMFI [1]
	//and
	//close cross above emaFast
	
	//and
	//emaFast < emamid
	//and 
	//MACDGradient > 0 
	//and
	
	{
(
stochData1 = 1  //5
and
oData1FastK > oData1SlowD 
//and
//oData1FastK > StochOverSold 
//and
//oData1FastK > StochOverSold
and  
(
(oData1FastK [1] < oData1SlowD [1]) or (oData1FastK [2] < oData1SlowD [2]) or (oData1FastK [3] < oData1SlowD [3])
) 
and
(
(oData1FastK [1] < StochOverSold) or (oData1FastK [2] < StochOverSold) or (oData1FastK [3] < StochOverSold) 
)
)
}

	then 
	begin
	buy longbuyingPower Shares next bar at market  ;

	end;


	{
	if marketposition = 1 //Scale In  - Conditions Add Entry long
	and
	close > open
	//and
	//close [1] <= open [1]

	//close > high [1]
	//high5 < emaVerySlow
	and
	close cross above EHLOCupband
	and
	close cross above high9
	//and
	//close > emaVerySlow
	//and
	//close cross above emaFast
	//and
	//close >= DonchianUp
	//and
	//Histogram > 0
	//and
	//close cross above emaFast

	//and
	//close > emaMid
	//and
	//high5 < emaMid
	//and
	//low < low [1]
	//and
	//close < open [1]
	//and
	//close[1] >= open[1]
	//and
	//close < emaFast
	//and
	//(Close/entryprice-1)*100 > MinProfitforadd 
	//and
	//(1-close/entryprice)*100 > 0
	//and
	//barssinceentry > 20
	and
	CurShares < maxpositions 
	then 
	begin
	buy longbuyingPower1 Shares next bar at market  ;
	end;

	}

	{
	if marketposition = 1 //Scale In x3 - Conditions Add Entry long
	//and
	//close > emaMid
	and
	high5 < emaMid
	and
	close [1] <= open [1]
	and
	low < low [1]
	and
	close cross above emaMid
	and
	close cross above emaVerySlow
	//and
	//close < open [1]
	//and
	//close[1] >= open[1]
	//and
	//close < emaFast
	//and
	//(Close/entryprice-1)*100 > MinProfitforadd 
	//and
	//(1-close/entryprice)*100 > 0
	//and
	//barssinceentry > 20
	and
	CurShares < maxpositions 
	then 
	begin
	buy longbuyingPower2 Shares next bar at market  ;
	end;
	}

	
	if         
	marketposition = 0 //Conditions Entry short
	//and
	//(
	//(PLTarget < PForDay) and (PLTarget > LForDay) //1
	//)  
	//and
	//(
	//(Time < 600.00) and (Time > 2200.00) //short time
	//)
	and
	close < Open //3
	and
	close < close [1]
	and
	close < low5 * (1+os4 /100)
	//and
	//Histogram < 0
	and
	Histogram < Histogram [1]
	and
	MACDLine > 0
	and
	SignalLine > 0 
	and
	close > emaFast *(1-maxgap6/100)
	and
	close > high * (1-maxgap7/100)
	and
	close cross below emaFast

	and
	(
	(close[1] > EHLOCupband) or (close[2] > EHLOCupband) or (close[3] > EHLOCupband) or (close[4] > EHLOCupband)
	)
	//and
	//(
	//(close[1] > vBubHLOC ) or (close[2] > vBubHLOC ) or (close[3] > vBubHLOC ) or (close[4] > vBubHLOC )
	//)
	
	

	and
	atr > 6
	


	//and
	//close < vBlb1
	//and
	//close > vBlb2
	//and
	//close < low26

	//and
	//close < EHLOCqtr1band

	//and
	//BearAngle and AngleShort

	//and
	//(close-open) >(close[1]-open[1])* 1.3
	//*and
	//close < low9

	
	//and
	//high5 > emaVerySlow
	//and
	//close < minlist (close [1], open [1]) //low
	//*and
	//close < emaverySlow * (1 - os3 /100)  

	//and
	//emaMid cross above emaVerySlow

	//and
	//emaMid >= emaverySlow * (1+Mingap/100) //from 10 
	//*and
	//emaMid >= emaverySlow * (1-Maxgap/100) //*
	//*and 
	//close >= emaverySlow * (1-Maxgap1/100) //*
	//and
	//emaMid > emaVerySlow
	//and 
	//emaMid >= emaverySlow * (1-Maxgap/100) //*
	//*and 
	//atr < Atrmax
	//and
	//atr > Atrmin

	//and
	//close < highD (0) * (1-Mingap/100)
	//*and
	//DonchianDown > DonchianUp * (1-maxgap5/100)
	//and
	//DonchianDown > DonchianUp * (1-maxgap5/100)
	//*and
	//DonchianDown < DonchianUp * (1-mingap2/100)


	//and
	//close [1] >= EHLOCupband

	
	//and
	
	{
(
stochData1 = 1 //F
and
oData1FastK < oData1SlowD 
//and
//oData1FastK < StochOverBot 
//and
//oData1FastK < StochOverBot
and  
(
(oData1FastK [1] > oData1SlowD [1]) or (oData1FastK [2] > oData1SlowD [2]) or (oData1FastK [3] > oData1SlowD [3])
)  
and
(
(oData1FastK [1] > StochOverBot) or (oData1FastK [2] > StochOverBot) or(oData1FastK [3] > StochOverBot) 
)
)
}

	//close < highD (0) * (1-Mingap/100)

	//and
	//and
	//emaMid < emaVerySlow
	//and
	//emaMid <= emaverySlow * (1-Mingap/100) //till 10 
	//and
	//emaMid >= emaverySlow * (1-Maxgap/100) //till 10 
	//and
	//close >= emaverySlow * (1-Maxgap1/100) //till 8
	//and
	//close > high5 * (1-maxgap4/100)
	//and
	//close of data2 < ema2mid 
	//and
	//close >= high *(1-maxgap3/100) 
	//and
	//Mom <= 0

	//and
	//high > high [1]

	//and
	//close <= emaMid * (1-Mingap1/100) //till 8 
	//and
	//close >= emaMid * (1-Maxgap2/100) //till 8 
	//and
	//close cross below emaFast
	//and
	//
	//(close cross below emaFast) or (close [1] cross below emaFast[1]) or  (close [2] cross below emaFast[2])
	//)

	//and
	//
	//(
	//(close [1] >  open [1]) or (close [2] >  open [2])
	//)

	//and
	//VMFI < VMFI [1]
	//*and
	//close cross below emaFast
	//*and
	//emaFast > emamid



	then 
	begin
	sellshort shortbuyingPower Shares next bar at market  ;
	end;
	

	{
	if marketposition = -1 //Scale In  - Conditions Add Entry Short
	and
	close < Open
	//and
	//close [1] >= open [1]

	//and
	//close < low [1]
	//and
	//close < emaMid
	//and
	//low5 > emaVerySlow
	and
	close cross below EHLOCdownband
	//and
	//close cross below emaFast
	and
	close cross below low9
	and
	close < emaVerySlow


	//and
	//Histogram < 0
	//and
	//close cross below emaFast


	//and
	//close < open [1]
	//and
	//close[1] >= open[1]
	//and
	//close < emaFast
	//and
	//(1-Close/entryprice)*100 > MinProfitforadd 
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
	if marketposition = -1 //Scale In x3 - Conditions Add Entry short
	//and
	//close > emaMid
	and
	low5 > emaMid
	and
	close [1] >= open [1]
	and
	high > high [1]
	and
	close cross below emaMid
	and
	close cross below emaVerySlow
	//and
	//close < open [1]
	//and
	//close[1] >= open[1]
	//and
	//close < emaFast
	//and
	//(Close/entryprice-1)*100 > MinProfitforadd 
	//and
	//(1-close/entryprice)*100 > 0
	//and
	//barssinceentry > 20
	and
	CurShares < maxpositions 
	then 
	begin
	sellshort shortbuyingPower2 Shares next bar at market  ;
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


//close long position with trail start moving after small profit in the first bar from entry
if marketposition = 1 //there is long position open
and
(close/entryprice-1)*100 >= SmallMinProfit 
//and
//barssinceentry <= 5
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
Close < longStop //* (1-os1/100)
Then
begin
Sell longbuyingPower1 Shares Next Bar at Market;
//crossind1 = true;
end;

{
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
Sell longbuyingPower1 Shares Next Bar at Market;
crossind2 = true;
end;
}
	

	{
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
Sell longbuyingPower Shares Next Bar at Market;
crossind3 = true;
end;
}

{
//close long position with trail start moving after large profit in the first bar from entry
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
}

//reset cross ind after fake move
if marketposition = 1 //there is long position open
and
(close/entryprice-1)*100 >= smallbaseProfit1 
and
barssinceentry < 5
//and
//Close < longStop //* (1-os1/100)
Then
begin
crossind1 = true;
end;

	
//close long position after cross 1 and go break even
if marketposition = 1 //there is long position open
and
close < (entryprice * 1.000067)
and
barssinceentry < 5
//and
//Close < longStop * (1-os1/100)
and
crossind1 = true
//and
//close > lastExitPrice 
Then
begin
Sell Next Bar at Market;

end;


	{
	//close long position when cross 200 after more then 10 bars
	if marketposition = 1 //there is long position open
	and
	(close/entryprice-1)*100 >= SmallbaseProfit 
	and
	barssinceentry > 20
	//and
	//Close < longStop * (1-os1/100)
	and
	close cross below emaVerySlow 
	//and
	//close > lastExitPrice 
	Then
	begin
	Sell Next Bar at Market;
	end;
	}

	{
	//close long position when cross above ema200
	if marketposition = 1 //there is long position open
	//and
	//(close/entryprice-1)*100 >= SmallbaseProfit 
	and
	close cross below emaVerySlow
	Then
	begin
	Sell Next Bar at Market;
	end;
	}

	{
	//close 2 out long position after cross with stop
	if marketposition = 1 //there is long position open
	and
	CurShares = longbuyingPower1 
	and
	barssinceentry > 1
	Then
	begin
	Sell longbuyingPower1 Shares Next Bar at (entryprice + Close)/2  stop;
	end;
	}

	{
	//close 2 out long position after cross with trail
	if marketposition = 1 //there is long position open
	and
	(close/entryprice-1)*100 >= SmallbaseProfit 
	and
	CurShares = longbuyingPower1 
	and
	barssinceentry > 1
	and
	Close < longStop * (1-os1/100)
	and
	close > lastExitPrice 
	Then
	begin
	Sell longbuyingPower1 Shares Next Bar at Market;
	end;
	}




	{
	//close long position when cross below min of 5 open-close
	if marketposition = 1 //there is long position open
	and
	Close < low5 
	Then
	begin
	Sell Next Bar at Market;
	end;
	}

	{
	//close long position when there is 3 bars short
	if marketposition = 1 //there is long position open
	and
	(
	(close <= open ) and (close [1] <= open [1]) and (close [2] <= open [2])
	)
	Then
	begin
	Sell Next Bar at Market;
	end;
	}

	{
	//close long position when there is 20 dolar profit
	if marketposition = 1 //there is long position open
	and
	(close/entryprice-1)*100 >= SmallMinProfit1 
	Then
	begin
	Sell Next Bar at Market;
	end;
	}

	{
	//close long position when cross below ema 200
	if marketposition = 1 //there is long position open
	and
	close cross below emaVerySlow
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

// START--  EXIT SHORT BASE OF PRECENT -------------------------------------------------------

if marketposition = -1
then
[IntrabarOrderGeneration = True] //trade intra-bar


//close short position with trail start moving after small profit in the first bar from entry
if marketposition = -1 //there is long position open
and
(1-close/entryprice)*100 >= SmallMinProfit 
//and
//barssinceentry <= 5
//and
//AngleLong = False
//entryprice >= vBlb2
then 
begin
valuePercentTrail = ((entryprice * SmallTrailStop) /100);
trailProfit = lowest(low , Barssinceentry); 
trailExit = trailProfit - valuePercentTrail;        
buytocover  next bar at trailExit  stop;
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
Close > shortStop //* (1+os1/100)
Then
begin
buytocover shortbuyingPower1 Shares Next Bar at Market;
//crossind1 = true;
end;

{
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
buytocover shortbuyingPower1 Shares Next Bar at Market;
crossind2 = true;
end;
}
	

{	
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
end;
}

{
//close short position with trail start moving after large profit in the first bar from entry
if marketposition = -1 //there is long position open
and
(1-close/entryprice)*100 >= largeMinProfit 
//and
//barssinceentry <= 2
//and
//AngleLong = False
//entryprice >= vBlb2
then 
begin
valuePercentTrail = ((entryprice * largeTrail) /100);
trailProfit = lowest(low , Barssinceentry); 
trailExit = trailProfit - valuePercentTrail;        
buytocover  next bar at trailExit  stop;
end;
}

//reset cross ind after fake move
if marketposition = -1 //there is long position open
and
(1-close/entryprice)*100 >= smallbaseProfit1 
and
barssinceentry < 5
//and
//Close < longStop //* (1-os1/100)
Then
begin
crossind1 = true;
end;

	
//close long position after cross 1 and go break even
if marketposition = -1//there is long position open
and
close > entryprice * 0.999933
and
barssinceentry < 5
//and
//Close < longStop * (1-os1/100)
and
crossind1 = True
//and
//close > lastExitPrice 
Then
begin
buytocover Next Bar at Market;
end;


	{
	//close 2st long position with trail start moving cross back
	if marketposition = -1 //there is long position open
	and
	(1-Close/entryprice)*100 >= SmallbaseProfit1 
	and
	barssinceentry > 1
	//and
	//Close < longStop * (1-os1/100)
	and
	close cross above emaFast 
	//and
	//close > lastExitPrice 
	Then
	begin
	buytocover Next Bar at Market;
	end;
	}

	{
	//close short position when cross above ema200
	if marketposition = -1 //there is long position open
	and
	Close cross above emaVerySlow * (1+os2/100)
	Then
	begin
	buytocover Next Bar at Market;
	end;
	}

	{
	//close short position when cross above min of 5 open-close
	if marketposition = -1 //there is long position open
	and
	Close > high5 
	Then
	begin
	buytocover Next Bar at Market;
	end;
	}

	{
	//close short position when there is 20 dolar profit
	if marketposition = -1 //there is long position open
	and
	(1-Close/entryprice)*100 >= SmallMinProfit1 
	Then
	begin
	buytocover Next Bar at Market;
	end;
	}

	{
	//close short position when cross above ema 200
	if marketposition = -1 //there is long position open
	and
	close cross above emaVerySlow
	Then
	begin
	buytocover Next Bar at Market;
	end;
	}

	{
	//close short position when there is 3 bars long
	if marketposition = -1 //there is long position open
	and
	(
	(close >= open ) and (close [1] >= open [1]) and (close [2] >= open [2])
	)
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

	//close short position at the EOD
	if marketposition = 1
	and Time = 2300.00 
	then
	begin
	sell next bar at market;
	end;
	}

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

