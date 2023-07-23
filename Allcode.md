        //@version=31323-2
        Inputs:

        FastLength(9),
        MidLength(20),
        MidLength1 (30),
        SlowLength(50),
        VerySlowLength (200),
        stdDevMultiplier2 (2),
        RsiSlowLength(10),
        RsiFastLength(8),
        TLength (21),
        SLength (21),
        MinGapSlowToMid(0.1),
        RsiMinForLong(40),
        RsiMaxForShort(60),
        MomentumLength(14),
        Longminmom (-0.3),
        Shortmaxmom (0.3),
        ExitBarNum1(12),
        ExitBarNum2(24),
        ExitBarNum3(36),
        ExitBarNum (5),
        MinProfitAfter1Hour(100),
        MinProfitAfter2Hours(150),
        MinProfitAfter3Hours(180),
        CloseAfter1Hour(20),
        CloseAfter2Hour(20), 
        CloseAfter3Hour(40),
        MinProfitForTheDay(200),
        MaxFromLH(0.2), //0.16875
        MinFromLH (0.12),
        MaxFromLHEntry (0.75),
        MinFromLHentry (0.15),
        MinKeltnerCross (0.08),
        MinemaGap (0.0005), // 0.01875
        MaxemaGap (0.025), //0.22  
        Mingap (0.14), //0.06 was too tight according to 8.3.23 , 3:03 AM //0.15
        Maxgap (0.025),
        MinProfit (0.00625),
        SmallMinProfit (0.1), //after 12 pips start trail of 4 pips //0.075 with stochastic //0.0925 //0.25 //0.2 //0.21
        smallbaseProfit (0.05), 
        largeMinProfit (0.04375), //after 10 pips start trail of 8 pips //0.09375
        SmallMinProfitPart1 (0.05), //after 3 pips limit 3 at the middle of the chanel
        SmallMinProfitPart2 (0.0375), //after 6 pips limit at the other side of the channel
        MinProfitforadd (0.07),
        MaxProfitForAdd (0.1),
        FastMinProfit (0.0625), //0.1125
        MinBaseProfit (0.03),
        MinLossForAdd (0.4),
        SmallTrail (0.04), //0.04375 with stochastic //0.00625 //0.0125 //0.025
        largeTrail (0.025),
        MinSQQQTQQQGap (0.09),
        Minbarsfortake (5), //2
        MinBarsForMove (30), //12
        MaxBarsforadd (1),
        maxpositions (6),
        MinbarsHL (5),
        ExitCrossOS (0.14),
        StopLossOS (0.01875),
        adxperiod (14),
        adxmin(25),
        vwapLength (20),
        SQQQTQQQGap(0.15),
        AtrLength (14),
        AtrMin(15), //0.6
        Atrmax (1.8),
        ANGLE_MA1( 8), //25
        ANGLE_MA2( 60 ),
        ANGLE_MA3( 70 ), 
        TailHammerRatio (7),
        MinChanel (3),
        MaxChanel (10),
        Hlocpartlong (2),
        Hlocpartshort (2),
        LTpct (0.3),
        STpct (0.3),
        RatioLength (200),
        CrossEMAos (0.0125),
        os1 (0.0133),

        PForDay (800), //1500 //1950 //100
        LForDay (-50), //-1100 //-500 //-50

        //Donchian 
        DonchianLength (20), 

        //macd
        macdFastLength( 12 ), 
        macdSlowLength( 26 ), 
        MACDlineLength( 9 ) ,

        //BB
        BStedDev1(1),
        BStedDev2(1.5), //1.5
        BStedDev3(3),
        BUpperBand(200),
        BLowerBand(200),
        MinFromBB (0.24),
        MaxFromBB (0.8),

        //BB HLOC
        BStedDevHLOC (2), 
        BUpperBandHLOC(21), //39
        BLowerBandHLOC(21), //39

        //Keltner
        KStdAtr(1.5),
        KUpperBand(43),
        KLowerBand(43),


        //Stoch
        StochPiriod1( 5 ), //14
        //StochPiriod2( 14 ),
        StochLength1( 5 ), 
        StochLength2( 4 ),
        StochOverBot(74), //76
        StochOverSold(26), //14
        stochmid (50),

        //RSI
        RSIOverbot (70),
        RSIoversold (46),

        double AccountBalance(10000), // Account balance 10,000 $
        PctPerTrade(50),
        TakeProfit (200),
        TakeProfitPct (6.5),
        StopPct (0.025),
        longSL(240), //180 with stochastic //140 //80 //450
        shortSL(240),

        //Zscore
        longminzscore (-2),
        shortminzscore (2);


        vars:
        smaFast(0),
        longStop (-9999999),
        smaMid(0),
        emaMid30 (0),
        ema3VerySlow (0),
        emaVerySlow (0),
        smaSlow(0),
        emaSlow (0),
        emaMid (0),
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
        AvgVolumeLength(50), //50
        volumeUP (30), //10
        mom (0),
        vwap(0), 
        atr (0),
        adxcalc (0),
        longbuyingPower(0),
        shortbuyingPower(0),
        longbuyingPower1 (0),
        shortbuyingPower1 (0),
        curProfit(0),
        TakeProfitAmt (0),
        StopAmt (0),
        SwitchLargeSmall (0),
        buydbg(""),
        selldbg(""),
        valsdbg(""),
        CurShares (0),

        //macd
        vMacd(0), 
        vMacdAvg(0), 
        vDiff(0) ,

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


        //E-BB
        stdclose (0),
        evBub2 (0),
        evBlb2 (0),

        //BB HLOC
        vBubHLOC (0),
        vBlbHLOC (0),
        HLOC  (0),
        vBmbHLOC (0),
        emaHLOC (0),
        stdHLOC (0),
        EHLOCupband  (0),
        EHLOCdownband  (0),

        //Keltner
        vKeltUp(0),
        vKeltDown(0),

        //VOLUME
        vVOL(0),
        vAvgVol(0),
        vTicks(0),
        vAvgTicks(0),

        //sqqq and tqqq gap
        TQQQdaychange (0),
        SQQQdaychange (0),
        GapDAYTQQQSQQQ (0),
        GapDAYSQQQTQQQ (0),


        // Trailing
        barCount(0), // count from the first bar
        high1stBar(0), // Extreme high from a list 
        low1stBar(0), // Extreme low from a list 
        trailProfit(0),
        SmallTrailStop(SmallTrail ), //4 pips 
        LargeTrailStop(largeTrail ), //8 pips // 0.01875
        FastTrailStop(0.34),
        intrabarpersist trailExit(0), // F1 Update on every tick
        valuePercentTrail(0),
        is_long_symbol(true),

        //PL for a day
        NetProf(0),
        PLTarget(0),

        //RSI
        vRSI (0), 

        //Zaviot
        MAValue1( 0 ),
        MAValue2 ( 0 ),
        MAValue3( 0 ), 
                
        MASlope1( 0 ), // SHIPOOAA
        MASlope2( 0 ), 
        MASlope3( 0 ), 
                
        MAAngle1( 0 ), // ZAVIT
        MAAngle2( 0 ),
        MAAngle3( 0 ),

        AngleLong(FALSE),
        AngleShort(FALSE),
        BullAngle(FALSE), 
        BearAngle(FALSE),         

        //Donchian
        DonchianUp (0),
        DonchianDown (0),                 

        //Stoch
        oData1FastK( 0 ),
        oData1FastD( 0 ), 
        oData1SlowK( 0 ),
        oData1SlowD( 0 ), 
        stochData1(0),
        stochData2(0),

        //Triangle
        THign  (0),
        TLow (0),
        LTBreak (0),
        STBreak (0);

                        
        //PL for a day
        if DATE <> DATE[1] 
        then 
        begin
        NetProf = NetProf + NetProfit - NetProf[1];
        end;
        PLTarget = Netprofit - NetProf;

                                
        [IntrabarOrderGeneration = True] //trade intra-bar

        emaFast = XAverage(close,FastLength);
        emaMid = XAverage(close,MidLength);
        emaMid30 = XAverage(close,MidLength1);
        emaSlow = XAverage(close,SlowLength);
        emafast1 = XAVERAGE(XAVERAGE(close,FastLength),FastLength);
        demafast = emaFast * 2 - emafast1  ;    
        emaverySlow = XAverage(close,VerySlowLength);
        //ema2Fast = 0;//XAverage(close,FastLength) of data2;
        //ema2Slow = 0;//XAverage(close ,slowLength) of data2;
        //ema2verySlow = 0;//XAverage(close,VerySlowLength)of data2;
        adxcalc = ADX(adxperiod);
        longbuyingPower = 1 ;//(AccountBalance/Close)*PctPerTrade/100; // the amount of shares i can buy //1
        longbuyingPower1 = 5;
        shortbuyingPower = 1 ;
        shortbuyingPower1 = 1 ;

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

        emaHLOC = XAverage (HLOC , BUpperBandHLOC);
        stdHLOC = StdDev(HLOC , BUpperBandHLOC);

        EHLOCupband = emaHLOC + stdHLOC ;
        EHLOCdownband = emaHLOC  - stdHLOC ;


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


        if marketposition = 0 then 
        begin
        //Long Prints - No position - dbug tag
        buydbg= ""; 
        if ((PLTarget < PForDay) and (PLTarget > LForDay))  then
         buydbg = buydbg + "1" else buydbg = buydbg + "X" ;
        if close cross above EHLOCupband  then
         buydbg = buydbg + "2" else buydbg = buydbg + "X" ;
        if close > Open  then
         buydbg = buydbg + "3" else buydbg = buydbg + "X" ;
         if close > open [1]   then
         buydbg = buydbg + "4" else buydbg = buydbg + "X" ; 
        if close < vBub3 then
         buydbg = buydbg + "5" else buydbg = buydbg + "X" ;
        if close <= low *(1+MaxFromLH/100)[1]  
        then buydbg = buydbg + "6" else buydbg = buydbg + "X" ;

        //Short Prints - No position - dbug tag
        selldbg = "";
        if ((PLTarget < PForDay) and (PLTarget > LForDay))  then
        selldbg = selldbg + "1" else selldbg = selldbg + "X" ;
        if close cross below EHLOCdownband  then
        selldbg = selldbg + "2" else selldbg = selldbg + "X" ;
        if close < Open    then
        selldbg = selldbg + "3" else selldbg = selldbg  + "X" ;
        if close < open [1]  then
        selldbg = selldbg + "4" else selldbg = selldbg  + "X" ;
        if close > vBlb3 then
        selldbg = selldbg + "5" else selldbg = selldbg  + "X" ;
        if close >= high *(1-MaxFromLH/100)   then
        selldbg = selldbg + "6" else selldbg = selldbg  + "X" ;


        if marketposition = 0  
        and
        ELDateToString(date) = "05/04/2023" //and symbol = "soxs" //and Time = 1300
        //and (close cross over emaFast  or close cross below emaFast )
        then
        //Long Prints - but No position
        print ( "MOM> symbol=" , symbol," ", "islong=", is_long_symbol,  "no position","  ",
         ELDateToString(date),"Time=", time,"buydbg=", buydbg, "  ", "selldbg=", selldbg,
         "     ","bar=", BarNumber,
        "entryprice=","xxxx.xx", 
        "close=", close, "PLTarget=", PLTarget,
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


        if marketposition = 0 //Conditions Entry Long
        and
        (
        (PLTarget < PForDay) and (PLTarget > LForDay) //1
        )  
        and
        (Time > 1500.00 and Time < 2200.00)
        and
        close > Open //3
        //and
        //close > open [1] 
        //and
        //close [1] < open [1]
        and
        close < vBlb2 //5
        //and
        //close <= LowD(0) *(1+MaxFromLH/100) //entry near to low of the day 
        //and
        //close > high [1]//2
        //and
        //close <= low *(1+MaxFromLH/100) //6
        //and
        //close >= DonchianUp
        //and
        //close cross above EHLOCupband //2
        and
        zscore <= longminzscore 
        and
        (
        (close cross above emaFast ) or (close[1] cross above emaFast [1] )
        )  //J
        and
        close > open [1]
        and
        close [1] <= open [1]
        //pullback
        //(
        //(close [1] <= open [1]) or (close [2] <= open [2])
        //)

        //and
        //triger
        //(
        //(close [3] cross above emaFast [3]) or
        //(close [4] cross above emaFast [4]) or
        //(close [5] cross above emaFast [5]) 
        //(close [6] cross above emaFast [6]) or
        //(close [7] cross above emaFast [7]) 
        //)   


        //and
        //check the price in the choppy zone
        //(low[1] >= evBlb2 and low[2] >= evBlb2)
        //and
        //Close < vBub3 //3
        //and
        //Close < vBub2 //3

        //and
        //close > vwap //2
        //and
        //check channel IS not too tight
        //(vBub2/vBlb2 -1)*100 > Mingap //4
        //and
        //atr > AtrMin //5
        //and
        //atr < Atrmax //6
        //and
        //close [1] < (EHLOCupband+EHLOCdownband)/2 //4
        //and
        //check the price fell to bottom before the pull back in 1-2-3 pre candles
        //(
        //(close [1] cross below EHLOCdownband [1]) or //3
        //(close [2] cross below EHLOCdownband [2]) 
        //)

        //check there is a significant pull back
        //and
        //close > (high[1]+low[1])/2 //4


        //and
        //(
        //stochData1 = 1  //7
        //and
        //oData1FastK > oData1SlowD 
        //and
        //oData1FastK > StochOverSold 
        //and
        //oData1FastK < stochmid
        //and  
        //((oData1FastK [1] < oData1SlowD [1]) or (oData1FastK [2] < oData1SlowD [2])) 
        //and 
        //(
        //(oData1FastK [1] < StochOverSold) or (oData1FastK [2] < StochOverSold) or (oData1FastK [3] < StochOverSold) 
        //)



        //and
        //Close < (EHLOCupband+EHLOCdownband)/Hlocpartlong //7
        //and
        //close [1] < (EHLOCupband+EHLOCdownband)/2
        //and
        //close [1] < EHLOCdownband 
        //and
        //atr > AtrMin //3
        //and
        //absvalue(vBubHLOC - vBlbHLOC) >= MinChanel //3
        //and
        //absvalue(vBubHLOC - vBlbHLOC) <= MaxChanel //4
        //and
        //Ticks > vAvgTicks * (1+volumeUP/100)
        //and
        //AngleLong
        //and
        //BullAngle
        //and
        //close > vwap
        //and
        //close < vKeltUp   //4
        //and
        //vRSI < RSIOverbot //4
        //and
        //close >= emaFast * (1+MinEMAGap/100)//5
        //and
        //close of data2 below emaFast [1] //6
        //and
        //close cross above emaFast //7
        //and
        //close cross above EHLOCupband //8
        //and
        //close  cross above LTBreak
        //and
        //close cross above KUpperBand

        then 
        begin
        buy longbuyingPower Shares next bar at market  ;
        end;


        if marketposition = 1 //Scale In - Conditions Add Entry Long
        and
        close > Open
        and
        close > open [1]
        and
        (
        (close [1] <= open [1]) or (close [2] <= open [2])
        )
        and 
        close cross above emaFast
        and
        (1-close/entryprice)*100 > MinLossForAdd 
        //and
        //(1-close/entryprice)*100 > 0
        //and
        //barssinceentry > 20
        and
        CurShares < maxpositions 
        then 
        begin
        buy longbuyingPower1 Shares next bar at market  ;
        end;


        {
        //buy more after fast minimum profit
        if marketposition = 1 //there is long position open
        and
        (close/entryprice-1)*100 >= SmallMinProfitforadd 
        and
        barssinceentry < MaxBarsforadd
        and
        MarketPosition_at_Broker < maxpositions 
        //and
        //AngleLong = False
        //entryprice >= vBlb2
        then 
        begin
        buy buyingPower Shares next bar at market  ;
        end;
        }

        {
        if marketposition = 1 //add for Long position
        and
        (1-Close/entryprice)*100 >= SmallMinProfitforadd 
        then 
        begin
        buy buyingPower Shares next bar at market  ;
        end;
        }

        {
        if         
        marketposition = 0 //Conditions Entry short
        and
        (
        (PLTarget < PForDay) and (PLTarget > LForDay) //1
        )  //1
        and
        close < Open //3
        //and
        //close < open [1] //4
        //and
        //close [1] > open [1]
        and
        close > vBub2 //5
        and 

        (
        (close cross below emaFast) or (close[1] cross below emaFast [1])
        )  //J
        and
        close < open [1]
        and
        close [1] >= open [1]


        //pullback
        //(
        //(close [1] >= open [1]) or (close [2] >= open [2])
        //)

        //and
        //triger
        //(
        //(close [3] cross below emaFast [3]) or
        //(close [4] cross below emaFast [4]) or
        //(close [5] cross below emaFast [5]) 
        //(close [6] cross below emaFast [6]) or
        //(close [7] cross below emaFast [7])
        //)

        //and
        //close >= high *(1-MaxFromLH/100) //6\
        //And
        //Close <=DonchianDown
        //and
        //close cross below EHLOCdownband //2
        and
        zscore >= shortminzscore 


        //and
        //close >= HighD(0)* (1-MaxFromLH/100)  //entry near to high of the day 
        //and
        //close < Low [1]//2
        //close < Open //2

        //and
        //check the price in the choppy zone
        //(High[1] <= evBub2 and High[2] <= evBub2)
        //and
        //Close > vBlb3 //3
        //and
        //Close > vBlb2 //3
        //and
        //close < vwap //6
        //and
        //check channel is not too tight
        //(vBub2/vBlb2 -1)*100 > Mingap //4
        //and
        //atr > AtrMin //5
        //and
        //atr < Atrmax //6
        //and
        //check the price jump to top before the pull back in 1-2-3 pre candles
        //(
        //(close [1] cross above EHLOCupband [1]) or  //3
        //(close [2] cross above EHLOCupband [2]) 
        //)
        //check there is a significant pull back
        //and
        //close < open [1]
        //and
        //close < (high[1]+low[1])/2 //4

        //and
        //(
        //stochData1 = 1 //7
        //and
        //oData1FastK < oData1SlowD 
        //and
        //oData1FastK < StochOverBot 
        //and
        //oData1FastK > stochmid
        //and  
        //((oData1FastK [1] > oData1SlowD [1]) or (oData1FastK [2] > oData1SlowD [2])) 
        //and
        //(
        //(oData1FastK [1] > StochOverBot) or (oData1FastK [2] > StochOverBot) or (oData1FastK [3] > StochOverBot)
        //)
        //and
        //Close > (EHLOCupband+EHLOCdownband)/Hlocpartshort  //7
        //and
        //close [1] > (EHLOCupband+EHLOCdownband)/2
        //and
        //close [1] > EHLOCdownband 
        //and
        //atr > AtrMin //2
        //and
        //absvalue(vBubHLOC - vBlbHLOC) >= MinChanel //3
        //and
        //absvalue(vBubHLOC - vBlbHLOC) <= MaxChanel //4
        //and
        //Ticks > vAvgTicks * (1+volumeUP/100)
        //and
        //AngleShort 
        //and
        //close < vwap
        //and
        //close > vKeltDown   //4
        //and
        //BearAngle 
        //and
        //AngleShort 
        //and
        //vRSI > RSIoversold //4
        //and
        //close <= emaFast * (1-MinEMAGap/100) //5
        //and
        //close [1] cross above emaFast [1]   //6
        //and
        //Close cross below emaFast  //7
        //and
        //close cross below EHLOCdownband //8
        //and
        //close < STBreak
        //and
        //close cross below KLowerBand

        then 
        begin
        sellshort shortbuyingPower Shares next bar at market  ;
        end;
        }

        {
        if marketposition = -1 //Scale In - Conditions Add Entry Long
        and
        close < Open
        and
        close < open [1]
        and
        close[1] >= open[1]
        and
        close < emaFast
        and
        (1-close/entryprice)*100 > MinProfitforadd 
        //and
        //(1-close/entryprice)*100 > 0
        //and
        //barssinceentry > 20
        and
        CurShares < maxpositions 
        then 
        begin
        sellshort shortbuyingPower1 Shares next bar at market  ;
        end;
        }


        {

        if marketposition = -1 //add for short position
        and
        (1-Close/entryprice)*100 >= SmallMinProfitforadd 
        then 
        begin
        sellshort buyingPower Shares next bar at market  ;
        end;
        }

        {
        //sell more after fast minimum profit
        if marketposition = -1 //there is long position open
        and
        (1-Close/entryprice)*100 >= SmallMinProfitforadd 
        and
        barssinceentry < MaxBarsforadd
        and
        MarketPosition_at_Broker < maxpositions 
        //and
        //AngleLong = False
        //entryprice >= vBlb2
        then 
        begin
        sellshort buyingPower Shares next bar at market  ;
        end;
        }


        //long position prints
        if marketposition = 1 
        and ELDateToString(date) = "05/04/2023" //and symbol = "soxs" //and Time = 1300
        then 
        print ( "MOM> symbol=" , symbol," ",  "in long", "      "
        ,ELDateToString(date),"Time=", time,"buydbg=", buydbg, "     ","bar=", BarNumber,
        "entryprice=",entryprice, 
        "close=", close, "PLTarget=", PLTarget,
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
        and ELDateToString(date) = "05/04/2023" //and symbol = "soxs"//and Time = 1300
        then 
        print ("MOM> symbol=" , symbol," ", "in short","     ", ELDateToString(date),"Time=", time,"selldbg=", selldbg , "     ","bar=", BarNumber,
        "entryprice=",entryprice, 
        "close=", close, "PLTarget=", PLTarget,
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

   	//close long position with trail
	if marketposition = 1
	then
	[IntrabarOrderGeneration = True] //trade intra-bar

	//close long position with trail start moving after small profit in the first bar from entry
	if marketposition = 1 //there is long position open
	and
	(close/entryprice-1)*100 >= SmallMinProfit 
	and
	barssinceentry <= 1
	//and
	//AngleLong = False
	//entryprice >= vBlb2
	then 
	begin
	valuePercentTrail = ((entryprice * SmallTrailStop) /100);
	trailProfit = Highest(high , Barssinceentry); 
	trailExit = trailProfit - valuePercentTrail;        
	sell  next bar at trailExit  stop;
	end;



	//close short position with trail start moving after the first bar from entry
	if marketposition = 0
	then
	begin
	longStop = -9999999;
	end;

	if marketposition = 1 //there is long position open
	and
	(close/entryprice-1)*100 >= SmallbaseProfit 
	and
	barssinceentry > 1
	then
	begin
	// Calculate the trailing stop price
	if low [1] > longStop 
	then
	begin
	longStop = low[1];
	end;
	end;


	//close 1st long position with trail start moving cross back
	if marketposition = 1 //there is long position open
	and
	(close/entryprice-1)*100 >= SmallbaseProfit 
	and
	barssinceentry > 1
	and
	Close < longStop * (1-os1/100)
	Then
	begin
	//crossind = true;
	Sell longbuyingPower Shares Next Bar at Market;
	end;


	//close long position with trail start moving cross back
	if marketposition = 1 //there is long position open
	and
	(close/entryprice-1)*100 >= SmallbaseProfit 
	and
	barssinceentry > 1
	//and
	//Close < longStop * (1-os1/100)
	and
	close cross below emaMid30 
	//and
	//close > lastExitPrice 
	Then
	begin
	Sell Next Bar at Market;
	end;


        {
        //there is long position open and pass too much time without profit
        if marketposition = 1
        and
        (close/entryprice-1)*100 <= MinBaseProfit 
        and 
        barssinceentry > MinBarsForMove 
        then
        sell next bar at low [1]  stop;
        }


        {
        //close long position with trail start moving after large profit when entry price more then 200-2 deviation
        if marketposition = 1 //there is long position open
        and
        (close/entryprice-1)*100 >= largeMinProfit 
        and
        entryprice < vBlb2
        //AngleLong = True
        //entryprice < vBlb2
        then 
        begin
        valuePercentTrail = ((entryprice * LargeTrailStop) /100);
        trailProfit = Highest(high , Barssinceentry); 
        trailExit = trailProfit - valuePercentTrail;        
        sell  next bar at trailExit  stop;
        end;
        }

{
        //close long position after cross ema back
        if marketposition = 1 //there is long position open
        and
        (close/entryprice-1)*100 >= MinBaseProfit 
        and
        Close cross below emaFast  * (1-CrossEMAos/100)
        then 
        begin
        sell  next bar at market;
        end;
}


        {
        //take profit for a part of long position after small profit and move the stop to breakeven for the rest 
        if marketposition = 1 //there is long position open
        and
        (close/entryprice-1)*100 >= SmallMinProfitPart1 
        then 
        begin        
        sell 3         shares next bar at market;
        end;
        }

        ///take profit for a long position when touch middle of the channel
        //if marketposition = 1 //there is long position open
        //and
        //(vBmbHLOC/entryprice-1)*100 >= SmallMinProfitPart1 
        //then
        //begin
        //sell 4 shares next bar at vBmbHLOC limit;
        //end;

        //take profit for a part of long position when touch other side of the channel
        //if marketposition = 1 //there is long position open
        //and
        //(vBubHLOC/entryprice-1)*100 >= SmallMinProfitPart2
        //then 
        //begin        
        //sell next bar at vBubHLOC limit;
        //end;

{
        //take profit when zscore reach target
        if marketposition = 1 //there is long position open
        and
        Zscore >= 0
        then 
        begin        
        sell next bar at market;
        end;
}
        {
        //take profit when zscore reach target
        if marketposition = -1 //there is long position open
        and
        Zscore <= 0
        then 
        begin        
        buytocover next bar at market;
        end;
        }

        //exit when cross back 
        //if marketposition = 1 //there is long position open
        //and
        //Close <= (vBubHLOC *(1-StopLossOS/100))
        //then 
        //begin        
        //sell next bar at market;
        //end;

        {
        //take profit for a short position with trail start moving after small profit when entry price less then 200-2 deviation 
        if marketposition = -1 //there is short position open
        and
        (1-Close/entryprice)*100 >= SmallMinProfit 
        //and
        //AngleShort = False
        //and
        //entryprice <= vBub2
        then 
        begin
        valuePercentTrail = ((entryprice * SmallTrailStop) /100);
        trailProfit = Lowest(low , Barssinceentry); 
        trailExit = trailProfit + valuePercentTrail; //          
        buytocover next bar at trailExit  stop;
        end;
        }

        {
        if marketposition = -1 //there is short position opens and pass too much time without profit
        and
        (1-Close/entryprice)*100 <= MinBaseProfit 
        and
        barssinceentry > MinBarsForMove 
        then
        buytocover next bar at High [1] stop;
        }

        {
        //take profit for a short position with trail start moving after large profit when entry price more then 200-2 deviation 
        if marketposition = -1 //there is short position open
        and
        (1-Close/entryprice)*100 >= largeMinProfit 
        //AngleShort = True
        and
        //entryprice > vBub2
        then 
        begin
        valuePercentTrail = ((entryprice * LargeTrailStop) /100);
        trailProfit = Lowest(low , Barssinceentry); 
        trailExit = trailProfit + valuePercentTrail; //          
        buytocover next bar at trailExit  stop;
        end;
        }

        {
        //close short position after cross ema back
        if marketposition = -1 //there is short position open
        and
        (1-Close/entryprice)*100 >= MinBaseProfit 
        and
        Close cross above emaFast
        then 
        begin
        buytocover next bar at market;
        end;
        }




        {
        //take profit for a part of short position after small profit and move the stop to breakeven for the rest 
        if marketposition = -1 //there is long position open
        and
        (1-Close/entryprice)*100 >=  SmallMinProfitPart1 
        then 
        begin        
        buytocover 3 shares next bar at market;
        end;
        }

        //take profit for a part of short position when touch middle of the channel
        //if marketposition = -1 //there is short position open
        //and
        //(1-vBmbHLOC/entryprice)*100 >= SmallMinProfitPart1 
        //then
        //begin
        //buytocover 4 shares next bar at vBmbHLOC limit;
        //end;

        //take profit for a short position when touch other side of the channel
        //if marketposition = -1 //there is short position open
        //and
        //(1-vBlbHLOC/entryprice)*100 >= SmallMinProfitPart2
        //then 
        //begin        
        //buytocover next bar at vBlbHLOC limit;
        //end;

        {
        //exit when cross back 
        //if marketposition = -1 //there is long position open
        //and
        //Close >= (vBlbHLOC *(1+StopLossOS/100))        
        //then 
        //begin        
        //buytocover next bar at market;
        //end;
        }

        {
        //take profit when zscore reach target
        if marketposition = -1 //there is long position open
        and
        Zscore <= 0
        then 
        begin        
        buytocover next bar at market;
        end;
        }


        //SetProfitTarget;
        if marketposition = 1
        then
        begin
        SetStopLoss(longSL);
        end;

        {
        if marketposition = -1
        then
        begin
        SetStopLoss(shortSL);
        end;
        }










