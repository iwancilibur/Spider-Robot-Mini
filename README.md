# Spider-Robot-Mini

This is an inexpensive 3D printed 12 DOF quadruped robot using Arduino kind control board. It has two playing modes. One is autonomous pilot mode which the robot walks and performs actions randomly. This is the default. The other is control mode where the robot is controlled by iPhone or Android phone via BLE technology. The assembly videos at below should guide everyone to make one easily. They are also available in
https://www.instructables.com/id/Ez-Arduino-Spidey-Making-a-12-DOF-3D-Printed-Quadr/
.

It is based on our another quadruped robot design
https://www.thingiverse.com/thing:2901132

is a bigger size versoin. We also have a design of hexapod robot
https://www.thingiverse.com/thing:3650641
. Perhaps, you will be interested to make them too.

https://www.thingiverse.com/thing:4153131

https://www.thingiverse.com/thing:3099712

if you want to use Infrared remote control to control Spidey instead of using BlueTooth BLE module and Apps.
https://www.thingiverse.com/thing:3624838

if you want to make the Bluetooth gamepad to control Spidey
Video Demos:

    https://youtu.be/fOYrCuP1R1U
    https://youtu.be/d3f_IFLi8i4
    https://youtu.be/FgAnbn1XKww
    https://youtu.be/LLlxMSZ1ZfE

Software:

Robot Code -

    Arduino code on githup

Control Apps -

    goBLE iOS app on Apple Store; for Bluetooth LE module
    playBLE Android app on Google Play; for Bluetooth LE module
    virtual-Gamepad-BLE Android app contributed by a supporter for Bluetooth LE module; compatible to Android 5.0 and latest.
    virtual-gamepad-SPP Android app contributed by a supporter for HC-06, HC-05 and SPP-CA classic Bluetooth 4.0 SPP module; compatible to Android 4.0 and above

Hardware:

The components can be found in ebay, amazon, aliexpress, DX and etc online store.

    a HuaDuino board, it is Arduino Nano compatible with enhanced features. It integrates everything on a single PCB. It's a lot easier for people to make a bot with it. Embedded battery charging circuit, battery charging is more convenient. It can be found on ebay.
    a single 3.7V 18650 lithium ion battery or battery pack with XH2.54 connector, if you want longer running time getting a pack with two 18650 in parallel. For this robot, you may like to use our design 18650 battery holder. However, it is also fine to use 3.7V 10440 lithium ion and 3.7V lithium polymer battery dimension not bigger than W35mm, L70mm & T60mm.
    12 x Tower Pro SG90 or compatible 9g servos.
    a female-female dupoint wire or anything you can figure out for connecting two pins
    some m2x6 tapping screws

Bluetooth Module

    a HC-06, HC-05 and SPP-CA classic Bluetooth 4.0 SPP module, if you use this type of Bluetooth module; must use the virtual-gamepad-SPP Android app for control; baud rate must be set to 115200; see this tutorial to configure the baud rate using AT commands;
    Or
    a BT-05 CC2540 Bluetooth LE module - this is optional if you don't need App control. In fact, there are many BLE modules named differently, but they are built with CC254x chip. Examples such as HM-10 and CC41-A are the typical you can find in the market. Since the firmware is different, the AT command set may vary too. You may use this code to identify them. To work with the robot code and the apps, baud rate is required to set to 115200; service UUID must set to 0xDFB0 and characteristic UUID must set to 0xDFB1 using the AT commands. Below is the code intended to do that automatically but it may not work if you have different one.. The reference of the AT command set to configure BT-05 BLE can be downloaded here. You don't need this module if you like to make this gamepad to control and play Spidey.

Below only required for Bluetooth LE module

The following stand alone Arduino program issues AT commands setting BT-05 BLE module service UUID, characteristic UUID and baud rate, assuming the BLE default baud rate is 9600. For running below code in HuaDuino with the module onto it, the S1 switch must be set to the BT position.

void setup() {
  Serial.begin(9600); //change to fit your ble initial baud_rate, usually is 9600
  Serial.println("AT+UUID0xDFB0\r"); //  set service UUID
  delay(50);
  Serial.println("AT+CHAR0xDFB1\r"); // set characteristic UUID
  delay(50);
  Serial.println("AT+BAUD8\r");  // set baud rate to 115200
}
void loop() {}

The steps you should do of uploading the Arduino sketch to HuaDuino for BLE control are as following

1) insert the BLE module, switch S1 to USB side, turn on huaduino,
2) uploading the above ble module setup program
3) turn off huaduino, switch S1 to BT side
4) turn on huaduino, let the ble module setup program run in few seconds.
5) switch S1 to USB side
6) uploading the robot code by open "firmware.ino"
7) switch S1 back to BT side, the robot now can be controlled by BLE

for HuaDuino, in Arduino IDE software:

    the board selection should be "Arduino Nano", processor "ATmega328" for AVR Boards support version 1.6.20 or older.
    the board selection should be "Arduino Nano", processor "ATmega328 (Old Bootloader)" for AVR Boards support version 1.6.21 or newer.
