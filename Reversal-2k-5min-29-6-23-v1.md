
        if marketposition = 0 //Conditions Entry Long
        and
        (
        (PLTarget < PForDay) and (PLTarget > LForDay) //1
        )  
        and
        (Time > 1500.00 and Time < 2200.00)
        and
        close > Open //3
        //and
        //close > open [1] 
        //and
        //close [1] < open [1]
        and
        close < vBlb2 //5
        //and
        //close <= LowD(0) *(1+MaxFromLH/100) //entry near to low of the day 
        //and
        //close > high [1]//2
        //and
        //close <= low *(1+MaxFromLH/100) //6
        //and
        //close >= DonchianUp
        //and
        //close cross above EHLOCupband //2
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
        //pullback
        //(
        //(close [1] <= open [1]) or (close [2] <= open [2])
        //)

        //and
        //triger
        //(
        //(close [3] cross above emaFast [3]) or
        //(close [4] cross above emaFast [4]) or
        //(close [5] cross above emaFast [5]) 
        //(close [6] cross above emaFast [6]) or
        //(close [7] cross above emaFast [7]) 
        //)   


        //and
        //check the price in the choppy zone
        //(low[1] >= evBlb2 and low[2] >= evBlb2)
        //and
        //Close < vBub3 //3
        //and
        //Close < vBub2 //3

        //and
        //close > vwap //2
        //and
        //check channel IS not too tight
        //(vBub2/vBlb2 -1)*100 > Mingap //4
        //and
        //atr > AtrMin //5
        //and
        //atr < Atrmax //6
        //and
        //close [1] < (EHLOCupband+EHLOCdownband)/2 //4
        //and
        //check the price fell to bottom before the pull back in 1-2-3 pre candles
        //(
        //(close [1] cross below EHLOCdownband [1]) or //3
        //(close [2] cross below EHLOCdownband [2]) 
        //)

        //check there is a significant pull back
        //and
        //close > (high[1]+low[1])/2 //4


        //and
        //(
        //stochData1 = 1  //7
        //and
        //oData1FastK > oData1SlowD 
        //and
        //oData1FastK > StochOverSold 
        //and
        //oData1FastK < stochmid
        //and  
        //((oData1FastK [1] < oData1SlowD [1]) or (oData1FastK [2] < oData1SlowD [2])) 
        //and 
        //(
        //(oData1FastK [1] < StochOverSold) or (oData1FastK [2] < StochOverSold) or (oData1FastK [3] < StochOverSold) 
        //)



        //and
        //Close < (EHLOCupband+EHLOCdownband)/Hlocpartlong //7
        //and
        //close [1] < (EHLOCupband+EHLOCdownband)/2
        //and
        //close [1] < EHLOCdownband 
        //and
        //atr > AtrMin //3
        //and
        //absvalue(vBubHLOC - vBlbHLOC) >= MinChanel //3
        //and
        //absvalue(vBubHLOC - vBlbHLOC) <= MaxChanel //4
        //and
        //Ticks > vAvgTicks * (1+volumeUP/100)
        //and
        //AngleLong
        //and
        //BullAngle
        //and
        //close > vwap
        //and
        //close < vKeltUp   //4
        //and
        //vRSI < RSIOverbot //4
        //and
        //close >= emaFast * (1+MinEMAGap/100)//5
        //and
        //close of data2 below emaFast [1] //6
        //and
        //close cross above emaFast //7
        //and
        //close cross above EHLOCupband //8
        //and
        //close  cross above LTBreak
        //and
        //close cross above KUpperBand

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


        {
        //buy more after fast minimum profit
        if marketposition = 1 //there is long position open
        and
        (close/entryprice-1)*100 >= SmallMinProfitforadd 
        and
        barssinceentry < MaxBarsforadd
        and
        MarketPosition_at_Broker < maxpositions 
        //and
        //AngleLong = False
        //entryprice >= vBlb2
        then 
        begin
        buy buyingPower Shares next bar at market  ;
        end;
        }

        {
        if marketposition = 1 //add for Long position
        and
        (1-Close/entryprice)*100 >= SmallMinProfitforadd 
        then 
        begin
        buy buyingPower Shares next bar at market  ;
        end;
        }

        {
        if         
        marketposition = 0 //Conditions Entry short
        and
        (
        (PLTarget < PForDay) and (PLTarget > LForDay) //1
        )  //1
        and
        close < Open //3
        //and
        //close < open [1] //4
        //and
        //close [1] > open [1]
        and
        close > vBub2 //5
        and 

        (
        (close cross below emaFast) or (close[1] cross below emaFast [1])
        )  //J
        and
        close < open [1]
        and
        close [1] >= open [1]


        //pullback
        //(
        //(close [1] >= open [1]) or (close [2] >= open [2])
        //)

        //and
        //triger
        //(
        //(close [3] cross below emaFast [3]) or
        //(close [4] cross below emaFast [4]) or
        //(close [5] cross below emaFast [5]) 
        //(close [6] cross below emaFast [6]) or
        //(close [7] cross below emaFast [7])
        //)

        //and
        //close >= high *(1-MaxFromLH/100) //6\
        //And
        //Close <=DonchianDown
        //and
        //close cross below EHLOCdownband //2
        and
        zscore >= shortminzscore 


        //and
        //close >= HighD(0)* (1-MaxFromLH/100)  //entry near to high of the day 
        //and
        //close < Low [1]//2
        //close < Open //2

        //and
        //check the price in the choppy zone
        //(High[1] <= evBub2 and High[2] <= evBub2)
        //and
        //Close > vBlb3 //3
        //and
        //Close > vBlb2 //3
        //and
        //close < vwap //6
        //and
        //check channel is not too tight
        //(vBub2/vBlb2 -1)*100 > Mingap //4
        //and
        //atr > AtrMin //5
        //and
        //atr < Atrmax //6
        //and
        //check the price jump to top before the pull back in 1-2-3 pre candles
        //(
        //(close [1] cross above EHLOCupband [1]) or  //3
        //(close [2] cross above EHLOCupband [2]) 
        //)
        //check there is a significant pull back
        //and
        //close < open [1]
        //and
        //close < (high[1]+low[1])/2 //4

        //and
        //(
        //stochData1 = 1 //7
        //and
        //oData1FastK < oData1SlowD 
        //and
        //oData1FastK < StochOverBot 
        //and
        //oData1FastK > stochmid
        //and  
        //((oData1FastK [1] > oData1SlowD [1]) or (oData1FastK [2] > oData1SlowD [2])) 
        //and
        //(
        //(oData1FastK [1] > StochOverBot) or (oData1FastK [2] > StochOverBot) or (oData1FastK [3] > StochOverBot)
        //)
        //and
        //Close > (EHLOCupband+EHLOCdownband)/Hlocpartshort  //7
        //and
        //close [1] > (EHLOCupband+EHLOCdownband)/2
        //and
        //close [1] > EHLOCdownband 
        //and
        //atr > AtrMin //2
        //and
        //absvalue(vBubHLOC - vBlbHLOC) >= MinChanel //3
        //and
        //absvalue(vBubHLOC - vBlbHLOC) <= MaxChanel //4
        //and
        //Ticks > vAvgTicks * (1+volumeUP/100)
        //and
        //AngleShort 
        //and
        //close < vwap
        //and
        //close > vKeltDown   //4
        //and
        //BearAngle 
        //and
        //AngleShort 
        //and
        //vRSI > RSIoversold //4
        //and
        //close <= emaFast * (1-MinEMAGap/100) //5
        //and
        //close [1] cross above emaFast [1]   //6
        //and
        //Close cross below emaFast  //7
        //and
        //close cross below EHLOCdownband //8
        //and
        //close < STBreak
        //and
        //close cross below KLowerBand

        then 
        begin
        sellshort shortbuyingPower Shares next bar at market  ;
        end;
        }

        {
        if marketposition = -1 //Scale In - Conditions Add Entry Long
        and
        close < Open
        and
        close < open [1]
        and
        close[1] >= open[1]
        and
        close < emaFast
        and
        (1-close/entryprice)*100 > MinProfitforadd 
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
	end;



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
	//crossind = true;
	Sell longbuyingPower Shares Next Bar at Market;
	end;


	//close long position with trail start moving cross back
	if marketposition = 1 //there is long position open
	and
	(close/entryprice-1)*100 >= SmallbaseProfit 
	and
	barssinceentry > 1
	//and
	//Close < longStop * (1-os1/100)
	and
	close cross below emaMid30 
	//and
	//close > lastExitPrice 
	Then
	begin
	Sell Next Bar at Market;
	end;


        {
        //there is long position open and pass too much time without profit
        if marketposition = 1
        and
        (close/entryprice-1)*100 <= MinBaseProfit 
        and 
        barssinceentry > MinBarsForMove 
        then
        sell next bar at low [1]  stop;
        }


        {
        //close long position with trail start moving after large profit when entry price more then 200-2 deviation
        if marketposition = 1 //there is long position open
        and
        (close/entryprice-1)*100 >= largeMinProfit 
        and
        entryprice < vBlb2
        //AngleLong = True
        //entryprice < vBlb2
        then 
        begin
        valuePercentTrail = ((entryprice * LargeTrailStop) /100);
        trailProfit = Highest(high , Barssinceentry); 
        trailExit = trailProfit - valuePercentTrail;        
        sell  next bar at trailExit  stop;
        end;
        }

{
        //close long position after cross ema back
        if marketposition = 1 //there is long position open
        and
        (close/entryprice-1)*100 >= MinBaseProfit 
        and
        Close cross below emaFast  * (1-CrossEMAos/100)
        then 
        begin
        sell  next bar at market;
        end;
}


        {
        //take profit for a part of long position after small profit and move the stop to breakeven for the rest 
        if marketposition = 1 //there is long position open
        and
        (close/entryprice-1)*100 >= SmallMinProfitPart1 
        then 
        begin        
        sell 3         shares next bar at market;
        end;
        }

        ///take profit for a long position when touch middle of the channel
        //if marketposition = 1 //there is long position open
        //and
        //(vBmbHLOC/entryprice-1)*100 >= SmallMinProfitPart1 
        //then
        //begin
        //sell 4 shares next bar at vBmbHLOC limit;
        //end;

        //take profit for a part of long position when touch other side of the channel
        //if marketposition = 1 //there is long position open
        //and
        //(vBubHLOC/entryprice-1)*100 >= SmallMinProfitPart2
        //then 
        //begin        
        //sell next bar at vBubHLOC limit;
        //end;

{
        //take profit when zscore reach target
        if marketposition = 1 //there is long position open
        and
        Zscore >= 0
        then 
        begin        
        sell next bar at market;
        end;
}
        {
        //take profit when zscore reach target
        if marketposition = -1 //there is long position open
        and
        Zscore <= 0
        then 
        begin        
        buytocover next bar at market;
        end;
        }

        //exit when cross back 
        //if marketposition = 1 //there is long position open
        //and
        //Close <= (vBubHLOC *(1-StopLossOS/100))
        //then 
        //begin        
        //sell next bar at market;
        //end;

        {
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
        }

        {
        if marketposition = -1 //there is short position opens and pass too much time without profit
        and
        (1-Close/entryprice)*100 <= MinBaseProfit 
        and
        barssinceentry > MinBarsForMove 
        then
        buytocover next bar at High [1] stop;
        }

        {
        //take profit for a short position with trail start moving after large profit when entry price more then 200-2 deviation 
        if marketposition = -1 //there is short position open
        and
        (1-Close/entryprice)*100 >= largeMinProfit 
        //AngleShort = True
        and
        //entryprice > vBub2
        then 
        begin
        valuePercentTrail = ((entryprice * LargeTrailStop) /100);
        trailProfit = Lowest(low , Barssinceentry); 
        trailExit = trailProfit + valuePercentTrail; //          
        buytocover next bar at trailExit  stop;
        end;
        }

        {
        //close short position after cross ema back
        if marketposition = -1 //there is short position open
        and
        (1-Close/entryprice)*100 >= MinBaseProfit 
        and
        Close cross above emaFast
        then 
        begin
        buytocover next bar at market;
        end;
        }




        {
        //take profit for a part of short position after small profit and move the stop to breakeven for the rest 
        if marketposition = -1 //there is long position open
        and
        (1-Close/entryprice)*100 >=  SmallMinProfitPart1 
        then 
        begin        
        buytocover 3 shares next bar at market;
        end;
        }

        //take profit for a part of short position when touch middle of the channel
        //if marketposition = -1 //there is short position open
        //and
        //(1-vBmbHLOC/entryprice)*100 >= SmallMinProfitPart1 
        //then
        //begin
        //buytocover 4 shares next bar at vBmbHLOC limit;
        //end;

        //take profit for a short position when touch other side of the channel
        //if marketposition = -1 //there is short position open
        //and
        //(1-vBlbHLOC/entryprice)*100 >= SmallMinProfitPart2
        //then 
        //begin        
        //buytocover next bar at vBlbHLOC limit;
        //end;

        {
        //exit when cross back 
        //if marketposition = -1 //there is long position open
        //and
        //Close >= (vBlbHLOC *(1+StopLossOS/100))        
        //then 
        //begin        
        //buytocover next bar at market;
        //end;
        }

        {
        //take profit when zscore reach target
        if marketposition = -1 //there is long position open
        and
        Zscore <= 0
        then 
        begin        
        buytocover next bar at market;
        end;
        }


        //SetProfitTarget;
        if marketposition = 1
        then
        begin
        SetStopLoss(longSL);
        end;

        {
        if marketposition = -1
        then
        begin
        SetStopLoss(shortSL);
        end;
        }





