# Black-Pill-Starter-Guide
This repository describes how to setup and install a blinking LED program via UART on the Black Pill.

## Table of Contents
* [Requirements](#requirements)
* [Installing IDE and Programmer](#installing-the-ide-and-the-programmer)
* [Wiring the FTDI to the Black Pill](#wiring-the-ftdi-to-the-black-pill)
* [Creating First STM32 Project](#creating-first-stm32-project)
* [Uploading Project to Black Pill via UART](#uploading-project-to-black-pill-via-uart)
* [Simple LED Blinking Program](#simple-led-blinking-program)

## Requirements
### Hardware
* FTDI FT232RL
* STM32F411CEU6 Black Pill
* USB Type-A to Mini USB Cable
* Four Jumper Wires
* Breadboard
### Software
* STM32 Cube IDE
* STM32 Cube Programmer

## Installing the IDE and the Programmer
The [STM32 Cube IDE](https://www.st.com/en/development-tools/stm32cubeide.html) can be downloaded from ST Microelectronic's website. There are installers for Linux, Windows or macOS. Note, however, that ST Microelectronics does require an email address in order to send the download link. After downloading the Cube IDE one can simply follow the installer's prompts in order to correctly setup the Cube IDE on your computer. Furthermore, during the installation process it is best to keep the default configurations for all path variables and install locations.

Next we have to install [STM32 Cube Programmer](https://www.st.com/en/development-tools/stm32cubeprog.html) which can be downloaded from ST Microelectronic's site. There are again cross platform installers for Linux, Windows or macOS. Simply download and run the installer, again making sure to leave all configuration options to their default values.

The STM32 Cube IDE will be used in order to create the program that is to be uploaded to the Black Pill as well as configure all the settings required for the Black Pill to function such as the clock frequency. The STM32 Cube Programmer, however, will be used to upload the ```<Your STM32 Project>.elf``` file via UART to the Black Pill.

## Wiring the FTDI to the Black Pill
![Wiring Diagram for the FTDI and the Black Pill](https://github.com/Bertus-Jooste/Black-Pill-Starter-Guide/blob/master/Wiring%20Diagram.png)

Note that if you use the VCC pin on the FTDI instead of a dedicated 3.3 V or 5 V pin, you must insure that if the yellow jumper on the FTDI board is set to 3.3 V you wire the VCC pin of the FTDI board to a 3.3 V tolerant pin on the Black Pill and if the yellow jumper on the FTDI board is set to 5 V you must wire the VCC pin on the FTDI board to a 5 V tolerant pin on the Black Pill. 3.3 V Tolerant pins are marked with a 3.3 V on the Black Pill and 5 V tolerant pins are marked with a 5 V on the Black Pill.

## Creating First STM32 Project
1. Open up the STM32 Cube IDE, select ```File -> New -> STM32 Project```
2. In the ````MCU/MPU Selector```, type ```STM32F411CEU6``` into the part number search bar. This is the full name of the MCU on the Black Pill board. Select the top result in the search results, and click ```next```.
3. In the ```project setup popup```, enter your project's name, leave the rest as default, click ```next```, then ```finish```.
4. Once that’s done, it will open up the ```pinout and configuration``` page. There it’ll display the physical shape of the MCU, and the pins and pin names. This is where you can set individual pins to different default values, and the IDE will use this info to auto-generate setup code. In our case, we want to just left-click the ```PC13 pin```, and click ```GPIO_Output```. This pin is the pin connected to a user-controlled LED on the Black Pill. If you look on the Black Pill, you can see the LED we want to control, and see it has ```C13``` next to it. Eventually we can set other pins to use more of the Black Pill’s dev board, but for now, that’s all we need.
5. To have the IDE generate code, click the ```save icon```, or hit ```ctrl+s``` to save the configuration. It will ask if you want to generate code, and then ask if you want to open the code perspective. Click ```yes``` to both.
6. Now the ```main.c``` file will be open in one of the tabs. Select it.
7. Scroll down to the ```while(1)``` section. This section is equivalent to the ```loop() function``` in arduino. Here we can add our code to turn the ```PC13``` pin on and off. Copy the [code](#simple-led-blinking-program) at the bottom of this README.md file and paste it into the ```while(1)``` loop.
8. Build the project by clicking the ```build all``` button to the right of the hammer icon or by hitting ```ctrl+b```.
  
## Uploading Project to Black Pill via UART
1. Open the STM32 Cube Programmer application on your computer.
2. Connect the FTDI via a USB cable to your computer.
3. Put your Black Pill into ```DFU boot mode``` by holding in the ```BOOT0``` button and simultaniously pressing the ```NRST``` button. Release the ```NRST``` button while still pressing the ```BOOT0``` button. Finally release the ```BOOT0``` button. Your Black Pill should now be in ```DFU boot mode```.
4. In the top right corner of the Cube Programmer change ```ST-LINK``` to ```UART```, insure that the right port is selected in the ```UART configuration``` menu and then click ```Connect```. Your Black Pill should now be connected to your computer via UART.
5. Select ```Erasing and Programming``` from the menu in the left side bar.
6. In the ```Download menu``` select the path to ```<Your STM32 Project Name>.elf``` file you created in the Cube IDE. The path will most probably be ```<Path to where you saved your project>/Debug/<Project Name>.elf```
7. Finally, click ```Start Programming``` in order to upload the file to your Black Pill.
8. You can now press the ```NRST``` button on the Black Pill. The LED on your Black Pill should now be blinking at a rate of 1 Hz. Note that the STM32 Cube Programmer will notify you that the connection to the Black Pill was lost. This is because the Black Pill is not in ```DFU boot mode``` anymore. Simply put the Black Pill back into ```DFU boot mode``` by following ```step 3``` and you will be able to reconnect to the Black Pill.

## Simple LED Blinking Program
```
while (1)
  {
	  HAL_GPIO_WritePin(GPIOC, GPIO_PIN_13, 0);
	  HAL_Delay(1000);
	  HAL_GPIO_WritePin(GPIOC, GPIO_PIN_13, 1);
	  HAL_Delay(1000);
  }
```
