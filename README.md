# Rx_Tx_BLE_Board

## Overview

This repository contains code for controlling an LED on a board using a remote node. When a button is pressed on the remote, the LED on the board lights up via Bluetooth Low Energy (BLE) communication.

## Features

- Controls an LED on a receiver board using a remote node over BLE.
- Uses BLE for low-power wireless communication.
- Simple, responsive design to toggle LED on/off with button press.
- Reads temperature and humidity data from the SHT40 sensor.
- Uses the I2C interface for communication.
- Configurable update rates and thresholds for sensor readings.
- Displays sensor data on a connected display (e.g., OLED).
- Compatible with Zephyr RTOS.

## Hardware Requirements

- BLE-Enabled Board (e.g., NRF52832DK or any Zephyr-compatible BLE board).
- BLE Node (remote) to send control signals.
- SHT40 Sensor (I2C temperature and humidity sensor).
- Microcontroller/Board: NRF52832 (or any other Zephyr-compatible platform with I2C support).
- Optional: OLED display to visualize data.

## Software Requirements

1. Zephyr RTOS
2. Nordic SDK (if using Nordic boards)
3. An IDE supporting Zephyr development (e.g., VS Code with Zephyr Extension)
4. CMake, west (for building Zephyr projects)

## Prerequisites

1. **Zephyr RTOS**: Ensure Zephyr is installed and set up correctly. Refer to the [Zephyr Getting Started Guide](https://docs.zephyrproject.org/latest/getting_started/index.html) for installation instructions.
2. **BLE Configuration**: Enable BLE support in Zephyr to allow communication between the remote node and receiver.
3. **SHT40 Sensor Driver**: The driver should be included in the device tree and enabled in the configuration.

## Setup

1. **Configure the Build Environment**: Set up the environment for your BLE-enabled board and remote node. Before building the project, set up the environment for your board. For example, if you're using an NRF52832 board.
2. **Enable BLE Support**: In the `prj.conf` file, ensure BLE configurations are enabled for both the remote node and receiver board.
3. **Enable SHT40 Support**: In the prj.conf file, ensure you have enabled I2C and sensor support.
3. **Building the Project**: Build and flash the code for both the remote and receiver.
4. **Pairing Remote and Receiver**: Set up pairing between the remote and receiver, ensuring BLE communication is established.
5. **Flashing the Firmware**: After a successful build, flash the firmware onto your board.

## How It Works

1. **Button Press on Remote**: When a button is pressed on the node (remote), a signal is sent to the receiver.
2. **LED Control on Receiver**: The receiver listens for BLE signals and toggles the LED based on the button state from the remote.

## Pin Configuration

- LED Pin on Receiver: Configurable via code.
- Button Pin on Remote: Configurable via code.

## SHT40 Sensor Pin Connections

| SHT40 Pin | Microcontroller Pin  |
|-----------|----------------------|
| VCC       | 3.3V                |
| GND       | GND                 |
| SDA       | I2C Data Line       |
| SCL       | I2C Clock Line      |


Sample Output:
==============
.. code-block:: console

        *** Booting Zephyr OS build v2.6.0-rc1-315-g50d8d1187138  ***
        SHT4X: 23.64 Temp. [C] ; 30.74 RH [%] -- 
        SHT4X: 23.66 Temp. [C] ; 32.16 RH [%] --
        SHT4X: 23.63 Temp. [C] ; 30.83 RH [%] -- 


## Usage

- Once the board is flashed, power on both the remote and receiver. When the remote's button is pressed, the LED on the receiver board will turn on. Releasing the button will turn off the LED.
- Once the board is flashed, the application will start reading temperature and humidity data from the SHT40 sensor at regular intervals and print the results over the serial console.

## Troubleshooting

### 1. BLE Connection Issues

- Ensure both devices are in range and properly powered.
- Confirm that BLE pairing was successful.
- Check the configuration to ensure BLE settings match on both devices.

### 2. LED Not Responding

- Verify the LED pin configuration on the receiver board.
- Check if the remote is sending signals correctly when the button is pressed.

### 3. Sensor Not Detected:
- Ensure the sensor is connected properly and the I2C address (0x44 by default) is correct.
- Verify that I2C is enabled in your configuration.

