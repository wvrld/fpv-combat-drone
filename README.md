# How to build FPV Combat Drone



Note : This tutorial contains content that could raise legal and ethical concerns. Please obtain guidance from legal experts or authorities in your country to ensure compliance with relevant laws and ethical standards.

In this tutorial, there will be no photos. Sorry, i wanna stay anonymous. 

# Speedy Bee F405 V3 Stack

The Speedy Bee F405 V3 is a flight controller and power distribution board designed specifically for FPV drones. It is equipped with an F4 processor, which provides fast and efficient performance for controlling the drone’s flight and with variety of ports and connectors for easy integration with ESC, receivers/transmitters, and the FPV camera. You will later see how easy it is to use.

link - https://www.speedybee.com/speedybee-f405-v3-bls-50a-30x30-fc-esc-stack/

Everything we need will be listed below. 

## Drone Components
  
- Mark 4 7'’ frame, video-camera Caddx Ratel 2 12000 TVL and 915 MHz receiver Express LRS Nano
- video transmitter VTX AKK Race Ranger 1.6W
- 4x EMAX ECOII Series ECO II 2807 6S 1300KV
- FPV antenna Lollipop 4 V4 SMA 10cm
- Propellers HQPROP 7035 7x3.5x3

## Drone Kit

- Li-ion Long range pack 6s2p — 9000 mAh
- 5.8G FPV Goggles 40CH X BAND
- RadioMaster Bandit Micro ELRS 915 MHz Radio Adapter
- RadioMaster TX12 Mark II Radio Controller

## Add-ons

- Beitian BN-220 GPS module and Buzzer
- Drop system for FPV on Mark 4 frame 7"

# Mark 4 frame assembling

The first step is the easiest one. You simply unfold all the items from the Mark 4 frame package and assemble it. Everything you need is just a screwdriver (M3) and the Mark 4 7" Schematic.

Professionals recommend not tightening the bolts at this stage. You will do that later, after soldering and assembling the entire drone. Simply screw the bolts softly with a hex-screwdriver M3 and enjoy the process.

# EMAX motors installing

When the frame is ready, the next step is preparing and installing the motors. I used EMAX ECOII Series ECO II 2807 6S 1300KV and a special protective coverage for the motor wires.

At this step, it is recommended to use a hex-screwdriver (M3) to install the motors without tightening the bolts. We will do so later.

# Power supply cable soldering

And here we are. This is perhaps the most challenging part of the job — soldering the power cables. It’s beneficial if you have any experience in soldering, otherwise, I would recommend searching on YouTube and watching the video ‘How to solder the power supply wires to FC’.
https://www.youtube.com/watch?v=rGUxVsbSl2c

Remember to solder the 1000uF low ESR Capacitor included in the Speedy Bee F405 V3 Stack package. Connect the Red wire to red (+) and the Black wire to black (-). This is necessary to protect the ESC board.

# EMAX motors soldering

After finishing soldering the motors to the board, you need to use a multimeter to test all the contacts. Please note that contacts from different motors should not be connected or show continuity.

At this stage, you can already connect the ESC to the FC with an 8-pin cable and link the entire device to a computer with Betaflight Configurator (using a USB cable) to pre-test the motors. 

# VTX and camera setup

According to the wiring diagram on the official website of Speedy Bee, the Video Transmitter VTX AKK Race Ranger 1.6W should be connected to the 9V, G, VTX, and T1 pins on the first UART port of the FC. T1 means that this is a TX from UART1. 

Always double-check all the pins when connecting any peripheral device to the flight controller because they may vary from device to device. For the VTX, we use red (1) and black (2) wires, as well as yellow (5) and green (6). The internal red (3) and black (4) wires should not be used. I have isolated them. These may be used to connect to the video camera directly, but we will be using the FC to connect with the camera through that.

