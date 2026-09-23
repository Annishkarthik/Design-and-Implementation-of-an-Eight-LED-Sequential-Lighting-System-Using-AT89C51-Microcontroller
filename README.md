Experiment: Push-Button-Controlled Buzzer and Speaker Using AT89C51
1. Aim

To interface a push button, buzzer, and speaker with the AT89C51 microcontroller and activate the buzzer and speaker when the push button is pressed.

2. Objective
To understand the basic operation of the AT89C51 8051 microcontroller.
To interface a push button as a digital input.
To interface a buzzer and speaker as output devices.
To control the buzzer and speaker using an NPN BC547 transistor.
To write and execute an Embedded C program for monitoring the push button.
To understand switch debouncing using a small software delay.
To observe the ON/OFF operation of the audible indicators.
3. Components Required
S.No.	Component	Specification	Quantity
1	Microcontroller	AT89C51	1
2	Push button	Normally Open	2
3	Buzzer	5 V	1
4	Speaker	Low-power speaker	1
5	NPN Transistor	BC547	1
6	Base Resistor	330 Ω	1
7	Pull-down Resistor	10 kΩ	1
8	Reset Resistor	10 kΩ	1
9	Capacitor	0.1 µF	1
10	Power Supply	Regulated +5 V DC	1
11	Crystal Oscillator	Suitable 8051 crystal	1
12	Connecting Wires	—	As required

The component values above are based on the repository's circuit description.

4. Theory
4.1 AT89C51 Microcontroller

The AT89C51 is an 8-bit microcontroller based on the 8051 architecture. It contains programmable I/O ports that can be configured for interfacing switches, LEDs, buzzers, displays, motors and other peripherals.

In this experiment:

P1.2 is used as the push-button input.
P3.2 is used as the control output for the transistor.
The transistor acts as a switching device for the buzzer and speaker.
4.2 Push Button

A push button is used to provide a digital input to the microcontroller.

The push button is connected between +5 V and P1.2.

A 10 kΩ pull-down resistor is connected between P1.2 and ground.

Therefore:

Button released → P1.2 = LOW
Button pressed → P1.2 = HIGH

This allows the microcontroller to determine whether the button is pressed.

4.3 BC547 Transistor

The AT89C51 output pin is used to control a BC547 NPN transistor.

The transistor works as an electronic switch.

When P3.2 = HIGH:

Base current flows through the 330 Ω resistor.
The BC547 turns ON.
Current flows through the buzzer and speaker.
The buzzer and speaker produce sound.

When P3.2 = LOW:

The transistor turns OFF.
Current through the buzzer and speaker stops.
The sound is switched OFF.

The repository specifies the BC547 collector as the common connection to the negative terminals of the buzzer and speaker, with their positive terminals connected to +5 V.

5. Pin Connections
AT89C51 Pin/Port	Connection
P1.2, Pin 3	Push-button input
P3.2 / INT0, Pin 12	BC547 base through 330 Ω
VCC, Pin 40	+5 V
GND, Pin 20	Ground
RST, Pin 9	Reset circuit
BC547 emitter	Ground
BC547 collector	Negative terminals of buzzer and speaker
Buzzer +	+5 V
Speaker +	+5 V
P1.2	10 kΩ pull-down to GND

The repository also notes that the AT89C51 requires a suitable clock circuit connected to XTAL1 and XTAL2.

Simplified connection
                 +5V
                  |
             Push Button
                  |
                  +-------- P1.2
                  |
                10kΩ
                  |
                 GND


AT89C51                         BC547
--------                       -------
P3.2 -------- 330Ω ----------> Base
                                |
                               |/
                         GND --|   Collector
                               |\
                                |
                                +------ Buzzer (-)
                                |
                                +------ Speaker (-)

Buzzer (+) -------------------- +5V
Speaker (+) ------------------- +5V
Emitter ----------------------- GND

Note: For an actual inductive/magnetic buzzer, a flyback diode should be provided across the load to protect the transistor.

