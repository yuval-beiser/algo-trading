[IntrabarOrderGeneration = True] //trade intra-bar

emaFast = XAverage(close,FastLength);
emaMid = XAverage(close,MidLength);
emaSlow = XAverage(close,SlowLength);
emafast1 = XAVERAGE(XAVERAGE(close,FastLength),FastLength);
demafast = emaFast * 2 - emafast1  ;    
emaverySlow = XAverage(close,VerySlowLength);
//ema2Fast = 0;//XAverage(close,FastLength) of data2;
//ema2Slow = 0;//XAverage(close ,slowLength) of data2;
//ema2verySlow = 0;//XAverage(close,VerySlowLength)of data2;
adxcalc = ADX(adxperiod);
buyingPower = 1 ;//(AccountBalance/Close)*PctPerTrade/100; // the amount of shares i can buy
//TakeProfitAmt = AccountBalance*PctPerTrade/100*TakeProfitPct/100;
//StopAmt = AccountBalance*PctPerTrade/100*StopPct/100;
valsdbg = "close=" + NumToStr(close ,2) + " dailyhigh=" + NumToStr(dailyhigh ,2) + " dailylow =" + NumToStr(dailylow ,2); // + " close =" + NumToStr(close ,2) + " close =" + NumToStr(close ,2) + " close =" + NumToStr(close ,2) + " close =" + NumToStr(close ,2) + " close =" + NumToStr(close ,2);
//print(Date, Time, "bar=", BarNumber, marketposition, valsdbg ); 


//BB HLOC 21
vBubHLOC = BollingerBand(HLOC ,BUpperBandHLOC,BStedDevHLOC);
vBlbHLOC = BollingerBand(HLOC ,BLowerBandHLOC, - BStedDevHLOC);
vBmbHLOC = (vBubHLOC+vBlbHLOC)/2;
HLOC = (HIGH+LOW+OPEN+CLOSE)/4;

HLOC2 = (HIGH of data2 +LOW of data2+OPEN of data2+CLOSE of data2)/4;
HLOC3 = (HIGH of data3 +LOW of data3+OPEN of data3+CLOSE of data3)/4;

emaHLOC = XAverage (HLOC , BUpperBandHLOC);
stdHLOC = StdDev(HLOC , BUpperBandHLOC);

emaHLOC2 = XAverage (HLOC2 , BUpperBandHLOC);
stdHLOC2 = StdDev(HLOC2 , BUpperBandHLOC);

emaHLOC3 = XAverage (HLOC3 , BUpperBandHLOC);
stdHLOC3 = StdDev(HLOC3 , BUpperBandHLOC);

EHLOCupband = emaHLOC + stdHLOC ;
EHLOCdownband = emaHLOC  - stdHLOC ;

EHLOCupband2 = emaHLOC2 + stdHLOC2 ;
EHLOCupband3 = emaHLOC3 + stdHLOC3 ;

EHLOCdownband2 = emaHLOC2 - stdHLOC2 ;
EHLOCdownband3 = emaHLOC3 - stdHLOC3 ;

//macd
vMacd = MACD( Close, macdFastLength, macdSlowLength ) ; // Fast line MACD
vMacdAvg = XAverage( vMacd , MACDlineLength) ; // Slow line MACD
vDiff = vMacd - vMacdAvg ; // Histogram

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


//VWAP crossing
vwap = Average(HLOC * Volume, vwapLength ) / Average(Volume, vwapLength );

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

//Zcore - Ratio between 2 stocks
Ratio = close / close of data2;
MeanRatio = Average (Ratio , RatioLength);
DevRatio = StdDev (MeanRatio , RatioLength);
Zscore = (Ratio - MeanRatio) / DevRatio ;

//Zcore - Ratio between 2 stocks
Ratio2 = close / close of data3;
MeanRatio2 = Average (Ratio , RatioLength);
DevRatio2 = StdDev (MeanRatio , RatioLength);
Zscore2 = (Ratio - MeanRatio) / DevRatio ;
