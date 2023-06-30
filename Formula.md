[IntrabarOrderGeneration = True] //trade intra-bar

smaFast = Average(close,FastLength);
smaMid = Average(close,MidLength);
emaMid = XAverage(close,MidLength);
//ema3VerySlow = XAverage(close,VerySlowLength) of data3;
smaSlow = Average(close,SlowLength);
emaSlow = XAverage(close,SlowLength);
emaverySlow = XAverage(close,VerySlowLength);
emaFast = XAverage(close,FastLength);

emafast1 = XAVERAGE(XAVERAGE(close,FastLength),FastLength);
demafast = emaFast * 2 - emafast1  ;    

ema2Fast = XAverage(close,FastLength)of data2;
//ema2Slow = XAverage(close,SlowLength)of data2;
ema2verySlow = XAverage(close,VerySlowLength) of data2;
rsiSlow = rsi(close,RsiSlowLength);
rsiFast = rsi(close,RsiFastLength);
mom = Momentum(close, MomentumLength);
adxcalc = ADX(adxperiod);

//emadayVerySlow = XAverage(close,VerySlowLength) of data4;
//emadayfast = XAverage(close,FastLength) of data4;

If 
(
(close of data2 cross above ema2verySlow) or (close[1] of data2 cross above ema2verySlow) 
)
or 
(
(close of data2 cross below ema2verySlow) or (close[1] of data2 cross below ema2verySlow) 
)
then 
begin 
MultiplierPower=1 ;
end;

buyingPower = (AccountBalance/Close)*PctPerTrade/100*MultiplierPower; // the amount of shares i can buy

longbuyingPower1 = (AccountBalance/Close)*PctPerTrade/100*MultiplierPower*Pctforadd/100;
shortbuyingPower1 = (AccountBalance/Close)*PctPerTrade/100*MultiplierPower*Pctforadd/100;

TakeProfitAmt = AccountBalance*PctPerTrade/100*TakeProfitPct/100*MultiplierPower;
StopAmt = AccountBalance*PctPerTrade/100*StopPct/100*MultiplierPower;
valsdbg = "close=" + NumToStr(close ,2) + " dailyhigh=" + NumToStr(dailyhigh ,2) + " dailylow =" + NumToStr(dailylow ,2); // + " close =" + NumToStr(close ,2) + " close =" + NumToStr(close ,2) + " close =" + NumToStr(close ,2) + " close =" + NumToStr(close ,2) + " close =" + NumToStr(close ,2);
//print(Date, Time, "bar=", BarNumber, marketposition, valsdbg ); 

CurShares = GetPositionQuantity (getsymbolname, GetAccountID);

//BB
vBub1= BollingerBand(close,BUpperBand,BStedDev1);
vBlb1= BollingerBand(close,BLowerBand, - BStedDev1);
  
v2Bub1= BollingerBand(close of data2,BUpperBand,BStedDev1);
v2Blb1= BollingerBand(close of data2,BLowerBand, - BStedDev1);
  
vBub2= BollingerBand(close,BUpperBand,BStedDev2);
vBlb2= BollingerBand(close,BLowerBand, - BStedDev2);

vBub3= BollingerBand(close,BUpperBand,BStedDev3);
vBlb3= BollingerBand(close,BLowerBand, - BStedDev3);

vBub5= BollingerBand(close,BUpperBand,BStedDev5);
vBlb5= BollingerBand(close,BLowerBand, - BStedDev5);


//VWAP crossing
vwap = Average(close * Volume, vwapLength ) / Average(Volume, vwapLength );

//volume calc
//vTicks = Ticks ;
vAvgTicks= AverageFC( Ticks, AvgVolumeLength) ;

//Stoch
stochData1  = Stochastic( H, L, C, StochPiriod1, StochLength1, StochLength2, 1, 
oData1FastK, oData1FastD, oData1SlowK, oData1SlowD ) ; 

//Donchian
DonchianUp = HighestFC (h, DonchianLength );
DonchianDown = LowestFC (l, DonchianLength );

//RSI
vRSI = RSI (close, RsiFastLength);

//Macd
MACDLine = MACD(Close, 12, 26); // Close price, short period, long period
SignalLine = XAverage(MACDLine, 9); // Signal line is a 9-period EMA of the MACD line
Histogram = MACDLine - SignalLine;

//Zcore - Ratio between 2 stocks
Ratio = close / close of data4;
MeanRatio = Average (Ratio , RatioLength);
DevRatio = StdDev (MeanRatio , RatioLength);
Zscore = (Ratio - MeanRatio) / DevRatio ;


//PL for a day
if DATE <> DATE[1] 
then 
begin
NetProf = NetProf + NetProfit - NetProf[1];
end;
PLTarget = Netprofit - NetProf;

//calc a switch for identify long or short (for the connection with VXX)
if symbol = "SOXS" or symbol = "LABD" or symbol = "SQQQ" then
is_long_symbol = False;
