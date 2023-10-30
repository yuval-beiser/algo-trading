
//reset alertsGenerated when not in possition
if marketposition = 0 and rtPosition= 0
then
alertsGenerated = 0;


//Reset MP
if marketposition = 0 and LastMarketPosition <> 0
then begin
ExitBarNum = BarNumber;
rtPosition = marketposition;
end;
LastMarketPosition = marketposition;

//reset crossind
if marketposition = 0
then
begin
crossind1 = False;
end;

//reset crossind
if marketposition = 0
then
begin
crossind2 = False;
end;

//close on cross back
if marketposition = 0
then
begin
shortStop = 9999999;
end;

//close on cross back
if marketposition = 0
then
begin
longstop = -9999999;
end;
