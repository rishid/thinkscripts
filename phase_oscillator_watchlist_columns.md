Watchlist columns with color coding for up, down, and compression along with the PO value.

To add these

1. Go to a watchlist or your MarketWatch tab -> Quotes subtab and click the gear button at the top right of the list (to the very right of the columns)

2. Search for a Custom (Custom1 through Custom19)  column and copy and paste this code in.

```def pivot = ExpAverage(close, 21);
def above_pivot = close >= pivot;
def oscillator_signal = Round(ExpAverage(((close - pivot) / (3.0 * ATR(14))) * 100, 3),2);
def bband_offset = 2.0 * STDev(close, 21);
def bband_up = pivot + bband_offset
;
def bband_down = pivot - bband_offset;
def compression_threshold_up = pivot + (2.0 * ATR(14));
def compression_threshold_down = pivot - (2.0 * ATR(14));
def expansion_threshold_up = pivot + (1.854 * ATR(14));
def expansion_threshold_down = pivot - (1.854 * ATR(14));
def compression = if above_pivot then bband_up - compression_threshold_up else compression_threshold_down - bband_down;
def expansion_zone = if above_pivot then bband_up - expansion_threshold_up else expansion_threshold_down - bband_down;
def expansion = compression[1] <= compression[0];
def compression_tracker = if expansion and expansion_zone > 0 then 0 else if compression <= 0 then 1 else 0;
plot phase_oscillator = oscillator_signal;
phase_oscillator.AssignValueColor(if compression_tracker == 1 then Color.MAGENTA 
                                        else if oscillator_signal >= 0 then Color.GREEN
                                        else Color.RED);```

3. Rename your Custom to PO (Timeframe)

4. Change the timeframe to the desired timeframe that matches 3.

5. Add it as a column.

6. Repeat for other timeframes. I have M/W/D/4H/H/30m/10m/3m/1m (Please note this may affect the performance of your computer, I'm testing it on a pretty fast machine)
