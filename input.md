	//@version=31323-2
	Inputs:
	maximumloss(0.143), //120 //160
	FastLength(9),
	MidLength(20),
	MidLength1(30),
	SlowLength(50),
	AssetMultiplier (2), //2=micro , 20=mini
	length (5),
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
	MaxFromSR (0.2),
	MaxFromLHEntry (0.75),
	MinFromLHentry (0.15),
	MinKeltnerCross (0.08),
	MinemaGap (0.0005), // 0.01875
	MaxemaGap (0.025), //0.22  
	Mingap (0.2), //0.06 was too tight according to 8.3.23 , 3:03 AM //0.15
	Mingap1 (0.01),
	Maxgap (0.12), //0.O5
	Maxgap1 (0.2), //0.2 //0.02 //0.2
	Maxgap2 (0.05), //0.2
	maxgap3 (0.09),
	maxgap4 (0.26),
	maxgap5 (0.1), 
	
	MinProfit (0.00625),
	smallbaseProfit (0.033), //0.035 //0.19 //0.02 //0.1 //0.5 //CROSS1:0.033 (5P)
	smallbaseProfit1 (0.059), //0.035 //0.19 //0.02 //0.1 //0.5 //CROSS2:0.059 (9P) 
	SmallMinProfit (0.133), //after 12 pips start trail of 4 pips //0.075 with stochastic //0.1 //TRAIL PCT FROM 5P //0.033
	SmallMinProfit1 (0.05), 
	largeMinProfit (0.44), //after 10 pips start trail of 8 pips //0.09375
	SmallMinProfitPart1 (0.05), //after 3 pips limit 3 at the middle of the chanel //0.05
	Smallbaseloss (0.03),
	SmallMinProfitPart2 (0.0375), //after 6 pips limit at the other side of the channel
	MinProfitforadd (0.01),
	MaxProfitForAdd (0.1),
	FastMinProfit (0.0625), //0.1125
	MinBaseProfit (0.03),
	MinLossForAdd (0.1), //0.1
	SmallTrail (0.02), //0.04375 with stochastic //0.00625 //0.0125 //0.025 //0.01875 //TRAIL SPREAD: 0.5P //0.0033
	largeTrail (0.09),
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
	Atrmax (15),
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
	ppLength (5),
	os1 (0.0133), //0.03 - offset 
	os2 (0.01),
	os3 (0.0133), // 2$ - 0.133 precent 

	PForDay (6000), //1500 //1950 //100 //800 //15000
	LForDay (-800), //-1100 //-500 //-50 //-2000

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

	//Zscore
	longminzscore (-2),
	shortminzscore (2);