Video-camera Caddx Ratel 2 12000 TVL connects to the flight controller using 5V, G, and CAM pins. Red (1) to 5V, Black (2) to G, and Yellow (3) to CAM.

After soldering all the necessary connections, you can proceed to connect the FPV system either to your computer or directly to the battery for testing. If there is no smoke, congratulations, you have completed the work correctly. From this point, you can even turn on your FPV glasses and search for the channel to search your FPV drone. It should already be operational by this point if UART1 is configured correctly. 

And don’t forget to connect your FPV antenna, Lollipop 4 V4 SMA 10cm, if you power on the VTX. Otherwise, there is a chance it could burn down.

# ELRS receiver setup

The ELRS receiver is used to connect your drone with the Radio Controller. The operator manages the drone’s direction, speed, turns, altitude, and everything else using this radio controller. It is the primary device for controlling the drone.

According to the official documentation, it should be connected to UART2 on the FC board. Double-check which one you use and connect it according to the specification. In my case, as I am using Express LRS Nano, so that I connected Black to G, Red to 4V5, White to R2, and Yellow to T2.

But before that, I also soldered these wires to the ELRS receiver exactly and double-checked that TX from the receiver should be connected with RX (R2) on the controller. At the same time, RX on the receiver should be connected to TX (T2) on the controller.

Once you have done this, you can power on your FC and pair the device with your RadioMaster TX12 or analog radio controller to check its functionality and readiness.

# Software Part

Alright, we’ve completed the soldering, so we’re good to move on. Next up, let’s configure the parameters for our Drone. To do that, you’ll need to download the Betaflight Configurator for your operating system and connect your drone to the computer via USB.

On the first screen you will likely see the image of your drone and some general information. We skip this page and go to the ‘Ports’ tab to properly check and setup parameters.

Since we’ve soldered the VTX on UART1, we need to select one of the VTX-related types from the list under the ‘Peripherals’ section. In my scenario, since the Race Ranger VTX utilizes the SmartAudio protocol, I’ve opted for ‘VTX (TBS SmartAudio)’. In your case just try one of the VTX here.

The next page is the ‘Configuration’, where we need to enable the following:

- Enable ‘Accelerometer’ and ‘Barometer’;
- Set up your craft’s name instead of ‘UA-914’ displayed on my screen;
- Enable arming even under angle (180 degrees);
- Enable ‘RX_LOST’ and ‘RX_SET’ for audible alerts.

Later, when setting up the Drop system with servo drive, we’ll also enable ‘SERVO_TILT’ in the ‘Other Features’ section to enable the drone to work with servo drive (for bombing).

In the ‘Power & Battery’ section, you’ll likely need to configure the following settings:
- Minimum cell voltage: 3.0
- Maximum cell voltage: 4.2
- Warning cell voltage: 3.1
These settings are ensuring correct operation with the power supply.

PID (Proportional-Integral-Derivative) profiles determine how the flight controller responds to various inputs and disturbances during your flight.

By adjusting these PID profile settings, you can optimize the flight performance of the drone, achieving better stability, maneuverability, and responsiveness.

‘Rate Profile Settings’ control how sensitive and responsive the drone is to stick movements, particularly regarding its rate of rotation or change in direction. These settings essentially dictate how quickly the drone reacts to pilot inputs. The default value for parameters highlighted in red is 620, but let’s set it to 490 to increase performance.

By adjusting ‘Filter Settings’, you can effectively reduce noise and vibrations in the sensor data, resulting in smoother flight performance, improved stability, and better control responsiveness.

The ‘Receiver’ section is used to configure how the flight controller communicates with the receiver unit, in our case ELRS 915 MHz Nano, which receives commands from the RadioMaster TX12 radio controller.

Since we’ve soldered our receiver to UART2 as configured in the ‘Ports’ section above, we only need to adjust a few parameters on this page:

