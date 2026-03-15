# -CAN-Based-Automotive-Dashboard-
Implemented an Automotive Dashboard using CAN bus where ECU1 and ECU2 send vehicle data to ECU3 which displays it on an LCD.





## Project Overview

This project demonstrates an Automotive Dashboard System using CAN (Controller Area Network) communication. Multiple Electronic Control Units (ECUs) transmit vehicle parameters through CAN bus, and a central Dashboard ECU receives the data and displays it on an LCD.

The system simulates how real automotive ECUs communicate with each other in modern vehicles.

---

## System Architecture

```
           CAN BUS NETWORK
       -----------------------

      ECU1               ECU2
   (Speed & Gear)    (RPM & Indicator)
       |                    |
       |                    |
       ------- CAN BUS -------
                |
                |
              ECU3
          Dashboard ECU
        (LCD Display + LEDs)
```

---

## ECU Functions

### ECU1 – Speed & Gear ECU

This ECU simulates vehicle speed and gear position.

Functions:
- Reads analog value using ADC to simulate speed.
- Reads keypad input for gear selection.
- Sends speed and gear information using CAN messages.

Transmitted CAN Messages:

| Parameter | Message ID |
|----------|-----------|
| Speed | 0x10 |
| Gear | 0x20 |

---

### ECU2 – RPM & Indicator ECU

This ECU simulates engine RPM and indicator status.

Functions:
- Reads analog input to simulate engine RPM.
- Reads switch inputs for left/right indicators.
- Sends RPM and indicator status through CAN.

Transmitted CAN Messages:

| Parameter | Message ID |
|----------|-----------|
| RPM | 0x30 |
| Indicator | 0x50 |

Indicator States:

| Value | Meaning |
|------|--------|
| 1 | Right Indicator |
| 2 | Left Indicator |
| 3 | Indicator OFF |

---

Timer overflow
      ↓
ISR executes
      ↓
flag1 toggles
      ↓
LED ON / OFF


ECU1 / ECU2 send CAN data
        ↓
ECU3 receives indicator status
        ↓
flag2 updated in main
        ↓
Timer0 interrupt occurs
        ↓
ISR toggles LEDs
        ↓
Indicator blinking

### ECU3 – Dashboard ECU

This ECU acts as the central dashboard.

Functions:
- Receives CAN messages from ECU1 and ECU2.
- Identifies message type using message ID.
- Displays values on Character LCD.
- Controls LED indicators using Timer0 interrupt.

Displayed Parameters:

- Vehicle Speed
- Gear Position
- Engine RPM
- Indicator Direction

Example Dashboard Display:

```
SP   EV   RPM   IND
45   G3   2300  ->
```

---

## CAN Message IDs Used

| Message ID | Parameter |
|------------|----------|
| 0x10 | Speed |
| 0x20 | Gear |
| 0x30 | RPM |
| 0x50 | Indicator |

Each parameter has a unique identifier so the dashboard ECU can recognize the received data.

---

## CAN Communication Process

1. ECU1 calculates speed and gear.
2. ECU2 calculates RPM and indicator status.
3. Both ECUs transmit data using CAN bus.
4. ECU3 continuously receives CAN messages.
5. ECU3 checks the message ID.
6. Based on the ID, the dashboard updates the display.

---

## Hardware Components

- PIC Microcontroller
- CAN Module
- Character LCD (CLCD)
- Potentiometer (for Speed and RPM simulation)
- Push Buttons / Keypad
- LEDs (for indicator simulation)
- Timer0 interrupt module

---

## Software Modules

| File | Purpose |
|-----|--------|
| main.c | Main application logic |
| can.c | CAN communication configuration |
| clcd.c | LCD display driver |
| timer0.c | Timer interrupt for indicator blinking |
| message_handler.c | CAN message processing |
| msg_id.h | CAN message ID definitions |

---

## Features

- Multi ECU communication
- CAN bus implementation
- Dashboard simulation
- Indicator blinking using interrupts
- Modular embedded software design

---

## Advantages

- Reduced wiring using CAN communication
- Reliable ECU communication
- Real-time dashboard monitoring
- Scalable architecture for adding more ECUs

---

## Limitations

- Simulated vehicle parameters
- Limited number of ECUs
- Character LCD display only

---

## Future Improvements

- Add Engine Temperature monitoring
- Add Fuel Level indicator
- Add graphical TFT dashboard
- Integrate real vehicle sensors
- Add diagnostic communication

---

## Applications

- Automotive dashboard systems
- Vehicle monitoring systems
- Embedded network communication
- Automotive ECU development

---

## Author

Embedded Systems Project

Automotive Dashboard using CAN Communication

