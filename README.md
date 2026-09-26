# Design-and-Implementation-of-an-Eight-LED-Sequential-Lighting-System-Using-AT89C51-Microcontroller
Design and Implementation of an Eight-LED Sequential Lighting System Using AT89C51 Microcontroller using Proteus
##  Overview

This project presents the **design and implementation of an eight-LED sequential lighting system using the AT89C51 microcontroller**.

Eight LEDs are interfaced with **Port 2 (P2.0–P2.7)** of the AT89C51. The microcontroller controls the LEDs such that they glow one after another with a predefined time delay, producing a **running LED effect**.

The project demonstrates basic concepts of **8051 microcontroller programming, GPIO interfacing, bit manipulation, and software delay generation**.

---

##  Objectives

* To interface eight LEDs with the AT89C51 microcontroller.
* To understand the operation of 8051 I/O ports.
* To generate a sequential LED lighting pattern.
* To implement software delay using Embedded C.
* To understand bit shifting and port manipulation.
* To simulate the circuit using Proteus.

---

##  Hardware Requirements

| Component                      | Quantity    |
| ------------------------------ | ----------- |
| AT89C51 Microcontroller        | 1           |
| LED                            | 8           |
| Resistor 330 Ω                 | 8           |
| Crystal Oscillator 11.0592 MHz | 1           |
| Capacitor 33 pF                | 2           |
| 5 V DC Power Supply            | 1           |
| Breadboard                     | 1           |
| Connecting Wires               | As required |

---

##  Software Requirements

* **Keil µVision** – For Embedded C programming and HEX file generation
* **Proteus** – For circuit simulation

---

##  Circuit Connections

The eight LEDs are connected to **Port 2** of the AT89C51.
```text
AT89C51                    LED

P2.0 ───── 330Ω ───── LED1
P2.1 ───── 330Ω ───── LED2
P2.2 ───── 330Ω ───── LED3
P2.3 ───── 330Ω ───── LED4
P2.4 ───── 330Ω ───── LED5
P2.5 ───── 330Ω ───── LED6
P2.6 ───── 330Ω ───── LED7
P2.7 ───── 330Ω ───── LED8
```

Each LED is connected through a **330 Ω current-limiting resistor**.

> **Note:** The program assumes an active-HIGH LED connection. If the hardware uses active-LOW logic, the LED patterns must be inverted.

---

##  Working Principle

The AT89C51 sends an 8-bit pattern to **Port 2**. Only one bit is set at a time, causing one LED to glow.

The sequence is:

```text
00000001 → 00000010 → 00000100 → 00001000
     ↓
00010000 → 00100000 → 01000000 → 10000000
```

Therefore:

```text
LED1 → LED2 → LED3 → LED4 → LED5 → LED6 → LED7 → LED8
```

After LED8, the sequence starts again from LED1.

---

##  Embedded C Program

```c
#include <reg51.h>

void delay(void)
{
     unsigned int i, j;

    for(i = 0; i < 500; i++)
    {
        for(j = 0; j < 120; j++);
    }
}

void main(void)
{
    unsigned char i;

    while(1)
    {
        for(i = 0; i < 8; i++)
        {
            P2 = (1 << i);
            delay();
        }
    }
}
```

---

## Program Explanation

### Header File

```c
#include <reg51.h>
```
This header file provides the definitions required to access the registers of the 8051 microcontroller.

### Port Configuration

Port 2 is used to control the eight LEDs.

```c
P2 = (1 << i);
```

The expression shifts a single `1` bit from P2.0 toward P2.7.

### LED Sequence

| Step | P2 Value | Binary     | LED  |
| ---- | -------- | ---------- | ---- |
| 1    | `01H`    | `00000001` | LED1 |
| 2    | `02H`    | `00000010` | LED2 |
| 3    | `04H`    | `00000100` | LED3 |
| 4    | `08H`    | `00001000` | LED4 |
| 5    | `10H`    | `00010000` | LED5 |
| 6    | `20H`    | `00100000` | LED6 |
| 7    | `40H`    | `01000000` | LED7 |
| 8    | `80H`    | `10000000` | LED8 |

---

##  Flowchart

```text
             ┌─────────────┐
             │    START    │
             └──────┬──────┘
                    │
                    ▼
          ┌──────────────────┐
          │ Initialize Port 2│
          └────────┬─────────┘
                   │
                   ▼
          ┌──────────────────┐
          │ Set LED Pattern  │
          └────────┬─────────┘
                   │
                   ▼
          Next LED   LED1
               │       │
               └───┬───┘
                   │
                   ▼
                Repeat
```

---

##  Simulation

The circuit can be simulated in **Proteus** using the following procedure:

1. Create the AT89C51 circuit.
2. Connect eight LEDs to Port 2.
3. Add 330 Ω resistors in series with the LEDs.
4. Connect the crystal oscillator and capacitors.
5. Add the reset and power supply connections.
6. Write the Embedded C program in Keil µVision.
7. Compile the program and generate the `.hex` file.
8. Load the HEX file into the AT89C51 model in Proteus.
9. Start the simulation.
10. Observe the sequential LED operation.

---

##  Project Structure

```text
Eight-LED-Sequential-Lighting/
│
├── README.md
│
├── src/
│   └── led_sequence.c
│
├── hex/
│   └── led_sequence.hex
│
├── simulation/
│   └── led_sequence.pdsprj
│
└── images/
    ├── circuit.png
    └── simulation.png
```
---

##  Expected Output

The LEDs glow sequentially:

```text
LED1 → LED2 → LED3 → LED4
                      ↓
LED8 ← LED7 ← LED6 ← LED5
```

The sequence repeats continuously.

---



## Output
<img width="1337" height="989" alt="WhatsApp Image 2026-09-24 at 1 48 32 PM" src="https://github.com/user-attachments/assets/54f36c91-7159-4857-801b-923e8f55eef0" />


##  Applications

This type of sequential lighting system can be used in:

* Decorative lighting systems
* Indicator panels
* Electronic displays
* Signalling systems
* Traffic-light demonstrations
* Embedded-system prototypes
* Microcontroller learning projects

---
##  Result

The eight-LED sequential lighting system using the AT89C51 microcontroller** was successfully designed and implemented. The eight LEDs connected to Port 2 of the AT89C51 glowed **sequentially from LED1 to LED8 with a predefined time delay. The sequence was repeated continuously, producing a running-light effect.Thus, the required sequential LED lighting operation was successfully achieved and verified through simulation.
