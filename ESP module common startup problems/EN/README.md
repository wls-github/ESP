##  Prepare an esp-f module of Shenzhen Doit Technology Co., Ltd., or a nodemcu of Doit Technology Co., Ltd


  <img src="../README_IMAGE/1.png" width="400" />
  
 ## 2. Start BOOT analysis.
When ESP8266 is started, the following information will be printed from the serial port from UART0 at a baud rate of 74880.

  <img src="../README_IMAGE/2.png" width="400" />
  
 8266 start log analysis, the general process of running after the program is powered on:
1.Boot mode selection
2. Load the ram rom and verify that the flash is complete
3. Boot jump to the user area and run the program
4. rf initialization, sector selection, the following is the normal user_init program.
ESP8266 has three BOOT modes, which are jointly determined by MTDO (GPIO15), GPIO0, and GPIO2. In boot mode: (3, 7) 3 means boot from flash, 1 means programming code through serial port.

 <img src="../README_IMAGE/3.png" width="400" />
 
 ESP8266 pin level corresponds to the startup mode description of the module:
 
 <img src="../README_IMAGE/4.png" width="400" />
 
 ESP8266 power-up sequence.
   CHIP_EN power-on sequence requirements: CHIP_EN chip enable pin, no internal pull-up, high level is valid. CHIP_EN should be powered on later than or at the same time as the system power 3.3V. Generally, CH-EN has an external RC circuit, and the delay can be about us level.
   After CHP_EN is pulled high for about 60ms, the device determines the boot mode (GPIO15.GPIO0, GPIO2), and then the UART can communicate.
EXT_RSTB: external reset pin, internal pull-up, floating high. EST_RSTB is a level trigger. A low level triggers a chip reset. If it is an external reset signal to the ESP8266EX, the minimum requirement (0.25 VIO.100us).

  <img src="../README_IMAGE/5.png" width="400" />
  
   <img src="../README_IMAGE/6.png" width="400" />
   
   Startup FAQ:
   
   <img src="../README_IMAGE/7.png" width="400" />
   
   Check the information on the serial port UART0 to determine tst cause: 2. If it is other mode, please check if there is any problem with the power supply and module.
boot mode: (3, x) Please confirm if it is in 3 mode. If in 1 mode. Please pull GPIO0 low, if the module is in download mode in 1 mode

 <img src="../README_IMAGE/8.png" width="400" />
 
 If printing waiting for host, please confirm whether GPIO15 is pulled low from 10k to 12k. Remember the power-on sequence. If it has been pulled low, you can add a capacitor to the EN pin to delay power supply.
 
 

   
