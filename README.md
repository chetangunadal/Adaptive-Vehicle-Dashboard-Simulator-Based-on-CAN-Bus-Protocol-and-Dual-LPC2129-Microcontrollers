# LPC2129 CAN-Based Vehicle Monitoring and Control System

## 1. Project Overview

This project implements a vehicle monitoring and control system using two LPC2129 microcontrollers communicating through the Controller Area Network (CAN) protocol.

The system monitors sensor parameters such as potentiometer value, temperature, and ultrasonic distance. It also provides vehicle lighting control using external interrupts.

Two microcontrollers are used:
- **Node A (Transmitter):** Reads sensor values and detects switch interrupts. It transmits the collected data and control commands through CAN.
- **Node B (Receiver):** Receives CAN messages, processes the received data, controls output LEDs, and displays the information through UART0.

## 2. Project Objectives

- Implement CAN communication between two LPC2129 microcontrollers.
- Read analog sensor values using ADC.
- Measure distance using an ultrasonic sensor.
- Implement external interrupts for vehicle lighting control.
- Transmit multiple sensor values through CAN frames.
- Display received information using UART0 serial communication.

## 3. Hardware Components

| Component | Purpose |
|---|---|
| LPC2129 Microcontroller × 2 | CAN transmitter and receiver |
| CAN Transceiver × 2 | CAN bus communication |
| Potentiometer | Analog input measurement |
| LM35 Temperature Sensor | Temperature measurement |
| Ultrasonic Sensor | Distance measurement |
| Push Buttons × 3 | External interrupt inputs |
| LEDs | Vehicle light indication |
| UART0 | Serial monitoring |

## 4. System Architecture

### Node A – Transmitter

Node A performs the following operations:

1. Initializes external interrupts.
2. Initializes CAN communication.
3. Initializes UART0 and ADC.
4. Reads the potentiometer value using ADC channel 0.
5. Reads the temperature sensor using ADC channel 1.
6. Measures ultrasonic distance.
7. Transmits sensor information through CAN.
8. Detects external interrupt inputs for:
   - Left indicator ON/OFF
   - Headlight ON/OFF
   - Right indicator ON/OFF

### Node B – Receiver

Node B performs the following operations:

1. Initializes CAN communication.
2. Initializes UART0.
3. Waits for CAN messages from Node A.
4. Checks the received CAN ID.
5. Processes lighting control commands.
6. Controls the corresponding LEDs.
7. Extracts potentiometer, temperature, and ultrasonic values.
8. Displays the received information through UART0.

## 5. CAN Communication Details

| Parameter | Configuration |
|---|---|
| Protocol | CAN |
| Controller | LPC2129 CAN1 |
| CAN ID | 0x123 |
| Baud Rate | 125 Kbps |
| DLC | 8 Bytes |
| Frame Type | Data Frame |

### CAN Data Format

| CAN Data | Information |
|---|---|
| Byte 0 | Lighting control command |
| Byte 1 | Potentiometer value |
| Byte 2 | Temperature value |
| Byte 3 | Reserved |
| Byte 4–7 | Ultrasonic data field |

## 6. Lighting Control Commands

| Command | Operation |
|---|---|
| 0x01 | Left indicator ON |
| 0x11 | Left indicator OFF |
| 0x02 | Headlight ON |
| 0x22 | Headlight OFF |
| 0x03 | Right indicator ON |
| 0x33 | Right indicator OFF |

## 7. Software Structure

```text
LPC2129-CAN-Vehicle-Monitoring/
│
├── Node_A/
│   ├── main.c
│   ├── can1_driver.c
│   ├── adc.c
│   ├── uart0.c
│   ├── delay.c
│   ├── ultrasonic.c
│   └── header.h
│
├── Node_B/
│   ├── main.c
│   ├── can1_driver.c
│   ├── uart0.c
│   ├── delay.c
│   └── header.h
│
└── README.md
```

## 8. Expected Output

**Node A UART Output**
```text
left on
pot=45
temp=28
```

**Node B UART Output**
```text
waiting nodeB
nodeB
left indicator on
pot=45
temp=28
ultra=15
```

*Note: These are illustrative output examples.*

## 9. Applications

- Vehicle monitoring systems
- Automotive lighting control
- Embedded automotive communication
- Sensor data monitoring
- CAN-based distributed control systems

## 10. Conclusion

This project demonstrates CAN communication between two LPC2129 microcontrollers. It integrates ADC, ultrasonic sensing, external interrupts, UART communication, and LED control to develop a basic vehicle monitoring and control system.

The project provides practical experience in embedded C programming, ARM7 microcontrollers, sensor interfacing, interrupt handling, and CAN protocol communication.

## 11. Technologies Used

- Embedded C
- LPC2129 (ARM7)
- CAN Protocol
- ADC
- UART0
- External Interrupts
- Ultrasonic Sensor
- Keil µVision
