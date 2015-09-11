# Photon

The Photon is a tiny WiFi development kit based around USI's WM-N-BM-09 module. This module is a combination of Broadcom's BCM43362 WiFi radio and a STM32F205G microcontroller.

'포톤'은 USI의 WM-N0BM-09 모듈을 기반으로 하는 매우 작은 와이파이 개발 키트입니다. 이 모듈은 브로드컴의 BCM43362 와이파이 라디오와 STM32F205G 마이크로컨트롤러로 구성되어 있습니다. 

The Photon has a similar footprint and is as close to drop-in compatible as possible with the Spark Core.
'포톤'은 스파크의 '코어'와 비슷한 구조를 가지고 있으며 가능한 한 호환이 될 수 있도록 되어 있다.

### Some highlights of the USI module:
USI 모듈의 특징

 1. IEEE 802.11b/g/n
 2. Soft AP mode - read smooth WiFi setup process
 3. STM32F205G
 	- 1 MB Flash
 	- 128KB RAM
 	- 120 MHz clock
 4. Measures 12mm x 11mm x 1.3mm

Compared to the Spark Core, the Photon introduces some additional hardware features and changes:
스파크 '코어'와 비교해보면 '포톤'은 몇가지 하드웨어 기능이 추가, 변화되었다.  

 1. Pin 3V3* is now replaced with VBAT. This pin can be used to power the internal RTC, backup registers and SRAM when the module is put in standby mode.
3V3핀은 VBAT로 바뀌었다. 이 핀은 모듈이 대기모드에 있을 때 내부 RTC, 백업 레지스터, SRAM에 전원을 공급하는데 사용될 수 있다. 
 2. Pins D1 and D2 can also be used for CAN communication (TX and RX respectively).
D1과 D2핀은 CAN통신(각각의 TX와 RX) 을 위해 사용될 수 있다. 
 3. Pin A3 now features a DAC (channel 2)
A3핀은 이제 DAC(채널 2)을 포함하고 있다.
 4. Pin A6 is changed to DAC and exposes a DAC (channel 1).
A6핀은 DAC로 바뀌었고, DAC라고 써져있다.(채널 1)
 5. Pin A7 is changed to WKP (Wakeup). This pin can be used as a standard GPIO, ADC input, PWM or to WAKEUP (rising edge) the module from sleep/standby modes.
