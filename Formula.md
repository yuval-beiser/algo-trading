                        
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
longbuyingPower = 3 ;//(AccountBalance/Close)*PctPerTrade/100; // the amount of shares i can buy //1
longbuyingPower1 = 2;
shortbuyingPower = 3 ;
shortbuyingPower1 = 2 ;

CurShares = GetPositionQuantity (getsymbolname, GetAccountID);


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

{
HLOC3 = (HIGH of data3 +LOW of data3+OPEN of data3+CLOSE of data3)/4;
HLOC4 = (HIGH of data4 +LOW of data4+OPEN of data4+CLOSE of data4)/4;
HLOC5 = (HIGH of data5 +LOW of data5+OPEN of data5+CLOSE of data5)/4;
}
	
emaHLOC = XAverage (HLOC , BUpperBandHLOC);
stdHLOC = StdDev(HLOC , BUpperBandHLOC);

emaHLOC2 = XAverage (HLOC2 , BUpperBandHLOC);
stdHLOC2 = StdDev(HLOC2 , BUpperBandHLOC);

{
emaHLOC3 = XAverage (HLOC3 , BUpperBandHLOC);
stdHLOC3 = StdDev(HLOC3 , BUpperBandHLOC);

emaHLOC4 = XAverage (HLOC4 , BUpperBandHLOC);
stdHLOC4 = StdDev(HLOC4 , BUpperBandHLOC);

emaHLOC5 = XAverage (HLOC5 , BUpperBandHLOC);
stdHLOC5 = StdDev(HLOC5 , BUpperBandHLOC);
}

EHLOCupband = emaHLOC + stdHLOC ;
EHLOCdownband = emaHLOC  - stdHLOC ;

EHLOCupband2 = emaHLOC2 + stdHLOC2 ;

{
EHLOCupband3 = emaHLOC3 + stdHLOC3 ;
EHLOCupband4 = emaHLOC4 + stdHLOC4 ;
EHLOCupband5 = emaHLOC5 + stdHLOC5 ;
}

EHLOCdownband2 = emaHLOC2 - stdHLOC2 ;

{
EHLOCdownband3 = emaHLOC3 - stdHLOC3 ;
EHLOCdownband4 = emaHLOC4 - stdHLOC4 ;
EHLOCdownband5 = emaHLOC5 - stdHLOC5 ;
}

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

//Zcore - Ratio between 2 stocks
Ratio = close / close of data2;
MeanRatio = Average (Ratio , RatioLength);
DevRatio = StdDev (MeanRatio , RatioLength);
Zscore = (Ratio - MeanRatio) / DevRatio ;


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
high5 = maxlist(close [1] , open [1], close [2] , open [2], close [3] , open [3], close [4] , open [4], close [5] , open [5],
close [6] , open [6], close [7] , open [7], close [8] , open [8], close [9] , open [9], close [10] 
);

{, open [10],
close [11] , open [11], close [12] , open [12], close [13] , open [13], close [14] , open [14], close [15] , open [15] ,
close [16] , open [16], close [17] , open [17], close [18] , open [18], close [18] , open [19], close [19] , open [19] ,
close [20] , open [20]
);
}
{
close [21] , open [21], close [22] , open [22], close [23] , open [23], close [24] , open [24] ,
close [25] , open [25], close [26] , open [26], close [27] , open [27], close [28] , open [28], close [29] , open [29] ,
close [30], open [30], close [31] , open [31], close [32] , open [32], close [33] , open [33], close [34] , open [34],
close [35] , open [35], close [36] , open [36], close [37] , open [37], close [38] , open [38], close [39] , open [39],
close [40] , open [40]
}


low5 = minlist (close [1] , open [1], close [2] , open [2], close [3] , open [3], close [4] , open [4], close [5] , open [5],
close [6] , open [6], close [7] , open [7], close [8] , open [8], close [9] , open [9], close [10] 
);

{
 open [10],
close [11] , open [11], close [12] , open [12], close [13] , open [13], close [14] , open [14], close [15] , open [15] ,
close [16] , open [16], close [17] , open [17], close [18] , open [18], close [18] , open [19], close [19] , open [19] ,
close [20] , open [20]
);
}

{
close [21] , open [21], close [22] , open [22], close [23] , open [23], close [24] , open [24] ,
close [25] , open [25], close [26] , open [26], close [27] , open [27], close [28] , open [28], close [29] , open [29] ,
close [30] , open [30] , close [31] , open [31], close [32] , open [32], close [33] , open [33], close [34] , open [34],
close [35] , open [35], close [36] , open [36], close [37] , open [37], close [38] , open [38], close [39] , open [39],
close [40] , open [40]
}

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
