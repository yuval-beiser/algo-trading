// formulas

//[IntrabarOrderGeneration = True] //trade intra-bar

//when no position reset CurShares - number of micro positions in same time 
if marketposition = 0
then
CurShares = 0;

//when no position use close bar
if marketposition = 0
then
[IntrabarOrderGeneration = true] //trade intra-bar


emaFast = XAverage(close,FastLength);
emaMid = XAverage(close,MidLength);
emaSlow = XAverage(close,SlowLength);
emafast1 = XAVERAGE(XAVERAGE(close,FastLength),FastLength);
demafast = emaFast * 2 - emafast1  ;    
emaverySlow = XAverage(close,VerySlowLength);
//ema2Fast = XAverage(close,FastLength) of data2;
//ema2Slow = 0;//XAverage(close ,slowLength) of data2;
//ema2verySlow = XAverage(close,VerySlowLength)of data2;
//ema2mid = XAverage(close,MidLength) of data2;
adxcalc = ADX(adxperiod);
longbuyingPower = 1 ;//(AccountBalance/Close)*PctPerTrade/100; // the amount of shares i can buy //1 //3
longbuyingPower1 = 2; // scale in
longbuyingPower2 = 3;
shortbuyingPower = 1 ; //3
shortbuyingPower1 = 2 ;
shortbuyingPower2 = 3 ;


CurShares = GetPositionQuantity (getsymbolname, GetAccountID);

// long stoploss
if 
CurShares = 1 
then 
longSL = startlongSL
else 
longSL = updatedlongSL;

// short stoploss
if 
CurShares = 1
then 
shortSL = startshortSL
else 
shortSL = updatedshortSL;


//TakeProfitAmt = AccountBalance*PctPerTrade/100*TakeProfitPct/100;
//StopAmt = AccountBalance*PctPerTrade/100*StopPct/100;
valsdbg = "close=" + NumToStr(close ,2) + " dailyhigh=" + NumToStr(dailyhigh ,2) + " dailylow =" + NumToStr(dailylow ,2); // + " close =" + NumToStr(close ,2) + " close =" + NumToStr(close ,2) + " close =" + NumToStr(close ,2) + " close =" + NumToStr(close ,2) + " close =" + NumToStr(close ,2);
//print(Date, Time, "bar=", BarNumber, marketposition, valsdbg ); 


//BB HLOC 21
vBubHLOC = BollingerBand(HLOC ,BUpperBandHLOC,BStedDevHLOC);
vBlbHLOC = BollingerBand(HLOC ,BLowerBandHLOC, - BStedDevHLOC);
vBmbHLOC = (vBubHLOC+vBlbHLOC)/2;
HLOC = (HIGH+LOW+OPEN+CLOSE)/4;

emaHLOC = XAverage (HLOC , BUpperBandHLOC);
stdHLOC = StdDev(HLOC , BUpperBandHLOC);

EHLOCupband = emaHLOC + stdHLOC ;
EHLOCdownband = emaHLOC  - stdHLOC ;
EHLOCmidband = (EHLOCupband+EHLOCdownband)/2;
EHLOCqtr1band = EHLOCdownband+((EHLOCupband-EHLOCdownband)/4);
EHLOCqtr3band = EHLOCupband-((EHLOCupband-EHLOCdownband)/4);

//BB 200 Regular
vBub1= BollingerBand(close,BUpperBand,BStedDev1);
vBlb1= BollingerBand(close,BLowerBand, - BStedDev1);
  
vBub2= BollingerBand(close,BUpperBand,BStedDev2);
vBlb2= BollingerBand(close,BLowerBand, - BStedDev2);

vBub3= BollingerBand(close,BUpperBand,BStedDev3);
vBlb3= BollingerBand(close,BLowerBand, - BStedDev3);


//BB 200 Exponencial
stdclose = StdDev (close, VerySlowLength);
evBub2 = emaverySlow + (stdDevMultiplier2 * stdclose) ;
evBlb2 = emaverySlow - (stdDevMultiplier2 * stdclose) ;

{
//VWAP crossing
vwap = Average(HLOC * Volume, vwapLength ) / Average(Volume, vwapLength );
}
//macd
vMacd = MACD( Close, macdFastLength, macdSlowLength ) ; // Fast line MACD
vMacdAvg = XAverage( vMacd , MACDlineLength) ; // Slow line MACD
vDiff = vMacd - vMacdAvg ; // Histogram

//Keltner
vKeltUp = KeltnerChannel(HLOC ,KUpperBand,KStdAtr);
vKeltDown = KeltnerChannel(HLOC ,KLowerBand,-KStdAtr);

