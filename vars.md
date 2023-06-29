
vars:
smaFast(0),
smaMid(0),
ema3VerySlow (0),
emaVerySlow (0),
smaSlow(0),
emaSlow (0),
emaFast(0),
emafast1 (0),
demafast (0),
ema1preFast (0), 
ema2preFast (0), 
ema2Fast (0),
ema2Slow (0),
ema2verySlow (0),
rsiSlow(0),
rsiFast(0),
mom (0),
vwap(0), 
adxcalc (0),
buyingPower(0),
curProfit(0),
TakeProfitAmt (0),
StopAmt (0),
SwitchLargeSmall (0),
buydbg(""),
selldbg(""),
valsdbg(""),

//Donchian 
DonchianLength (21), 

//VOLUME
vVOL(0),
vAvgVol(0),
vTicks(0),
vAvgTicks(0),

//BB
vStd(0),
vBub1(0),
vBlb1(0),
vBub2(0),
vBlb2(0),
vBub3(0),
vBlb3(0),

//Satistical Arbitrage
Ratio (0),
MeanRatio (0),
devRatio (0),
Zscore (0),

// Trailing
barCount(0), // count from the first bar
high1stBar(0), // Extreme high from a list 
low1stBar(0), // Extreme low from a list 
trailProfit(0),
SmallTrailStop(SmallTrail ), //0.8
LargeTrailStop(largeTrail ),
FastTrailStop(FastTrail ), //0.38
intrabarpersist trailExit(0), // F1 Update on every tick
valuePercentTrail(0),

is_long_symbol(true),

//Macd
MACDLine (0),
SignalLine (0),
Histogram (0),

//PL for a day
NetProf(0),
PLTarget(0),

atr (0),

//Stoch
oData1FastK( 0 ),
oData1FastD( 0 ), 
oData1SlowK( 0 ),
oData1SlowD( 0 ), 
stochData1(0),
stochData2(0),

//Donchian
DonchianUp (0),
DonchianDown (0),
DonchianMid (0),

//RSI
vRSI (0);

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


longStop (-9999999);

shortStop (9999999);
