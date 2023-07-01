if marketposition = 0 //Conditions Entry Long
	and
	(
	(PLTarget < PForDay) and (PLTarget > LForDay) //1
	)  
	and
	(Time > 1500.00 and Time < 2200.00)
	and
	close > Open //3
	and
	close < vBlb2 //5
	and
	zscore <= longminzscore 
	and
	(
	(close cross above emaFast ) or (close[1] cross above emaFast [1] )
	)  //J
	and
	close > open [1]
	and
	close [1] <= open [1]
	then 
	begin
	buy longbuyingPower Shares next bar at market  ;
	end;

	if marketposition = 1 //Scale In - Conditions Add Entry Long
	and
	close > Open
	and
	close > open [1]
	and
	(
	(close [1] <= open [1]) or (close [2] <= open [2])
	)
	and 
	close cross above emaFast
	and
	(1-close/entryprice)*100 > MinLossForAdd 
	and
	CurShares < maxpositions 
	then 
	begin
	buy longbuyingPower1 Shares next bar at market  ;
	end;

	//close long position with trail start moving after small profit when entry price less then 200-2 deviation 
	if marketposition = 1 //there is long position open
	and
	(close/entryprice-1)*100 >= SmallMinProfit 
	then 
	begin
	valuePercentTrail = ((entryprice * SmallTrailStop) /100);
	trailProfit = Highest(high , Barssinceentry); 
	trailExit = trailProfit - valuePercentTrail;        
	sell  next bar at trailExit  stop;
	end;

	//SetProfitTarget;
	if marketposition = 1
	then
	begin
	SetStopLoss(longSL);
	end;