6. Working Principle
The AT89C51 continuously monitors the push button connected to P1.2.
A 10 kΩ pull-down resistor keeps P1.2 at LOW when the push button is released.
When the push button is pressed, P1.2 receives +5 V.
Therefore, P1.2 becomes HIGH.
The microcontroller detects the HIGH input.
The microcontroller makes P3.2 HIGH.
The HIGH signal is applied to the base of the BC547 through a 330 Ω resistor.
The BC547 switches ON.
Current flows through the buzzer and speaker.
The buzzer and speaker produce sound.
When the push button is released, P1.2 becomes LOW.
The microcontroller makes P3.2 LOW.
The BC547 switches OFF.
The buzzer and speaker stop producing sound.
This process is continuously repeated.
7. Algorithm
Start.
Initialize the microcontroller.
Configure P1.2 as the push-button input.
Configure P3.2 as the buzzer/speaker control output.
Initially set P3.2 LOW.
Read the state of P1.2.
Check whether the push button is pressed.
If P1.2 = HIGH, wait for approximately 20 ms for switch debouncing.
Read P1.2 again.
If P1.2 is still HIGH, make P3.2 HIGH.
Switch ON the BC547 transistor.
Activate the buzzer and speaker.
If P1.2 = LOW, make P3.2 LOW.
Switch OFF the BC547 transistor.
Switch OFF the buzzer and speaker.
Repeat the process continuously.
8. Flowchart
              ┌──────────────┐
              │    START     │
              └──────┬───────┘
                     │
                     ▼
          ┌─────────────────────┐
          │ Initialize P1.2 and │
          │       P3.2          │
          └──────────┬──────────┘
                     │
                     ▼
          ┌─────────────────────┐
          │ Read push button     │
          │       P1.2           │
          └──────────┬──────────┘
                     │
                     ▼
                ┌─────────┐
                │ P1.2=1? │
                └───┬─┬───┘
                  No│ │Yes
                    │ │
                    │ ▼
                    │ ┌────────────────┐
                    │ │ Delay 20 ms    │
                    │ └───────┬────────┘
                    │         │
                    │         ▼
                    │   ┌────────────┐
                    │   │ P1.2 still │
                    │   │ HIGH?      │
                    │   └────┬───┬───┘
                    │      No│   │Yes
                    │        │   │
                    │        │   ▼
                    │        │ ┌─────────────┐
                    │        │ │ P3.2 = HIGH │
                    │        │ └──────┬──────┘
                    │        │        │
                    │        │        ▼
                    │        │ ┌─────────────┐
                    │        │ │ Buzzer and  │
                    │        │ │ speaker ON  │
                    │        │ └──────┬──────┘
                    │        │        │
                    ▼        ▼        │
             ┌─────────────────┐      │
             │   P3.2 = LOW    │◄─────┘
             └────────┬────────┘
                      │
                      ▼
             ┌─────────────────┐
             │ Buzzer & speaker│
             │      OFF        │
             └────────┬────────┘
                      │
                      └──────► Repeat
9. Embedded C Program

The repository provides the following Embedded C program using reg51.h.

#include <reg51.h>

sbit BUTTON = P1^2;
sbit BUZZER = P3^2;

void delay_ms(unsigned int ms)
{
    unsigned int i, j;

    for (i = 0; i < ms; i++)
    {
        for (j = 0; j < 112; j++)
        {
            /* Approximate delay */
        }
    }
}

void main(void)
{
    /* Configure the button pin as input */
    BUTTON = 1;

    /* Initially switch OFF the buzzer and speaker */
    BUZZER = 0;

    while (1)
    {
        /* Check whether the push button is pressed */
        if (BUTTON == 1)
        {
            /* Debouncing delay */
            delay_ms(20);

            if (BUTTON == 1)
            {
                /* Switch ON the buzzer and speaker */
                BUZZER = 1;
            }
        }
        else
        {
            /* Switch OFF the buzzer and speaker */
            BUZZER = 0;
        }
    }
}
10. Program Explanation
#include <reg51.h>
#include <reg51.h>

This includes the 8051 microcontroller register definitions required for accessing ports such as P1 and P3.

Button declaration
sbit BUTTON = P1^2;

This assigns the name BUTTON to P1.2.

Buzzer declaration
sbit BUZZER = P3^2;

This assigns the name BUZZER to P3.2.

Although the variable is called BUZZER, this output actually controls the BC547, which switches both the buzzer and speaker.

Delay function
void delay_ms(unsigned int ms)

This creates an approximate delay used for switch debouncing.

Mechanical switches can produce rapid unwanted transitions when pressed or released. The approximately 20 ms delay helps prevent these false transitions.

Input configuration
BUTTON = 1;

The P1.2 pin is placed in the appropriate state for input operation.

Initial output
BUZZER = 0;

The buzzer and speaker are initially switched OFF.

Continuous monitoring
while (1)

The microcontroller continuously monitors the push button.

Button pressed
if (BUTTON == 1)

If P1.2 is HIGH, the program assumes that the push button is pressed.

After the debounce delay, the button is checked again.

BUZZER = 1;

P3.2 becomes HIGH, turning ON the BC547 and consequently the buzzer and speaker.

Button released
else
{
    BUZZER = 0;
}

When P1.2 is LOW, P3.2 is made LOW and the audible devices are switched OFF.

11. Input-Output Table
Push Button	P1.2	P3.2	BC547	Buzzer	Speaker
Released	LOW	LOW	OFF	OFF	OFF
Pressed	HIGH	HIGH	ON	ON	ON

This corresponds to the expected output given in the repository.

