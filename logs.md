
	{
	if marketposition = 0 then 
	begin
	//Long Prints - No position - dbug tag
	buydbg= ""; 
	if (
	(PLTarget < PForDay) and (PLTarget > LForDay) 
	)  
	 then
	 buydbg = buydbg + "1" else buydbg = buydbg + "X" ;
	if 
	(
	(Time > 1400.00) or (Time < 1200.00 and Time > 430.00) or (Time < 1200.00 and Time < 300.00) 
	)
	 then
	 buydbg = buydbg + "2" else buydbg = buydbg + "X" ;
	if close > Open  then
	 buydbg = buydbg + "3" else buydbg = buydbg + "X" ;
	if close > high5 then
	 buydbg = buydbg + "4" else buydbg = buydbg + "X" ;
	 if low5 < emaVerySlow then
	 buydbg = buydbg + "5" else buydbg = buydbg + "X" ; 
	if close > emaMid then
	 buydbg = buydbg + "6" else buydbg = buydbg + "X" ;
	if close > emaverySlow   
	then buydbg = buydbg + "7" else buydbg = buydbg + "X" ;
	if emaMid <= emaverySlow * (1+Maxgap/100)   
	then buydbg = buydbg + "8" else buydbg = buydbg + "X" ;
	if close <= emaverySlow * (1+Maxgap1/100) 
	then buydbg = buydbg + "9" else buydbg = buydbg + "X" ;
	if close cross above emaFast
	then buydbg = buydbg + "A" else buydbg = buydbg + "X" ;
	}

	{
	//Short Prints - No position - dbug tag

	selldbg = "";
	if (
	(PLTarget < PForDay) and (PLTarget > LForDay)
	)  then
	selldbg = selldbg + "1" else selldbg = selldbg + "X" ;
	if (
	(Time > 1400.00) or (Time < 1200.00 and Time > 430.00) or (Time < 1200.00 and Time < 300.00) //2
	) then
	selldbg = selldbg + "2" else selldbg = selldbg + "X" ;
	if close < Open  then
	selldbg = selldbg + "3" else selldbg = selldbg + "X" ;
	if close < low5    then
	selldbg = selldbg + "4" else selldbg = selldbg  + "X" ;
	if high5 > emaVerySlow   then
	selldbg = selldbg + "5" else selldbg = selldbg  + "X" ;
	if close < emaMid
	 then
	selldbg = selldbg + "6" else selldbg = selldbg  + "X" ;
	if close < emaverySlow   then
	selldbg = selldbg + "7" else selldbg = selldbg  + "X" ;
	if emaMid >= emaverySlow * (1-Maxgap/100)    then
	selldbg = selldbg + "8" else selldbg = selldbg  + "X" ;
	if close >= emaverySlow * (1-Maxgap1/100) then
	selldbg = selldbg + "9" else selldbg = selldbg  + "X" ;
	if close cross below emaFast
	 then selldbg = selldbg + "A" else selldbg = selldbg  + "X" ;
	}

{
//no position prints
if marketposition = 0 and ELDateToString(date) = "09/07/2023" and lastPrintBar <> BarNumber//and symbol = "soxs" //and Time = 1300
then 
begin
print ( "MOMTEST   > symbol=" , symbol," ",  
ELDateToString(date),"Time=", time, "time_s=", time_s, " lastPrintBar=",lastPrintBar, " buydbg=", buydbg, "     ",
 "no   position",
"close=", close,
"entryprice=",entryprice, 
"bar=", BarNumber,
"ExitBarNum=", ExitBarNum,
"marketposition=",marketposition,
"LastMarketPosition =", LastMarketPosition ,
"MinBarsAfterCloseToEntry  =", MinBarsAfterCloseToEntry ,
"MinBarsAfterCloseToEntry=" , MinBarsAfterCloseToEntry ,
"ExitBarNum + MinBarsAfterCloseToEntry=" , ExitBarNum + MinBarsAfterCloseToEntry
);
lastPrintBar = BarNumber;
end;

//long position prints
if marketposition = 1 and ELDateToString(date) = "09/07/2023" and lastPrintBar <> BarNumber//and symbol = "soxs" //and Time = 1300
then 
begin
print ( "MOMTEST   > symbol=" , symbol," ",  
ELDateToString(date),"Time=", time, "time_s=", time_s, " lastPrintBar=",lastPrintBar, " buydbg=", buydbg, "     ",
 "long   position",
"close=", close,
"entryprice=",entryprice, 
"bar=", BarNumber,
"ExitBarNum=", ExitBarNum,
"marketposition=",marketposition,
"LastMarketPosition =", LastMarketPosition ,
"MinBarsAfterCloseToEntry  =", MinBarsAfterCloseToEntry ,
"MinBarsAfterCloseToEntry=" , MinBarsAfterCloseToEntry ,
"ExitBarNum + MinBarsAfterCloseToEntry=" , ExitBarNum + MinBarsAfterCloseToEntry
);
lastPrintBar = BarNumber;
end;


//short position prints
if marketposition = -1 and ELDateToString(date) = "09/07/2023" and lastPrintBar <> BarNumber//and symbol = "soxs" //and Time = 1300
then 
begin
print ( "MOMTEST   > symbol=" , symbol," ",  
ELDateToString(date),"Time=", time, "time_s=", time_s, " lastPrintBar=",lastPrintBar, " buydbg=", buydbg, "     ",
 "short   position",
"close=", close,
"entryprice=",entryprice, 
"bar=", BarNumber,
"ExitBarNum=", ExitBarNum,
"marketposition=",marketposition,
"LastMarketPosition =", LastMarketPosition ,
"MinBarsAfterCloseToEntry  =", MinBarsAfterCloseToEntry ,
"MinBarsAfterCloseToEntry=" , MinBarsAfterCloseToEntry ,
"ExitBarNum + MinBarsAfterCloseToEntry=" , ExitBarNum + MinBarsAfterCloseToEntry
);
lastPrintBar = BarNumber;
end;
}

