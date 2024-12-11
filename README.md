# Test Application for Tibbit#61 (ISOLATED ±10V, 4-20mA ADC Tibbit)
Tibbit#61 offers two differential ±10V voltage inputs and two single-ended current-sinking 0~50mA current inputs. This Tibbit uses a 24-Bit Sigma-Delta ADC.
Tibbit#61-1 has an isolated 24VDC output to enable powering some sensors directly with the Tibbit without the need for any additional power supply. On the other hand, Tibbit#61-2 does not offer this DC-DC converter for cost saving.
The analog front-end and power supplies of both Tibbits are fully isolated.
Both Tibbits are calibrated at factory and calibration parameters are stored on a resident write-protected EEPROM. The library of the Tibbit is responsible to retrieve the calibration parameters from the EEPROM at initialization and use them for conditioning raw values read from the sensor and compensation.

For further information about Tibbit#61, you can see [Tibbit#61-1 documentation](https://docs.tibbo.com/tibbit_61-1) or [Tibbit#61-2 documentation](https://docs.tibbo.com/tibbit_61-2).

This sample offers a test application that can help read the voltage applied to two differential voltage inputs (VIN1 and VIN2) as well as the current that follows into the current inputs (IIN1 and IIN2). Simply you can apply different voltages to the inputs and see their value printed on the console of TIDE. For current inputs you can connect a resistor between 1kOhm ~ 4.7kOhm between 24V output of the Tibbit and one of the current input channels (IIN1 or IIN2) to see the current measurement values between approximately 4mA and 20mA. The current flowing into the input depends on the value of the resistor and 24V output's precise value. You can validate precision using an oscilloscope or a voltmeter.
As another approach, you can connect 0-10V output transmitters (sensors) or 4-20mA transmitters (sensors) to the analog inputs of the Tibbit to have a meaningful and close to a real-world application scenario.
To conclude, this sample application only configures the Tibbit as a voltage and current meter and reads voltage and current values periodically.

> [!TIP]
> Avoid applying any voltages exceeding ±10V to the voltage inputs to different channels and any negative voltage to inputs in single-ended mode as this might damage or degrade the precision of the Tibbit. 


## You Will Need

- A TPP3(G2) board. You can also use any other TPP boards such as TPP2G2; you might need to change the pin assignments in *global.tbh* and change platform settings in TIDE.
- One Tibbit#61-1
- Optionally one Tibbit#10 for the power supply
- Optionally one Tibbit#18 to go along with Tibbit#10
- A voltage source and/or 4-20mA current source

## Connection 
Follow the diagram below for a minimal testing setup of the Tibbit#62:
![The Block diagram of testing Tibbit#61-1](/Diagrams_and_Images/Connection_Diagram.png)

> [!TIP]
> Avoid conencting the TPS ground to the isolated ground. This might lead to damage to your analog sensors, Tibbit61, or TPS.


## The Test Program Flow
In *on_sys_init()*, 
1. The Tibbit is initialized and all voltages and faults of the Tibbit are checked and reported.
2. The VIN1 and VIN2 inputs of the Tibbit are configured as differential mode. And the two current inputs are configured.
3. The calibration parameters are retrieved from the EEPROM to be used for compensation of the offset and non-linearity.

In *on_sys_timer()*, the following process is being repeated periodically:
1. Two differential voltage channels and two current channels are scanned and read for the voltage and current, respectively and the values are printed in Volts and mili-Amperes.


## Useful Links
* [Tibbo Website](https://tibbo.com)
* [Tibbo Project System (TPS)](https://tibbo.com/store/tps.html)
* [AppBlocks — Our No-code Platform](https://appblocks.io)
* [Tibbit #61-1 — Official Product Page](https://tibbo.com/store/tps/tibbits.html#/61-1)
* [Tibbit #61-2 — Official Product Page](https://tibbo.com/store/tps/tibbits.html#/61-2)
* [Tibbit #61-1 — Official Documentation](https://docs.tibbo.com/tibbit_61-1)
* [Tibbit #61-2 — Official Documentation](https://docs.tibbo.com/tibbit_61-2)
* [Tibbit #61 — Tibbo BASIC Library](https://github.com/tibbotech/libraries/tree/main/tibbits/tbt61)
* [Tibbo Support Center](https://tibbo.com/support.html)