12. Procedure
Collect all the required components.
Connect the AT89C51 microcontroller to a regulated +5 V supply.
Connect the required crystal oscillator circuit to XTAL1 and XTAL2.
Connect the reset circuit to the RST pin.
Connect one terminal of the push button to +5 V.
Connect the other terminal of the push button to P1.2.
Connect a 10 kΩ pull-down resistor between P1.2 and GND.
Connect P3.2 to the base of the BC547 through a 330 Ω resistor.
Connect the emitter of BC547 to GND.
Connect the negative terminals of the buzzer and speaker to the collector of BC547.
Connect the positive terminals of the buzzer and speaker to +5 V.
Connect all grounds together.
Write the Embedded C program in Keil.
Compile the program and generate the required HEX file.
Load the HEX file into the AT89C51 in the required hardware/simulation environment.
Switch ON the +5 V supply.
Initially verify that the buzzer and speaker remain OFF.
Press the push button.
Observe that the buzzer and speaker turn ON.
Release the push button.
Observe that the buzzer and speaker turn OFF.
Record the observations.
13. Observation
S.No.	Push Button Status	P1.2	P3.2	Audible Output
1	Released	LOW	LOW	Buzzer and speaker OFF
2	Pressed	HIGH	HIGH	Buzzer and speaker ON
3	Released	LOW	LOW	Buzzer and speaker OFF
4	Pressed	HIGH	HIGH	Buzzer and speaker ON
14. Expected Output
When the push button is released
P1.2 = LOW
P3.2 = LOW
BC547 = OFF
Buzzer = OFF
Speaker = OFF
When the push button is pressed
P1.2 = HIGH
P3.2 = HIGH
BC547 = ON
Buzzer = ON
Speaker = ON

The repository specifies the same released/pressed relationship between P1.2, P3.2 and the audible devices.

15. Applications
Security alarm systems.
Emergency warning systems.
Doorbell circuits.
Industrial fault indicators.
Vehicle alert systems.
Patient assistance systems.
Simple electronic alert systems.
Push-button notification systems.

The first six applications are explicitly listed in the repository.

16. Advantages
Simple circuit design.
Low component count.
Easy to implement using an 8051 microcontroller.
Simple Embedded C program.
Provides immediate audible feedback.
Suitable for learning microcontroller GPIO interfacing.
Can be extended for alarm and notification applications.
17. Limitations
The circuit provides only basic ON/OFF sound control.
The basic program does not generate different musical tones.
A separate transistor stage is used because the microcontroller should not directly drive a relatively higher-current load.
Mechanical switch bouncing must be considered.
A suitable clock circuit is required for normal AT89C51 operation.
An inductive/magnetic buzzer may require a flyback diode for transistor protection.
18. Precautions
Use a regulated +5 V DC supply.
Check the AT89C51 pin connections before powering the circuit.
Ensure that VCC and GND are connected correctly.
Use the correct resistor values.
Ensure correct BC547 transistor pin identification.
Do not connect a high-power speaker directly to the microcontroller pin.
Use a transistor driver for the buzzer/speaker load.
Ensure all devices have a common ground.
Use the required crystal oscillator circuit for the AT89C51.
For a magnetic/inductive buzzer, use a suitable flyback diode as recommended in the project documentation.
19. Viva Questions and Answers
1. What is the aim of this experiment?

To interface a push button, buzzer and speaker with the AT89C51 microcontroller and activate the audible devices when the push button is pressed.

2. Which microcontroller is used?

AT89C51, an 8051-family 8-bit microcontroller.

3. Which pin is used for the push button?

P1.2, pin 3.

4. Which pin controls the buzzer and speaker?

P3.2, pin 12.

5. Why is a pull-down resistor used?

The 10 kΩ pull-down resistor ensures that P1.2 remains at a defined LOW logic level when the push button is not pressed.

6. What happens when the push button is pressed?

P1.2 becomes HIGH, the microcontroller makes P3.2 HIGH, the BC547 turns ON, and the buzzer and speaker produce sound.

7. What happens when the button is released?

P1.2 becomes LOW, P3.2 becomes LOW, the BC547 turns OFF, and the buzzer and speaker stop.

8. Why is BC547 used?

It acts as a switching/driver transistor between the microcontroller output and the audible load.

9. Why is a 330 Ω resistor used?

It is connected between P3.2 and the transistor base to limit the base current.

10. Why is a debounce delay required?

Mechanical push buttons can generate rapid unwanted transitions during switching. A short delay helps prevent false triggering.

11. What is the purpose of reg51.h?

It provides definitions for the 8051 microcontroller registers and ports.

12. What does sbit do?

It allows an individual bit of an 8051 register to be given a meaningful name.

13. What does sbit BUTTON = P1^2; mean?

It assigns the name BUTTON to bit 2 of Port 1, i.e. P1.2.

14. What does sbit BUZZER = P3^2; mean?

It assigns the name BUZZER to P3.2.
15. What is the output when P1.2 is LOW?
P3.2 is LOW and the buzzer/speaker are OFF.
16. What is the output when P1.2 is HIGH?
P3.2 becomes HIGH and the buzzer/speaker are ON.
20. Result

The push button was successfully interfaced with the AT89C51 microcontroller. When the push button was pressed, the microcontroller activated the BC547 transistor, which switched ON the buzzer and speaker. When the push button was released, the buzzer and speaker were switched OFF successfully. Thus, the required push-button-controlled buzzer and speaker operation was achieved.
