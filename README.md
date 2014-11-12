### Photon

The Spark Photon is a tiny WiFi development kit based around USI's WM-N-BM-09 module. This module is a combination of Broadcom's BCM43362 WiFi radio and a STM32F205G microcontroller.

The development kit will have a similar footprint and will be as close to drop-in compatible as possible with the Spark Core.

#### Some highlights of the USI module:

 1. IEEE 802.11b/g/n
 2. Soft AP mode - read smooth WiFi setup process
 3. STM32F205G
 	- 1 MB Flash
 	- 128KB RAM
 	- 120 MHz clock
 4. Measures 12mm x 11mm x 1.3mm

Compared to the Spark Core, the Photon introduces some additional hardware features and changes:

 1. Pin 3V3* is now replaced with VBAT. This pin can be used to power the internal RTC, backup registers and SRAM when the module is put in standby mode.
 2. Pins D1 and D2 can also be used for CAN communication (TX and RX respectively).
 3. Pin A3 now features a DAC (channel 2)
 4. Pin A6 is changed to DAC and exposes a DAC (channel 1).
 5. Pin A7 is changed to WKP (Wakeup). This pin can be used as a standard GPIO, ADC or to WAKEUP (rising edge) the module from sleep/standby modes.

A detailed description of the pin mapping can be found in the pin-mapping folder of this repository.
* Sheet 1: Overview of the pin-out.
* Sheet 2: Detailed description of USI module pin-out and its internal mapping to the microcontroller and WiFi radio.

#### Pin Descriptions:
- **VIN:** This is the power supply pin to the Photon with a voltage range of 3.6 to 5.5VDC (internally regulated down to 3.3VDC). When the Photon is powered via its USB port, this pin will *ouput* a voltage of approximately 4.7VDC. Why 4.7 and not 5? Well, the actual voltage will be the USB voltage, which is normally 5, minus the forward voltage drop (0.3V) of the protection diode.
- **RST:** This is an active-low reset pin for the Photon.
- **VBAT:** Supply to the internal RTC, backup registers and SRAM (1.8 to 3.3VDC).
- **3V3:** This pin is the output of the on-board regulator and is internally connected to the VDD of the WiFi module. When powering the Photon via VIN or the USB port, this pin will *output* a voltage of 3.3VDC. This pin can also be used to power the Photon directly (max input 3.3VDC). **NOTE:** When powering the Photon via this pin, do not put power on the VIN pin.
- **WKP:** This pin allows you to wakeup the module from sleep/standby modes. When not used as a WAKEUP, this pin can also be used as a digital GPIO, ADC input or PWM.
- **D0 - D1:** These are _digital only_ GPIO pins.
- **A0 - A5:** These can be used as digital GPIOs or as ADC inputs.
- **DAC:** This pin can be used as a digital GPIO, ADC input or as a DAC ouput.
- **RX:** Primarily used as UART RX, but can also be used as a digital GPIO, ADC input or PWM.
- **TX:** Primarily used as UART TX, but can also be used as a digital GPIO, ADC input or PWM.

Please review the spreadsheet under the pin-mapping folder to better understand the alternate functions of the GPIO pins.