- Receiver mode: Serial via UART;
- Serial Receiver Provider: CRSF;
- Enable ‘Telemetry’ to display key data on the radio controller;
- Channel Map: AETR1234.
Please note that when setting up the RadioMaster TX12, choose the CRSF protocol, which we have configured in the flight controller.

Adding an ‘ARM’ mode in the ‘Modes’ section allows you to control when the drone is armed or disarmed. To set this up, you need to bind your RadioMaster TX12 Radio Controller with the drone during configuration. Then, click on ‘Add Link’ next to the ‘ARM’ command, and toggle the switch on/off on the Radio Controller that you want to use for ARM/DISARM. This action configures it accordingly.

Also, using the yellow scroll, you can specify the tumbler state in which the drone will be armed. And don’t forget to save changes in the right bottom corner of the configuration page.

The ‘Motors’ section has tools for testing and resolving issues with the motors on your drone. It enables you to individually activate each motor to confirm their proper functionality and configuration.
For our setup, we should select the following options:
- Mixer: QUAD X;
- Motor protocol: DSHOT600.

As a part of motor testing, it permits you to confirm the functionality of each motor, adjust their output as needed, and ensure they spin in the correct direction for optimal flight control. Remember to utilize this feature safely by conducting tests without propellers installed on your drone to prevent any potential damage.

The OSD (On-Screen Display) section allows you to configure and customize the on-screen display settings for your FPV (First Person View) video feed displayed on your video monitor or goggles.
I would recommend to setup the following:
- Altitude (without decimals);
- Artificial horizon sidebars;
- Battery usage (graphical remaining);
- Craft name;
- Flight mode;
- Link quality;
- Warnings.

n addition to displaying various parameters on the screen, you can also drag and drop them to the specific location on the screen.

Overall it provides essential flight information at a glance, enhancing your situational awareness and overall flying experience. Properly configuring the OSD can help you monitor important telemetry data and make informed decisions while piloting the drone.

The VTX is responsible for transmitting the video feed from your drone’s onboard camera to your FPV (First Person View) goggles or video receiver. As you remember we have soldered our video transmitter to UART1 on FC.

Our AKK Race Ranger 1.6w has a specific VTX table which you have to download from the file. Look at the example below:

```json
{
    "description": "AKK Race Ranger VTX Config file",
    "version": "1.0",
 "vtx_table": {
        "bands_list": [
            {
                "name": "BOSCAM_A",
                "letter": "A",
                "is_factory_band": true,
                "frequencies": [
                    5865,
                    5845,
                    5825,
                    5805,
                    5785,
                    5765,
                    5745,
                    5725
                ]
            },
            {
                "name": "BOSCAM_B",
                "letter": "B",
                "is_factory_band": true,
                "frequencies": [
                    5733,
                    5752,
                    5771,
                    5790,
                    5809,
                    5828,
                    5847,
                    5866
                ]
            },
            {
                "name": "BOSCAM_E",
                "letter": "E",
                "is_factory_band": true,
                "frequencies": [
                    5705,
                    5685,
                    5665,
                    5645,
                    5885,
                    5905,
                    5925,
                    5945
                ]
            },
            {
                "name": "FATSHARK",
                "letter": "F",
                "is_factory_band": true,
                "frequencies": [
                    5740,
                    5760,
                    5780,
                    5800,
                    5820,
                    5840,
                    5860,
                    5880
                ]
            },
            {
                "name": "RACEBAND",
                "letter": "R",
                "is_factory_band": true,
                "frequencies": [
                    5658,
                    5695,
                    5732,
                    5769,
                    5806,
                    5843,
                    5880,
                    5917
                ]
            }
        ],
        "powerlevels_list": [
            {
                "value": 0,
                "label": "200"
            },
            {
                "value": 1,
                "label": "400"
            },
   {
                "value": 2,
                "label": "800"
            },
               {
                "value": 3,
                "label": "1600"
            }
        ]
    }
}
```

