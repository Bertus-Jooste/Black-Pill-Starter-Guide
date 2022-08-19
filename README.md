# Black-Pill-Starter-Guide
This is a repository which describes how to setup and install a program via UART on the Black Pill.

## Table of Contents
* [Requirements](#requirements)
* [Installing IDE and Programmer](#installing-ide-and-the-programmer)
* [Wiring the FTDI to the Black Pill](#wiring-the-ftdi-to-the-black-pill)
* [Creating First STM32 Project](#creating-first-stm32-project)
* [Uploading Project to Black Pill via UART](#uploading-project-to-black-pill-via-uart)

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

## Installing IDE and the Programmer
The [STM32 Cube IDE](https://www.st.com/en/development-tools/stm32cubeide.html) can be downloaded from ST Microelectronic's website. There are installers for either Linux, Windows of macOS. Note, however, that ST Microelectronics does require an email address in order to send the download link. After downloading the Cube IDE one can simply follow the installers prompts in order to correctly setup the Cube IDE on your device. Furthermore, note during the installation process it is best to leave all path variables and install locations with their default value.

Next we have to install [Cube Programmer](https://www.st.com/en/development-tools/stm32cubeprog.html) which can be downloaded from ST Microelectronic's site. There are again cross platform installers for Linux, Windows or macOS.

The STM32 Cube IDE will be used in order to create the program that is to be uploaded to the Black Pill as well as configure all the settings required for the Black Pill to function. The STM32 Cube Programmer, however, will be used to upload the <STM32 Project>.elf file via UART to the Black Pill.

## Wiring the FTDI to the Black Pill

## Creating First STM32 Project

## Uploading Project to Black Pill via UART
