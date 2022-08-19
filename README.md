# Black-Pill-Starter-Guide
This is a repository which describes how to setup and install a program via UART on the Black Pill.

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
The [STM32 Cube IDE](https://www.st.com/en/development-tools/stm32cubeide.html) can be downloaded from ST Microelectronic's website. There are installers for either Linux, Windows of macOS. Note, however, that ST Microelectronics does require an email address in order to send the download link. After downloading the Cube IDE one can simply follow the installers prompts in order to correctly setup the Cube IDE on your device. Furthermore, note during the installation process it is best to leave all path variables and install locations with their default value.

Next we have to install [Cube Programmer](https://www.st.com/en/development-tools/stm32cubeprog.html) which can be downloaded from ST Microelectronic's site. There are again cross platform installers for Linux, Windows or macOS.

The STM32 Cube IDE will be used in order to create the program that is to be uploaded to the Black Pill as well as configure all the settings required for the Black Pill to function. The STM32 Cube Programmer, however, will be used to upload the <STM32 Project>.elf file via UART to the Black Pill.

## Wiring the FTDI to the Black Pill
![Wiring Diagram of the FTDI and the Black Pill](https://github.com/Bertus-Jooste/Black-Pill-Starter-Guide/blob/master/Wiring%20Diagram.png)
  
Note that if you use the VCC pin on the FTDI, you must insure that the jumper on the FTDI board is set to 3.3 V if you want to power the Black Pill with 5 V, move the jumber of the FTDI to the 5 V posistion and power the Black Pill through one of its 5 V tolerant pins.

## Creating First STM32 Project
1. Open up STM32Cube IDE, select File -> New -> STM32 Project
2. In the MCU/MPU Selector, enter “STM32F411CEU” into the search. This is the full name of the MCU on the adafruit black pill board. Select the only result in the search results, and click next
3. In the project setup popup, set the project name (In my case, I chose “Blinky”), leave the rest as default, so click next, then finish.
4. Once that’s done, it will open up the pinout and configuration page. There it’ll display the physical shape of the MCU, and the pins and pin names. This is where you can set individual pins to different default values, and the IDE will use this info to auto-generate setup code. In our case, we want to just left-click the PC13 pin, and click “GPIO_Output”. This pin is the pin connected to a user-controlled LED on the black pill. If you look on the black pill, you can see the LED we want to control, and see it has C13 next to it. Eventually we can set other pins to use more of the black pill’s dev board, but for now, that’s all we need to make blinky run.
5. To have the IDE generate code, click the save icon, or hit ctrl+s to save the configuration. It will ask if you want to generate code, and then ask if you want to open the code perspective. Click yes to both.
6. Now the main.c file will be open in one of the tabs. Select it. This is finally some C code!
7. Scroll down to the while(1) section. This section is equivalent to the loop() function in arduino. Here we can add our code to turn the PC13 pin on and off.
  
## Uploading Project to Black Pill via UART
1. Open the Cube Programmer applications on your computer.
2. Connect the FTDI via a USB cable to your computer.
3. Put your Black Pill into DFU boot mode by holding in the BOOT0 button and simultaniously pressing the NRST button. Release the NRST button while still presseing the BOOT0 button. Finally release the BOOT0 button. Your Black Pill should now be in DFU boot mode.
4. In the top right corner of the Cube programmer change ST-LINK to UART, insure that the right port is selected in the UART configuration menu and then click Connect. Your Black Pill should now be connected to your computer via UART.
5. Select Erasing and Programming from the menu in the left side bar.
6. In the Download menu select the path to the <STM32 Project>.elf file you created in the Cube IDE.
7. Finally, click Start Programming in order to upload the file to your Black Pill.

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
