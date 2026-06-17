# Automatic Beverage Dispenser

A complete hardware and software solution for an automated beverage dispensing system. The project features a custom 2-layer printed circuit board (PCB) and firmware written in C for the STM32G0 microcontroller. The system accurately dispenses liquids by measuring the flow rate via a dedicated sensor and controlling a 12V fluid pump.

## Features
* **Adjustable Volume Control:** Users can set the desired liquid volume between 50 ml and 300 ml (in 50 ml increments) using the "Up" and "Down" tactile switches.
* **Precise Dispensing:** Utilizes an external flow sensor with interrupt-driven pulse counting to accurately measure the dispensed volume based on a configurable K-factor.
* **Automated Pump Control:** The MCU controls a 12V DC fluid pump via an onboard N-channel MOSFET (AO3400), automatically shutting it off once the target volume is reached.
* **Emergency Stop:** The pouring process can be manually halted at any time by pressing the "Start/Stop" button.
* **Expansion Ready:** Exposed I2C headers allow for future integration of external modules, such as an OLED display.

## Hardware Specifications
* **Microcontroller:** STM32G030F6P6 (ARM Cortex-M0+)
* **Power Supply:** 12V DC input (barrel jack), regulated to 3.3V for logic via an AMS1117 LDO.
* **Actuator Driver:** AO3400 MOSFET with flyback diode protection for the 12V pump.
* **Inputs:** 3x Tactile switches (hardware debounced/filtered), 1x Flow sensor signal input.
* **Interfaces:** SWD programming header, I2C expansion header.

## Software
The firmware is developed using STM32 HAL. It implements a simple state machine (`IDLE` and `POURING`) to manage user inputs and the dispensing process. Button inputs are software-debounced, and the flow sensor is handled via external interrupts (EXTI) to ensure no pulses are missed during the pump operation.