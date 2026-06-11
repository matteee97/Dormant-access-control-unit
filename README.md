# Dormant Access Control Unit

An embedded access control system based on a proximity sensor and Morse code input, designed to optimize energy consumption and security.

---

## Description

This project implements an intelligent access control unit that remains in low-power sleep mode and activates only when a presence is detected within 30 cm.

The user can enter a secret code through a push button using Morse code. The system manages:

- Authorized access
- Incorrect attempts
- Alarm activation
- Advanced power saving through interrupts

---

## Main Features

- Presence detection using an HC-SR04 ultrasonic sensor
- Message display on a 4-digit seven-segment display
- Morse code input through a push button
- Door unlocking via relay
- Alarm system with buzzer
- Sleep mode for energy optimization
- Fully interrupt-driven operation (no delays)

---

## Operating Logic

1. Sleep Mode
   - The system remains inactive to minimize power consumption.

2. Presence Detection
   - Periodic activation through the Watchdog Timer.
   - If the measured distance is less than 30 cm, the system becomes active.

3. User Interaction
   - The display shows "CIAO".
   - Morse code input:
     - Short press → .
     - Long press → -

4. Code Verification
   - Correct code → "Ent" displayed and door unlocked.
   - Incorrect code → "Er n" displayed, indicating remaining attempts.

5. Alarm Activation
   - After too many failed attempts, the display flashes "8888" and the buzzer is activated.

6. Return to Sleep Mode
   - The system returns to low-power operation.

---

## Modular Architecture

The system is divided into independent modules:

- HC-SR04 sensor module
- Seven-segment display module
- Push-button and Morse code handler
- Access control module
- Alarm management module
- Sleep mode manager

---

## Interrupt Management

The system is entirely event-driven and does not use delay().

### Interrupts Used

- WDT (Watchdog Timer) → sensor activation
- INT0 (ECHO) → distance measurement
- INT1 (Push Button) → Morse code input
- Timer0 → TRIG signal generation
- Timer1 → display multiplexing
- Timer2 → timing and timeout management

---

## Main Parameters

| Parameter | Value |
|------------|---------|
| Activation distance | 30 cm |
| Button debounce | 10–50 ms |
| Morse dot duration | 100–300 ms |
| Morse dash duration | 300–900 ms |
| Input timeout | ~6 s |
| Display refresh rate | ≥ 40 Hz |
| Buzzer frequency | ~750 Hz |

---

## Hardware Components

- HC-SR04 ultrasonic sensor
- 4-digit seven-segment display
- Push button
- Relay
- Buzzer
- Microcontroller (e.g., AVR)

---

## Alternative Solutions

- LED / RGB LED → simpler but less informative
- LCD display → more flexible but more complex
- PIR sensor → more energy-efficient but less precise

---

## Simulation

- Normal mode: https://wokwi.com/projects/408737880547079169
- Debug mode: https://wokwi.com/projects/421052364059217921

---

## User Manual

| Message | Meaning |
|----------|---------|
| CIAO (hello) | System ready |
| Ent | Access granted |
| Er n | Incorrect code |
| 8888 | Alarm active |

---

## Skills Developed

- Embedded programming
- Interrupt handling
- Power optimization
- Modular system design
- Hardware/software integration

---

## Conclusion

The system has been designed to be:

- Efficient
- Secure
- Responsive

Through the combined use of low-power techniques, interrupt-driven programming, and modular architecture, it provides a reliable and energy-efficient access control solution.
