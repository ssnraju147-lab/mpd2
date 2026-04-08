# mpd2

## Firmware 001 — Step 1: VREF Generation (Buffered Mid-Supply)

Use this step to create the ADC reference for ESP32 voltage/current waveform sampling.

1. Build a divider for mid-supply:
   - `3.3V -> 10k -> VREF_NODE -> 10k -> GND`
   - Expected `VREF_NODE` ≈ **1.65V**
2. Buffer the node using **LM358 op-amp A** as a voltage follower:
   - Pin 3 (IN+) -> `VREF_NODE`
   - Pin 2 (IN−) -> Pin 1 (feedback)
   - Pin 1 (OUT) -> `VREF`
3. Add local filtering on `VREF`:
   - `10uF` bulk capacitor (electrolytic/tantalum) to GND
   - `100nF` ceramic capacitor to GND
4. Route this buffered `VREF` as the shared offset for all voltage and current sensing ADC channels.

Result: all AC sensing channels are centered within ESP32 ADC input range.
