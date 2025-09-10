# EXPERIMENT-02-Interfacing-Multiple-Switches-for-LED-Control-Using-MicroPython


 
## NAME:Pragaharshitha NC

## DEPARTMENT:CSE(IOT)

## ROLL NO:212222110033


## AIM

To interface multiple switches with the Raspberry Pi Pico and control LEDs using MicroPython.

## APPARATUS REQUIRED

Raspberry Pi Pico

2 Push Button Switches

2 LEDs (Light Emitting Diodes)

330Ω Resistors

Breadboard

Jumper Wires

USB Cable

## THEORY



FIGURE-01: RASPBERRY PI PICO PINOUT DIAGRAM

Raspberry Pi Pico is a microcontroller board based on the RP2040 chip. It supports MicroPython, making it suitable for IoT and embedded applications. The Raspberry Pi Pico is a compact microcontroller board featuring a 40-pin layout, including power, ground, GPIO, and communication interface pins. It operates with a dual-core ARM Cortex-M0+ processor and supports MicroPython and C/C++ programming.

The power pins include VBUS (5V from USB), VSYS (1.8V to 5.5V input), 3V3(OUT) (regulated 3.3V output), and multiple ground (GND) connections. The board offers 26 multi-purpose GPIO pins (GP0 to GP28), which can be used for digital input, output, PWM, and communication interfaces such as I2C, SPI, and UART. It also features three analog-to-digital converter (ADC) pins (GP26, GP27, GP28), used for reading analog sensor values, along with an ADC_VREF pin to set the reference voltage.

For communication, I2C (SDA, SCL), SPI (MOSI, MISO, SCK), and UART (TX, RX) interfaces are mapped across different GPIO pins, allowing seamless connectivity with sensors and peripherals. All GPIO pins support PWM (Pulse Width Modulation), making it useful for motor control, LED brightness adjustment, and sound applications. The BOOTSEL button enables USB mass storage mode for firmware flashing, while the DEBUG pins (SWD interface) provide debugging capabilities. With its low power consumption, flexible GPIO options, and rich interface support, the Raspberry Pi Pico is widely used for IoT, embedded systems, robotics, and automation projects.

WORKING PRINCIPLE

The switches are connected as inputs to GPIO pins of the Pico.

The LEDs are connected as outputs.

A MicroPython script reads the switch states and controls the LEDs accordingly.

### CIRCUIT DIAGRAM
 ![image](https://github.com/user-attachments/assets/1c7234b9-5041-4156-94b8-0b846adb6b8e)
    Figure-01 circuit diagram of digital input interface 


Connect switch 1 to GP2 and switch 2 to GP3.

Connect LED 1 to GP14 via a 330Ω resistor.

Connect LED 2 to GP17 via a 330Ω resistor.

Connect the other terminals of the switches to GND.

## PROGRAM (MicroPython)

FIG1

```
from machine import Pin
import time

led = Pin(0, Pin.OUT)

switch = Pin(1, Pin.IN, Pin.PULL_DOWN)

while True:
    if switch.value() == 1:   
        led.value(1)
        print("Switch ON → LED ON")
    else:                    
        led.value(0)
        print("Switch OFF → LED OFF")
    
    time.sleep(0.1)

```
FIG2

```
from machine import Pin
import time

led1 = Pin(0, Pin.OUT)  
led2 = Pin(22, Pin.OUT)   

switch1 = Pin(1, Pin.IN, Pin.PULL_UP)  
switch2 = Pin(21, Pin.IN, Pin.PULL_UP)  

while True:
    s1 = 1 - switch1.value()
    s2 = 1 - switch2.value()

    state = (s1 << 1) | s2  
    if state == 0b00:        
        led1.value(0)
        led2.value(0)

    elif state == 0b01:      
        led1.value(0)
        led2.value(1)

    elif state == 0b10:       
        led1.value(1)
        led2.value(0)

    elif state == 0b11:      
        led1.value(1)
        led2.value(1)

    time.sleep(0.05)

```

## OUTPUT

FIGURE-01:

<img width="1920" height="1080" alt="486399714-143544a0-cbe8-4b92-b0b0-1c6324197d31" src="https://github.com/user-attachments/assets/5db38453-ffd1-41f4-a10e-ab0ffe4465ce" />

FIGURE-02:

<img width="1920" height="1080" alt="486399855-3572b4dd-df6e-4e87-88ad-3c178ff79e4b" src="https://github.com/user-attachments/assets/5245962d-c69d-403e-8b5e-d7dffaaa3382" />


## RESULTS:

The multiple switches connected to the Raspberry Pi Pico successfully controlled the LEDs based on their states, confirming the proper interfacing of digital inputs and outputs.

