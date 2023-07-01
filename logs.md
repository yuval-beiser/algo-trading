
	if marketposition = 0 then 
	begin
	//Long Prints - No position - dbug tag
	buydbg= ""; 
	if ((PLTarget < PForDay) and (PLTarget > LForDay))  then
	 buydbg = buydbg + "1" else buydbg = buydbg + "X" ;
	if close cross above EHLOCupband  then
	 buydbg = buydbg + "2" else buydbg = buydbg + "X" ;
	if close > Open  then
	 buydbg = buydbg + "3" else buydbg = buydbg + "X" ;
	 if close > open [1]   then
	 buydbg = buydbg + "4" else buydbg = buydbg + "X" ; 
	if close < vBub3 then
	 buydbg = buydbg + "5" else buydbg = buydbg + "X" ;
	if close <= low *(1+MaxFromLH/100)[1]  
	then buydbg = buydbg + "6" else buydbg = buydbg + "X" ;

	//Short Prints - No position - dbug tag
	selldbg = "";
	if ((PLTarget < PForDay) and (PLTarget > LForDay))  then
	selldbg = selldbg + "1" else selldbg = selldbg + "X" ;
	if close cross below EHLOCdownband  then
	selldbg = selldbg + "2" else selldbg = selldbg + "X" ;
	if close < Open    then
	selldbg = selldbg + "3" else selldbg = selldbg  + "X" ;
	if close < open [1]  then
	selldbg = selldbg + "4" else selldbg = selldbg  + "X" ;
	if close > vBlb3 then
	selldbg = selldbg + "5" else selldbg = selldbg  + "X" ;
	if close >= high *(1-MaxFromLH/100)   then
	selldbg = selldbg + "6" else selldbg = selldbg  + "X" ;


	if marketposition = 0  
	and
	ELDateToString(date) = "05/04/2023" //and symbol = "soxs" //and Time = 1300
	//and (close cross over emaFast  or close cross below emaFast )
	then
	//Long Prints - but No position
	print ( "MOM> symbol=" , symbol," ", "islong=", is_long_symbol,  "no position","  ",
	 ELDateToString(date),"Time=", time,"buydbg=", buydbg, "  ", "selldbg=", selldbg,
	 "     ","bar=", BarNumber,
	"entryprice=","xxxx.xx", 
	"close=", close, "PLTarget=", PLTarget,
	"emaFast=" , emaFast, 
	"LowD(0)=", LowD(0), "HighD(0)=", HighD(0), 
	"dema=", demafast,
	"vwap=", vwap,
	"vKeltUp  =", vKeltUp, "vKeltdown  =", vKeltDown, 
	"vBlb1 =", vBlb1, "vBlb2 =", vBlb2,"vBlb3 =", vBlb3,
	"vBub1 =", vBub1, "vBub2 =", vBub2,"vBub3 =", vBub3,
	"AvgVolumeLength= ", AvgVolumeLength, "volumeUP =", volumeUP ,
	"emaslow=", emaSlow, "emaverySlow =", emaverySlow , "ema3verySlow=" , ema3VerySlow , 
	 "ema2=",ema2Slow , "emaVerySlow=", ema3VerySlow, 
	"Close[1]=", Close[1], "Close[2]=", Close[2],
	"open=", Open, "open[1]=", Open[1], "open[2]=", Open[2],
	"low=", low, "low[1]=", Low[1], "low[2]=", Low[2],
	"high=", high, "high[1]=", high[1], "high[2]=", High[2],
	"openD0=", OpenD(0), "closeD1=", CloseD(1),
	"adxcalc =", adxcalc ,"adxmin=", adxmin , "MinProfit =",SmallMinProfit
	 ,"MinEMAGap=" , MinEMAGap,"MaxEMAGap=" , MaxEMAGap,
	 "smaFast=", smaFast, "smaMid=", smaMid, "smaSlow =", smaSlow ,
	  "MinGapSlowToMid=", MinGapSlowToMid,  
	"TakeProfitPct =", TakeProfitPct , "StopPct=", StopPct);
	end;


	//long position prints
	if marketposition = 1 
	and ELDateToString(date) = "05/04/2023" //and symbol = "soxs" //and Time = 1300
	then 
	print ( "MOM> symbol=" , symbol," ",  "in long", "      "
	,ELDateToString(date),"Time=", time,"buydbg=", buydbg, "     ","bar=", BarNumber,
	"entryprice=",entryprice, 
	"close=", close, "PLTarget=", PLTarget,
	"emaFast=" , emaFast, 
	"LowD(0)=", LowD(0), "HighD(0)=", HighD(0), 
	"dema=", demafast,
	"vwap=", vwap,
	"vKeltUp  =", vKeltUp, "vKeltdown  =", vKeltDown, 
	"vBlb1 =", vBlb1, "vBlb2 =", vBlb2,"vBlb3 =", vBlb3,
	"vBub1 =", vBub1, "vBub2 =", vBub2,"vBub3 =", vBub3,
	"AvgVolumeLength= ", AvgVolumeLength, "volumeUP =", volumeUP ,
	"emaslow=", emaSlow, "emaverySlow =", emaverySlow , "ema3verySlow=" , ema3VerySlow , 
	 "ema2=",ema2Slow , "emaVerySlow=", ema3VerySlow, 
	"Close[1]=", Close[1], "Close[2]=", Close[2],
	"open=", Open, "open[1]=", Open[1], "open[2]=", Open[2],
	"low=", low, "low[1]=", Low[1], "low[2]=", Low[2],
	"high=", high, "high[1]=", high[1], "high[2]=", High[2],
	"openD0=", OpenD(0), "closeD1=", CloseD(1),
	"adxcalc =", adxcalc ,"adxmin=", adxmin , "MinProfit =",SmallMinProfit
	 ,"MinEMAGap=" , MinEMAGap,"MaxEMAGap=" , MaxEMAGap,
	 "smaFast=", smaFast, "smaMid=", smaMid, "smaSlow =", smaSlow ,
	  "MinGapSlowToMid=", MinGapSlowToMid,  
	"TakeProfitPct =", TakeProfitPct , "StopPct=", StopPct);



	//short position prints       
	if marketposition = -1 
	and ELDateToString(date) = "05/04/2023" //and symbol = "soxs"//and Time = 1300
	then 
	print ("MOM> symbol=" , symbol," ", "in short","     ", ELDateToString(date),"Time=", time,"selldbg=", selldbg , "     ","bar=", BarNumber,
	"entryprice=",entryprice, 
	"close=", close, "PLTarget=", PLTarget,
	"emaFast=" , emaFast, 
	"LowD(0)=", LowD(0), "HighD(0)=", HighD(0), 
	"dema=", demafast,
	"vwap=", vwap,
	"vKeltUp  =", vKeltUp, "vKeltdown  =", vKeltDown, 
	"vBlb1 =", vBlb1, "vBlb2 =", vBlb2,"vBlb3 =", vBlb3,
	"vBub1 =", vBub1, "vBub2 =", vBub2,"vBub3 =", vBub3,
	"AvgVolumeLength= ", AvgVolumeLength, "volumeUP =", volumeUP ,
	"emaslow=", emaSlow, "emaverySlow =", emaverySlow , "ema3verySlow=" , ema3VerySlow , 
	 "ema2=",ema2Slow , "emaVerySlow=", ema3VerySlow, 
	"Close[1]=", Close[1], "Close[2]=", Close[2],
	"open=", Open, "open[1]=", Open[1], "open[2]=", Open[2],
	"low=", low, "low[1]=", Low[1], "low[2]=", Low[2],
	"high=", high, "high[1]=", high[1], "high[2]=", High[2],
	"openD0=", OpenD(0), "closeD1=", CloseD(1),
	"adxcalc =", adxcalc ,"adxmin=", adxmin , "MinProfit =",SmallMinProfit
	 ,"MinEMAGap=" , MinEMAGap,"MaxEMAGap=" , MaxEMAGap,
	 "smaFast=", smaFast, "smaMid=", smaMid, "smaSlow =", smaSlow ,
	  "MinGapSlowToMid=", MinGapSlowToMid,  
	"TakeProfitPct =", TakeProfitPct , "StopPct=", StopPct);
