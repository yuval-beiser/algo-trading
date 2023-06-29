if marketposition = 0
then
[IntrabarOrderGeneration = false] //trade intra-bar
                        
smaFast = Average(close,FastLength);
smaMid = Average(close,MidLength);
//ema3VerySlow = XAverage(close,VerySlowLength) of data3;
smaSlow = Average(close,SlowLength);
emaSlow = XAverage(close,SlowLength);
emaverySlow = XAverage(close,VerySlowLength);
emaFast = XAverage(close,FastLength);

emafast1 = XAVERAGE(XAVERAGE(close,FastLength),FastLength);
demafast = emaFast * 2 - emafast1  ;    

ema2Fast = XAverage(close,FastLength)of data2;
ema2Slow = XAverage(close,SlowLength)of data2;
ema2verySlow = XAverage(close,VerySlowLength)of data2;
rsiSlow = rsi(close,RsiSlowLength);
rsiFast = rsi(close,RsiFastLength);
mom = Momentum(close, MomentumLength);
adxcalc = ADX(adxperiod);
buyingPower = 5;//(AccountBalance/Close)*PctPerTrade/100; // the amount of shares i can buy
TakeProfitAmt = AccountBalance*PctPerTrade/100*TakeProfitPct/100;
StopAmt = AccountBalance*PctPerTrade/100*StopPct/100;
valsdbg = "close=" + NumToStr(close ,2) + " dailyhigh=" + NumToStr(dailyhigh ,2) + " dailylow =" + NumToStr(dailylow ,2); // + " close =" + NumToStr(close ,2) + " close =" + NumToStr(close ,2) + " close =" + NumToStr(close ,2) + " close =" + NumToStr(close ,2) + " close =" + NumToStr(close ,2);

//BB
vBub1= BollingerBand(close,BUpperBand,BStedDev1);
vBlb1= BollingerBand(close,BLowerBand, - BStedDev1);
  
vBub2= BollingerBand(close,BUpperBand,BStedDev2);
vBlb2= BollingerBand(close,BLowerBand, - BStedDev2);

vBub3= BollingerBand(close,BUpperBand,BStedDev3);
vBlb3= BollingerBand(close,BLowerBand, - BStedDev3);

//VWAP crossing
vwap = Average(close * Volume, vwapLength ) / Average(Volume, vwapLength );

//Macd
MACDLine = MACD(Close, 12, 26); // Close price, short period, long period
SignalLine = XAverage(MACDLine, 9); // Signal line is a 9-period EMA of the MACD line
Histogram = MACDLine - SignalLine;

//ATR
atr =  AvgTrueRange (AtrLength);

//volume calc
//vTicks = Ticks ;
vAvgTicks= AverageFC( Ticks, AvgVolumeLength) ;

//Stoch
stochData1  = Stochastic( H, L, C, StochPiriod1, StochLength1, StochLength2, 1, 
oData1FastK, oData1FastD, oData1SlowK, oData1SlowD ) ; 

//Donchian
DonchianUp = HighestFC (h, DonchianLength );
DonchianDown = LowestFC (l, DonchianLength );
DonchianMid = (DonchianUp + DonchianDown)/2;

//RSI
vRSI = RSI (close, RsiFastLength);

//Zcore - Ratio between 2 stocks
Ratio = close / close of data2;
MeanRatio = Average (Ratio , RatioLength);
DevRatio = StdDev (MeanRatio , RatioLength);
Zscore = (Ratio - MeanRatio) / DevRatio ;



// START - PL for a day - CHECK IF PROFIT OR LOSS FOR THE DAY 
if DATE <> DATE[1] 
then begin
NetProf = NetProf + NetProfit - NetProf[1];
end;
PLTarget = Netprofit - NetProf;

// END - PL for a day - CHECK IF PROFIT OR LOSS FOR THE DAY 


// START -CONDITIONS FOR OPEN LONG POSITION 


//Conditions Entry Long
if marketposition = 0 
and( (PLTarget < PForDay) and (PLTarget > LForDay) ) 
and(Time > 940.00 and Time < 1525.00) //Increase from 9:35 to filter noise at the open ("no trade zone") //2 
and zscore < longminzscore 
and close > open
and close > close[1] //or (close [1] > close[2])) //B
and close < vBlb1
and close <= DonchianMid
and close > emafast
and Histogram > 0
then Begin
buy Floor(buyingPower) Shares next bar at market  ;
End;

