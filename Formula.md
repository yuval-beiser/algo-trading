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
emaMid30 = XAverage(close,MidLength1);

emafast1 = XAVERAGE(XAVERAGE(close,FastLength),FastLength);
demafast = emaFast * 2 - emafast1  ;    

//ema2Fast = XAverage(close,FastLength)of data2;
//ema2Slow = XAverage(close,SlowLength)of data2;
ema2verySlow = XAverage(close,VerySlowLength)of data2;
rsiSlow = rsi(close,RsiSlowLength);
rsiFast = rsi(close,RsiFastLength);
mom = Momentum(close, MomentumLength);
adxcalc = ADX(adxperiod);

longbuyingPower = 3 ;//(AccountBalance/Close)*PctPerTrade/100; // the amount of shares i can buy //1 //3
longbuyingPower1 = 1; // scale in-out
longbuyingPower2 = 1;
shortbuyingPower = 3; //3
shortbuyingPower1 = 1 ; // scale in-out
shortbuyingPower2 = 1 ;

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
Zscore = (Ratio - MeanRatio) / DevRatio;

//high and low level
high5 = maxlist(close [1] , open [1], close [2] , open [2], close [3] , open [3], close [4] , open [4], close [5] , open [5] );
low5 = minlist (close [1] , open [1], close [2] , open [2], close [3] , open [3], close [4] , open [4], close [5] , open [5] );


//close short position with trail start moving after the first bar from entry
if marketposition = 0
then
begin
shortStop = 9999999;
end;

//PL for a day - CHECK IF PROFIT OR LOSS FOR THE DAY 
if DATE <> DATE[1] 
then 
begin
NetProf = NetProf + NetProfit - NetProf[1];
end;
PLTarget = Netprofit - NetProf;

//calc a switch for identify long or short (for the connection with VXX)
if symbol = "SOXS" or symbol = "LABD" or symbol = "SQQQ" then
is_long_symbol = False;