A7핀은 WKP(Wakeup)으로 바뀌었다. 이 핀은 표준 GPIO, ADC입력, PWM으로 사용할 수 있으며, 슬립/대기 모드의 모듈을 깨우는데(WAKEUP(rising edge:신호가 0에서 1로 상승하는) 사용할 수 있다. 
A detailed description of the pin mapping can be found in the pin-mapping folder of this repository.
핀 매핑의 상세한 설명은 이 저장소의 pin-mapping 폴더에서 찾을 수 있다.
* Sheet 1: Overview of the pin-out.
시트 1 : 핀 아웃의 개요.
* Sheet 2: Detailed description of USI module pin-out and its internal mapping to the microcontroller and WiFi radio.
시트 2 : USI 모듈 핀 아웃, 마이크로컨트롤러 내부 매핑, 와이파이 라디오의 상세한 설명.

### Pin Descriptions:
핀 설명:
- **VIN:** This is the power supply pin to the Photon with a voltage range of 3.6 to 5.5VDC (internally regulated down to 3.3VDC). When the Photon is powered via its USB port, this pin will *ouput* a voltage of approximately 4.7VDC. Why 4.7 and not 5? Well, the actual voltage will be the USB voltage, which is normally 5, minus the forward voltage drop (0.3V) of the protection diode.
VIN : 이것은 3.6~5.5VDC(내부적으로 3.3VDC로 레귤레이팅 함) 전압 범위를 갖는 '포톤'의 전력 공급 핀이다. '포톤'이 USB 포트를 통해 전력을 공급받을 때 이 핀은 정확히 4.7VDC의 전압을 '출력'할 것이다. 왜 5가 아닌 4.7일까? 자, 실제전압은 USB 전압(보통 5볼트)에서 보호다이오드의 순방향 전압 강하(0.3볼트)를 뺀다.
- **RST:** This is an active-low reset pin for the Photon.
- RST : 이것은 포톤의 acrive-low 리셋핀이다.
- **VBAT:** Supply to the internal RTC, backup registers and SRAM (1.8 to 3.3VDC).
VBAT : 내부 RTC, 백업 레지스터, SRAM에 전원(1.8 ~ 3.3VDC) 공급.
- **3V3:** This pin is the output of the on-board regulator and is internally connected to the VDD of the WiFi module. When powering the Photon via VIN or the USB port, this pin will *output* a voltage of 3.3VDC. This pin can also be used to power the Photon directly (max input 3.3VDC). **NOTE:** When powering the Photon via this pin, do not put power on the VIN pin.
3V3 : 이 핀은 온보드 레귤레이터의 출력이며 내부적으로 와이파이 모듈의 VDD(드레인 전원)와 연결되어 있다. VIN이나 USB포트를 통해 포톤에 전원을 공급할 때 이 핀은 3.3VDC의 전압을 '출력'할 것이다. 이 핀은 또한 직접포톤에 전원을 연결(최대 입력 전압 3.3VDC)하기 위해 사용하기도 한다. *NOTE : 이 핀을 통해 포톤에 전원을 공급할 때 VIN 핀으로 전원을 연결하지 말 것. 
- **WKP:** This is an active-high input that allows you to wakeup the module from sleep/deep sleep modes. When not used as a WAKEUP, this pin can also be used as a digital GPIO, ADC input or PWM.
WKP : 이것은 당신이 슬립/딥슬립 모드의 모듈을 켜기 위한 active-high 입력핀이다. WAKEUP으로 사용하지 않을 때 이 핀은 또한 디지털 GPIO, ADC입력 또는 PWM으로 사용할 수 있다. 
- **D0 - D7:** These are _digital only_ GPIO pins.
D0 - D7 : 이 핀들은 오직 digital GPIO로만 동작한다. 
- **A0 - A5:** These can be used as digital GPIOs or as ADC inputs.
A0 - A5 : 이 핀들은 digital GPIO 또는 ADC입력으로 사용할 수 있다. 
- **DAC:** This pin can be used as a digital GPIO, ADC input or as a DAC ouput.
DAC : 이 핀들은 digital GPIO, ADC입력 또는 DAC출력으로 사용할 수 있다. 
- **RX:** Primarily used as UART RX, but can also be used as a digital GPIO, ADC input or PWM.
RX : 기본적으로 UART RX로 사용하나, digital GPIO, ADC입력 또는 PWM으로 사용할 수 있다. 
- **TX:** Primarily used as UART TX, but can also be used as a digital GPIO, ADC input or PWM.
TX : 기본적으로 UART TX로 사용하나, digital GPIO, ADC입력 또는 PWM으로 사용할 수 있다. 

Please review the spreadsheet under the pin-mapping folder to better understand the alternate functions of the GPIO pins.
GPIO핀의 다른 기능들에 대한 더 나은 이해를 위해서는 pin-mapping 폴더 안의 스프레드시트를 확인하시오.

### Eagle (schematic and pcb layout):
이들(회로도와 PCB 레이아웃):
Under the `eagle` folder, you'll find the history of Photon designs.
'eagle' 폴더에서 당신은 포톤 설계의 역사를 확인할 수 있다. 
 1. **cam-drc:** Contains CAM Jobs (for creating gerbers) and DRC (Design Rule) files.
cam-drc : CAM작업(PCB기판을 뜨기 위한 거버 파일 생성을 위한)과 DRC파일(설계규칙)을 포함한다.
 2. **photon_v001:** The initial photon design.  This version of the design uses the same dimensions as the Spark Core and provides through-hole headers for mounting.
photon_v001 : 초기 '포톤' 설계. 이 설계버전은 스파크 '코어'와 동일한 치수를 사용하며, 장착을 위해 스루홀헤더(관통구멍)를 제공한다. 
 3. **photon_v010:** Several versions later, numerous tweaks and additions to the schematic, smaller less blinding RGB LED, aligned D7 LED with D7 pin, new SMPS voltage regulator, castellated and non-castellated have been merged, new slightly larger higher gain antenna, Bluetooth Co-existance pins are broken out to pads for a 1.27mm pitch (0.050") connector, pads on the bottom side of the board were added for the RGB LED, and MODE button connections and are centered on the 0.1" grid, and RF switch for software selection of u.FL vs Chip Ant. RF Test board's for versions are included to make tuning of matching components in RF stage easier. There is a second Photon design here with antenna scooted to the left 0.027" to give more clearance between D0 pin and antenna.  C1 in Pi filter was removed to make room for this tighter layout.
photon_v010 : 몇몇 버전 이후, 작고 눈부신 RGB LED, D7 핀과 D7 LED의 연동, 새로운 SMPS 전압 레귤레이터, 성곽 모양과 비성곽 모양의 통합, 새로운 조금 더 높은 성능의 안테나, 블루투스 공존 핀은 1.27mm 피치(0.050") 커넥터를 위해 면에서 튀어나옴, 보드의 아래쪽 면은 RGB LED를 위해 추가, MODE버튼이 연결되었고 0.1"격자에 집중됨, 그리고 u.FL과 칩 안테나의 소프트웨어적 선택을 위한 RF 스위치, 버전의 RF 테스트 보드는 RF 단계에서 구성요소의 매칭을 쉽게 튜닝할 수 있도록 포함되는 등 설계에 많은 기능의 변화와 추가가 있었다. 안테나에 대한 두번째 '포톤' 설계는 D0핀과 안테나 사이의 간격을 두 주기 위해 왼쪽으로 0.027" 이동하였다. 

 4. **photon_v019:** Several more versions later, numerous tweaks and additions to the schematic, WM-N-BM-09 soldermask updated, added some GND vias, MODE button label changed to SETUP, increased width of top and bottom (short) sides of PCB 20 mils to allow for v-score (overall board height is now 1.44"), SETUP and RESET buttons and RGB led are not centered on the 0.1" grid anymore but they are all still inline with each other, RF switch was changed to a much smaller 1mm version, 0201 dc blocking capacitors added to all RF ports, Pi filter was tuned to match antenna to 50 ohm impedance, half of the pads on the bottom were enlarged to 60 mils square, added fabrication spec.
photon_v019 : 몇몇 버전 이후 WM-N-BM-09의 솔더마스크 업데이트, GND 바이어스 추가, SETUP을 위한 MODE 버튼의 레벨 변화, v-score를 허용하기 위해 PCB 20밀리의 짧은쪽 상판과 하판의 폭 증가(현재 전체보드의 높이는 1.44"), SETUP과 RESET버튼과 RGB LED는 더이상 0.1"격자의 중심에 있지 않으나 여전히 각각 한줄로 있음, RF 스위치는 훨씬 더 작은 1mm버전으로 바뀌었고, 0201 dc 블로킹 캐패시터가 모든 RF 포트에 추가됨, 파이 필터는 50옴 임피던드 안테나에 맞게 조정되었고, 아랫면의 절반은 60제곱밀리미터로 확대되었으며, 제조사양이 추가되는 등 설계에 많은 기능의 변화와 추가가 있었다. 

#License
라이센스

Designed by Spark IO. Distributed under a Creative Commons Attribution, Share-Alike license.
Spark IO에서 설계함. Crearive Commons 저작자 표시에 따라 배포, 동일 조건 변경허락.
Development kits based on this product should be distributed under a similar license.
이 제품을 기반으로 한 개발 키트는 같은 라이센스 조건하에서만 배포할 수 있다. 
Commercial products using the Photon as a reference design need not comply with this license; further questions can be sent to hello@particle.io.
레퍼런스 디자인으로 '포톤'을 사용한 상용 제품은 이 라이센스를 준수할 필요가 없다; 추가 질문은 hello@particle.io로 보낼 수 있다. 
Check license.txt for more information.
더 많은 정보를 위해서는 license.txt를 확인한다.
