#region Using declarations
using System;
using System.ComponentModel;
using System.ComponentModel.DataAnnotations;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using NinjaTrader.Cbi;
using NinjaTrader.Data;
using NinjaTrader.Gui;
using NinjaTrader.Gui.Chart;
using NinjaTrader.Gui.SuperDom;
using NinjaTrader.Gui.Tools;
using NinjaTrader.Data.BarsTypes;
using NinjaTrader.NinjaScript;
using NinjaTrader.Core.FloatingPoint;
using NinjaTrader.NinjaScript.Indicators;
using NinjaTrader.NinjaScript.DrawingTools;
#endregion

namespace NinjaTrader.NinjaScript.Strategies
{
    public class MyStrategy : Strategy
    {
        private SMA smaFast;
        private SMA smaMid;
        private EMA ema3VerySlow;
        private EMA emaVerySlow;
        private SMA smaSlow;
        private EMA emaSlow;
        private EMA emaMid;
        private EMA emaFast;
        private EMA emafast1;
        private double demafast;
        private double ema1preFast;
        private double ema2preFast;
        private double ema2Fast;
        private double ema2Slow;
        private double ema2verySlow;
        private double ema2mid;
        private RSI rsiSlow;
        private RSI rsiFast;
        private ATR atr;
        private ADX adxcalc;
        private double longbuyingPower;
        private double shortbuyingPower;
        private double longbuyingPower1;
        private double shortbuyingPower1;
        private double longbuyingPower2;
        private double shortbuyingPower2;
        private double curProfit;
        private double TakeProfitAmt;
        private double StopAmt;
        private int CurShares;
        private BollingerBands bb1;
        private BollingerBands bb2;
        private BollingerBands bb3;
        private BollingerBands bbHLOC;
        private MACD macd;
        private KeltnerChannel keltner;
        private Stochastic stochastic;
        private double AccountBalance = 10000;
        private double PctPerTrade = 50;
        private double TakeProfit = 200;
        private double TakeProfitPct = 6.5;
        private double StopPct = 0.025;
        // Define your other variables here...

        protected override void OnStateChange()
        {
            if (State == State.SetDefaults)
            {
                Description = "My Strategy";
                Name = "MyStrategy";
                Calculate = Calculate.OnBarClose;
                // Set your other default values here...
            }
            else if (State == State.Configure)
            {
                // Initialize and add your indicators here...
                smaFast = SMA(FastLength);
                smaMid = SMA(MidLength);
                ema3VerySlow = EMA(VerySlowLength);
                emaVerySlow = EMA(VerySlowLength);
                smaSlow = SMA(SlowLength);
                emaSlow = EMA(SlowLength);
                emaMid = EMA(MidLength);
                emaFast = EMA(FastLength);
                emafast1 = EMA(FastLength);
                rsiSlow = RSI(RsiSlowLength);
                rsiFast = RSI(RsiFastLength);
                atr = ATR(AtrLength);
                adxcalc = ADX(adxperiod);
                bb1 = BollingerBands(BUpperBand, BLowerBand);
                bb2 = BollingerBands(BUpperBand, BLowerBand);
                bb3 = BollingerBands(BUpperBand, BLowerBand);
                bbHLOC = BollingerBands(BUpperBandHLOC, BLowerBandHLOC);
                macd = MACD(macdFastLength, macdSlowLength, MACDlineLength);
                keltner = KeltnerChannel(KUpperBand, KLowerBand, KStdAtr);
                stochastic = Stochastic(StochPiriod1, StochLength1, StochLength2);

                // Set up your other indicators here...
            }
        }

        protected override void OnBarUpdate()
        {
            // Implement your trading logic here...
            if (FirstTickOfBar)
            {
                // Perform calculations and actions on the first tick of the bar
                // Example:
                if (MarketPosition == MarketPosition.Flat)
                {
                    CurShares = 0;
                }
                
                // Implement your other first tick calculations here...
            }

            // Implement your other bar update logic here...
        }
    }
}
