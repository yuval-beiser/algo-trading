if marketposition = 0 then 
begin
//Long Prints - No position - dbug tag
buydbg= ""; 
if (
(PLTarget < PForDay) and (PLTarget > LForDay) 
)  
 then
 buydbg = buydbg + "1" else buydbg = buydbg + "X" ;
if (Time > 0700.00 and Time < 2200.00) then
 buydbg = buydbg + "2" else buydbg = buydbg + "X" ;
if close > Open  then
 buydbg = buydbg + "3" else buydbg = buydbg + "X" ;
if close > high5  then
 buydbg = buydbg + "4" else buydbg = buydbg + "X" ;
 if close > high [1]  then
 buydbg = buydbg + "5" else buydbg = buydbg + "X" ; 
if open > emaMid  then
 buydbg = buydbg + "6" else buydbg = buydbg + "X" ;
if open > emaverySlow    
then buydbg = buydbg + "7" else buydbg = buydbg + "X" ;
if emaMid >= emaverySlow * (1+Mingap/100)    
then buydbg = buydbg + "8" else buydbg = buydbg + "X" ;
if emaMid <= emaverySlow * (1+Maxgap/100)
then buydbg = buydbg + "9" else buydbg = buydbg + "X" ;
if close <= emaverySlow * (1+Maxgap1/100)
then buydbg = buydbg + "A" else buydbg = buydbg + "X" ;


//Short Prints - No position - dbug tag
selldbg = "";
if (
(PLTarget < PForDay) and (PLTarget > LForDay)
)  then
selldbg = selldbg + "1" else selldbg = selldbg + "X" ;
if (Time > 0700.00 and Time < 2200.00)  then
selldbg = selldbg + "2" else selldbg = selldbg + "X" ;
if close < Open  then
selldbg = selldbg + "3" else selldbg = selldbg + "X" ;
if close < low5    then
selldbg = selldbg + "4" else selldbg = selldbg  + "X" ;
if close < low   then
selldbg = selldbg + "5" else selldbg = selldbg  + "X" ;
if open < emaMid 
 then
selldbg = selldbg + "6" else selldbg = selldbg  + "X" ;
if open < emaverySlow    then
selldbg = selldbg + "7" else selldbg = selldbg  + "X" ;
if emaMid <= emaverySlow * (1-Mingap/100)    then
selldbg = selldbg + "8" else selldbg = selldbg  + "X" ;
if emaMid >= emaverySlow * (1-Maxgap/100) then
selldbg = selldbg + "9" else selldbg = selldbg  + "X" ;
if close >= emaverySlow * (1-Maxgap1/100)
 then selldbg = selldbg + "A" else selldbg = selldbg  + "X" ;




if marketposition = 0  
and
ELDateToString(date) = "06/14/2023" //and symbol = "soxs" //and Time = 1300
//and (close cross over emaFast  or close cross below emaFast )
then
//Long Prints - but No position
print ( "MOMTEST  > symbol=" , symbol," ", "islong=", is_long_symbol,  "no position","  ",
 ELDateToString(date),"Time=", time,"buydbg=", buydbg, "  ", "selldbg=", selldbg,
 "     ","bar=", BarNumber,
"entryprice=","xxxx.xx", 
"close=", close, 
//"shortStop =", shortStop  ,
"high5=", high5, "low5=", low5,
"S1=", S1, "S2=", S2, "S3=", S3, "R1=", R1,  "R2=", R2,  "R3=", R3, 
"EHLOCdownband =", EHLOCdownband ,
"EHLOCupband =", EHLOCupband ,
"PLTarget=", PLTarget,
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
and ELDateToString(date) = "06/14/2023" //and symbol = "soxs" //and Time = 1300
then 
print ( "MOMTEST   > symbol=" , symbol," ",  "in long", "      "
,ELDateToString(date),"Time=", time,"buydbg=", buydbg, "     ","bar=", BarNumber,
"entryprice=",entryprice, 
"close=", close, 
//"shortStop =", shortStop  ,
//"longStop =", longStop ,
"high5=", high5, "low5=", low5,
"S1=", S1, "S2=", S2, "S3=", S3, "R1=", R1,  "R2=", R2,  "R3=", R3, 
"EHLOCdownband =", EHLOCdownband ,
"EHLOCupband =", EHLOCupband ,
"PLTarget=", PLTarget,
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
and ELDateToString(date) = "06/14/2023" //and symbol = "soxs"//and Time = 1300
then 
print ("MOMTEST  > symbol=" , symbol," ", "in short","     ", ELDateToString(date),"Time=", time,"selldbg=", selldbg , "     ","bar=", BarNumber,
"entryprice=",entryprice, 
"close=", close, 
//"shortStop =", shortStop  ,
//"longStop =", longStop ,
"high5=", high5, "low5=", low5,
"S1=", S1, "S2=", S2, "S3=", S3, "R1=", R1,  "R2=", R2,  "R3=", R3, 
"EHLOCdownband =", EHLOCdownband ,
"EHLOCupband =", EHLOCupband ,
"PLTarget=", PLTarget,
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