//ATR
atr =  AvgTrueRange (AtrLength);

// Calculate a switch for identify long or short (for the connection with VXX)
if symbol = "SOXS" or symbol = "LABD" or symbol = "SQQQ" then
is_long_symbol = False;

//volume calc
//vTicks = Ticks ;
vAvgTicks= AverageFC( Ticks, AvgVolumeLength) ;

//Zaviot
MAValue1 = XAverage( Close, FastLength ) ; 
MASlope1 = ( MAValue1 - MAValue1[1] );// * (Minmove/Pricescale);  // SLOPE = Shipooaa 
MAAngle1 = ArcTangent( MASlope1 ) ; // ZAVIT = Press F1 to see explain
         
MAValue2 = XAverage( Close,MidLength  ) ; 
MASlope2 = ( MAValue2 - MAValue2[1]);// * (Minmove/Pricescale)  ; 
MAAngle2 = ArcTangent( MASlope2 ) ; 
         
MAValue3 = XAverage( Close, SlowLength ) ; 
MASlope3 = ( MAValue3 - MAValue3[1] );// * (Minmove/Pricescale)  ; 
MAAngle3 = ArcTangent( MASlope3 ) ; 

BullAngle = ((MAValue1 > MAValue2) And (MAValue2 > MAValue3)) ;//And (Close Crosses Over  MAValue1);
BearAngle = ((MAValue1 < MAValue2) And (MAValue2 < MAValue3)) ; //And (Close Crosses Under  MAValue1);
AngleLong  = (( MAAngle1 > ANGLE_MA1) And (MAAngle1 < ANGLE_MA2 ));
AngleShort = (( MAAngle1 < ANGLE_MA1 * (-1)) And (MAAngle1 > ANGLE_MA2 * (-1)) );

//Donchian
DonchianUp = HighestFC (h, DonchianLength );
DonchianDown = LowestFC (l, DonchianLength );

//Stoch
stochData1  = Stochastic( H, L, C, StochPiriod1, StochLength1, StochLength2, 1, 
oData1FastK, oData1FastD, oData1SlowK, oData1SlowD ) ; 

//RSI
vRSI = RSI (close, RsiFastLength);

//Triangle
//The upper boundary or resistance level of the ascending triangle pattern
THign = Highest(High, TLength);

//The lower boundary or support level of the ascending triangle pattern
TLow = Lowest(low, TLength);

//breakout level
LTBreak = THign  + (TLow - THign)* LTpct;
STBreak = THign  + (TLow - THign)* STpct;

//high and low level
high5 = maxlist(close [1] , open [1], close [2] , open [2], close [3] , open [3], close [4] , open [4], close [5] , open [5] );
low5 = minlist (close [1] , open [1], close [2] , open [2], close [3] , open [3], close [4] , open [4], close [5] , open [5] );

high9 = maxlist(close [1] , open [1], close [2] , open [2], close [3] , open [3], close [4] , 
open [4], close [5] , open [5], close [6] , open [6], close [7] , open [7], close [8] , open [8], close [9] , open [9] );

low9 = minlist (close [1] , open [1], close [2] , open [2], close [3] , open [3], close [4] , 
open [4], close [5] , open [5], close [6] , open [6], close [7] , open [7], close [8] , open [8], close [9] , open [9] );


//Macd
MACDLine = MACD(Close, 12, 26); // Close price, short period, long period
SignalLine = XAverage(MACDLine, 9); // Signal line is a 9-period EMA of the MACD line
Histogram = MACDLine - SignalLine;

//PP
// Calculate Support and Resistance Levels
PP = 
(
HighestFC(high,ppLength) + LowestFC(low,ppLength) + Close[1] 
) /3;
S1 = (2 * PP) - HighestFC(high, ppLength);
S2 = PP - (HighestFC (high, ppLength) - LowestFC(low, ppLength));
S3 = LowestFC(low, ppLength) - 2 * (HighestFC (high, ppLength) - PP);
R1 = (2 * PP) - LowestFC(low, ppLength);
R2 = PP + (HighestFC(high, ppLength) - LowestFC(low, ppLength));
R3 = HighestFC(high, ppLength) + 2 * (PP - LowestFC (low, ppLength));

{
//Zcore - Ratio between 2 stocks
Ratio = close / close of data2;
MeanRatio = Average (Ratio , RatioLength);
DevRatio = StdDev (MeanRatio , RatioLength);
Zscore = (Ratio - MeanRatio) / DevRatio ;
}

//PL for a day
if DATE <> DATE[1] 
then 
begin
NetProf = NetProf + NetProfit - NetProf[1];
end;
PLTarget = Netprofit - NetProf;