If you have any other VTX, you should find an appropriate VTX table and load it in this section by clicking on the ‘Load from file’ button. Once you’re done with this, you can proceed to choose the following settings:
- Band: RACEBAND;
- Channel: 1;
- Power: 200.

Also, enable ‘Low power disarm’ to conserve energy when the aircraft is disarmed and stay on the ground surface. Each time you do any changes don’t forget to save them clicking ‘Save’ button usually located in the right bottom corner of the configuration section page.

# Propellers installation
When you are done with all the configuration in Betaflight, you are ready to tighten bolts, install the battery onboard, and attach the propellers. Installing propellers is crucial for a successful flight. Installing them in the wrong direction can cause the drone to flip or sustain damage on its first flight. So, be careful.

In our configuration, we use the direct mode for motors. This means that the front left and back right motors rotate to the right side as [clockwise]. The right front and left bottom motors rotate [counterclockwise] to the left side. 

Each blade on the propeller has two sides: the side forming the top and the one at the bottom. The propeller should be installed on the motor so that the upper part of the blade faces the direction of motor rotation.

Tighten the nuts securely on all motors, but be careful not to over-tighten, as this can damage the motor or propeller. When done, ensure that everything is installed correctly, open the camera, bind with Radio Controller and Goggles, and you are ready for the first flight.

# Drop system installation
The Drop System is the final step of configuration which transforms our standard drone into a *military-grade tool*, enabling the deployment of bombs. From a technical prospective, it includes a servo mechanism capable of holding and releasing bombs when the operator switches the toggle to the bombing position.

I’ve connected the servo mechanism to the flight controller as follows:
- Red wire of servo is soldered to the 5V pin on the top right corner of FC;
- Black wire of servo is soldered to the G pin on the top right corner of FC;
- Yellow wire of servo is soldered to the S9 pin on the FC.
- 
Once you done with soldering you have to configure these last things in the Betaflight Configurator.

As we are using the 5V and G pins from the LED strip of the FC, we also need to enable them in the configuration by enabling LED_STRIP. Additionally, enabling SERVO_TILT allows us to configure the servo mechanism on one of the toggles.

I have selected mid (1500), min (1100), and max (1900) values for Servo 1, determining its angle of rotation. Additionally, I’ve configured A2 (AUX2 toggle) to serve as the bombing function.

Remember to save changes in all sections once you’ve finished configuration. Now, disconnect your drone from the computer, connect it to the battery, insert a tennis ball into the servo mechanism instead of a bomb, and test it using your RadioMaster TX12 radio controller.

## And thats it. You built military-grade drone. 

Legal and Ethical Considerations in Other Countries:

I know this platform is global, and building and using drones might not be legal in some countries. Therefore, I want to guide you through legal and ethical issues.

* While building and donating a drone itself may not be illegal in some countries, there are several legal and ethical aspects to consider: *

Exporting military-related technology or equipment, even if donated, is subject to export control regulations.

The International Traffic in Arms and Export Administration Regulations govern the export of defense articles and dual-use items. Depending on the technology involved, compliance with these regulations may be required.

The operation of drones, especially those intended for military purposes, is subject to regulations set by the Federal Aviation Administration (FAA) in the US.

These regulations cover various aspects, such as registration, airspace restrictions, and operational limitations. Therefore, it is crucial to build a drone that complies with FAA regulations to ensure legal operation.

The use of drones for military purposes, including combat operations, is subject to domestic and international laws, including laws governing armed conflict, human rights, and the laws of war.

Transferring military technology, even in the form of a donation, may have implications for national security and foreign policy. Depending on the nature of the technology and the recipient of the donation, approval or oversight from relevant government agencies may be necessary.

Given these legal complexities, citizens and organizations considering similar initiatives should seek legal advice and ensure compliance with applicable laws and regulations.

Additionally, transparency, accountability, and adherence to ethical principles are essential when engaging in activities involving military technology and defense efforts in your country.