// END -CONDITIONS FOR OPEN LONG POSITION 


//Conditions Entry Short 
// START -CONDITIONS FOR OPEN SHORT POSITION 

if marketposition = 0  and ( (PLTarget < PForDay) and (PLTarget > LForDay))  
and (Time > 940.00 and Time < 1525.00) //Increase from 9:35 to filter noise at the open("no trade zone") //2     
and zscore > shortminzscore 
and close < open
and close < close[1] 
and ((open[1] <= Close [1]) or (open [2] <= Close [2]) )
and close > vBub1
and close >= DonchianMid
and close < emafast
and Histogram < 0
then Begin
sellshort Floor(buyingPower) Shares next bar at market;
End;



// END - CONDITIONS FOR OPEN SHORT POSITION 


// START--  EXIT LONG BASE OF PRECENT -------------------------------------------------------


if marketposition = 1
then
[IntrabarOrderGeneration = True] //trade intra-bar - check every second and not 1 min
// false means check only for the close position 
//close long position with trail start moving after minimum profit 
if marketposition = 1 //there is long position open
and (Close/entryprice-1)*100 >= SmallMinProfit 
and barssinceentry <= 2 //  number of bars from begining . 
 
then begin
valuePercentTrail = ((entryprice * SmallTrailStop ) /100);
trailProfit = Highest(high , Barssinceentry); 
trailExit = trailProfit + valuePercentTrail; //          
sell next bar at trailExit  stop;
end;

// END - EXIT LONG BASE OF PRECENT -------------------------------------------------------




// START - EXIT LONG BASE ON CROSS PREVEVIOS LOW -------------------------------------------------------
//  initilias longStop
if marketposition = 0
then begin
longStop = -9999999;
end;

if marketposition = 1 //there is long position open
and (close/entryprice-1)*100 >= smallbaseProfit 
and barssinceentry > 2

then begin
// Calculate the trailing stop price
if low [1] > longStop 
then begin
longStop = low[1];
end;
end;



//close long position with trail start moving aafter the first bar from entry
if marketposition = 1 //there is long position open
and (close/entryprice-1)*100 >= smallbaseProfit 
and barssinceentry > 2
and Close < longStop 
Then begin
Sell Next Bar at Market;
end;

// END - EXIT LONG BASE ON CROSS PREVEVIOS LOW -------------------------------------------------------



// START--  EXIT SHORT BASE OF PRECENT -------------------------------------------------------

if marketposition = -1
then
[IntrabarOrderGeneration = True] //trade intra-bar


//close short position with trail start moving after minimum profit
if marketposition = -1 //there is long position open 
and (1-Close/entryprice)*100 >= SmallMinProfit 
and barssinceentry <= 2
then begin
valuePercentTrail = ((entryprice * SmallTrail) /100);
trailProfit = Lowest(low , Barssinceentry); 
trailExit = trailProfit + valuePercentTrail; //          
buytocover next bar at trailExit  stop;
end;


// END--  EXIT SHORT BASE OF PRECENT -------------------------------------------------------

// START - EXIT SHORT BASE ON CROSS PREVEVIOS High -------------------------------------------------------


//close short position with trail start moving after the first bar from entry
if marketposition = 0
then begin
shortStop = 9999999;
end;

if marketposition = -1 //there is long position open
and (1-Close/entryprice)*100 >= smallbaseProfit 
and barssinceentry > 2
then begin
// Calculate the trailing stop price
if High[1] < shortStop 
then begin
shortStop = High[1];
end;
end;



//close short position with trail start moving aafter the first bar from entry
if marketposition = -1 //there is long position open
and (1-Close/entryprice)*100 >= smallbaseProfit 
and barssinceentry > 2
and Close > shortStop 
Then begin
buytocover Next Bar at Market;
end;

// END - EXIT SHORT BASE ON CROSS PREVEVIOS High -------------------------------------------------------


// START - Exit on first stop loss -------------------------------------------------------

if marketposition = -1
then begin
SetStopLoss(shortSL);
end;

// END - Exit on first stop loss -------------------------------------------------------

