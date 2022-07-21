# Arduino-Session-Recap
This is a recap of the Arduino session that is part of Aquaphoton Academy's training.



## Table of contents
**[Introduction to Arduino](#introduction-to-arduino)**<br>
**[What is a microcontroller?](#what-is-a-microcontroller)**<br>
**[Digital Input Output: Behind the Scenes](#digital-input-output-behind-the-scenes)**<br>
**[Digital Input](#digital-input)**<br>
**[Analog to Digital Converter ADC](#analog-to-digital-converter-adc)**<br>
**[Timers and millis()](#timers-and-millis)**<br>
**[Pulse Width Modulation PWM](#pulse-width-modulation-pwm)**<br>
**[Serial Communication UART](#serial-communication-uart)**<br>
**[Useful Links](#userful-links)**<br>
<br>
<br>
<br>

# Introduction to Arduino
'Arduino' is a tool that helps us control a hardware circuit in the simplest way possible. <br>
It can refer to two different things: the hardware and the software. <br>

## Arduino Development Boards

An `Arduino` Development Board simplifies the connections of a standard microcontroller and adds clear labels to
most pins to make it easier to work with. It also allows us to upload the code using a usb cable instead of a seperate programmer that needs special software to work. <br>

![image](https://user-images.githubusercontent.com/58588893/180078057-7c15cb55-e6fe-48b0-af07-8d603547307c.png)

## Arduino IDE
Similar to Pycharm and Codeblocks, the `Arduino` IDE is where we write our code before we upload it to the `Arduino` Development Board. 
 `Arduino` provides us with a huge set of simple libraries and functions that allow us to work with any component without much in-depth knowledge about it.<br>
 Another feature that the `Arduino` IDE provides is that it can work with nearly every microcontroller and not only `Arduino` Development Boards.


![image](https://user-images.githubusercontent.com/58588893/180081103-2fd642b6-1a45-4812-a158-90f0b819aaaf.png)

[Jump back to the top](#table-of-contents)<br>
---

# What is a microcontroller?
A microcontroller is simply a microprocessor, which only handles and executes binary instructions, that interacts with the real world with the help of 
peripherals.

![image](https://user-images.githubusercontent.com/58588893/180081654-7cae3eeb-86e3-4b67-b416-23fbc381a406.png)<br>

## Microcontroller Pinout
Every microcontroller has a set of pins that can do multiple functions. As we can see in the Atmega328 microcontroller (the one used in `Arduino` Uno), there are
digital pins, analog pins, PWM pins, Rx & Tx pins (Serial), and others.

Atmega328 Pinout           |Arduino Uno Pinout
:-------------------------:|:-------------------------:
![ATmega328-Pinout](https://user-images.githubusercontent.com/58588893/180082312-39643b97-2987-47f8-853d-da7718c5b184.png)|![arduino_uno_pinout](https://user-images.githubusercontent.com/58588893/180083021-156ffb2e-f81c-46d5-96f3-4d6876c59974.png)




[Jump back to the top](#table-of-contents)<br>
---


# Digital Input Output: Behind the Scenes

## Blink Example Code

The Blink example code is the hello world of `Arduino` development. Below are the functions used in it and their explanation:

| Function                  | Description                                                                         | 
| --------------------------|:-----------------------------------------------------------------------------------:| 
| `pinMode()`               | Configures the specified pin to behave either as an input or an output              | 
| `digitalWrite()`          | Write a HIGH or a LOW value to a digital pin.                                       | 
| `delay()`                 | Pauses the program for the amount of time (in milliseconds) specified as parameter. | 

`LED_BUILTIN` is a predefined macro by `Arduino` and in the case of `Arduino` Uno it refers to pin 13.

![image](https://user-images.githubusercontent.com/58588893/180084797-b20a5154-8939-412a-9946-23b41917eec0.png)<br>

## How does it actually work

Internally, the microcontroller is able to control a digital pin through a peripheral called Digital Input Output
(DIO). The peripheral consists of 3 registers each 1 byte in size; so we can imagine it as a box with 8 empty slots (bits).
Each bit is responsible for 1 digital pin.<br><br>
The `Data Direction Register` controls whether a pin is input or output. If it's output, then it can output HIGH and LOW voltage levels
(5V and GND). If it's input, then it can be connected to something like a switch and detect when it's on and when it's off.<br><br>
`The Data Register` is where we decide if we want an output of HIGH(1) or LOW(0) voltage.<br><br>
`The Input Pins Register` is where the input pins store the detected values. A 1 at bit 6 indicates that Pin6 has detected a HIGH level on it.<br>

![data_direction](https://user-images.githubusercontent.com/58588893/180155970-c129c7d9-4f1b-4ac3-8bda-3a44c8c41cdf.png)
![data_register](https://user-images.githubusercontent.com/58588893/180155997-932ca72d-56ea-4288-95ff-0ff189c100fe.png)
![input_pins](https://user-images.githubusercontent.com/58588893/180156022-71dd5c7b-f898-4579-b59a-a5ac748de66c.png)<br>

## All possible combinations for data direction and data registers


| Direction Bit | Data Bit | Pin State      |
| --------------|:--------:|:--------------:|
| 0             | 0        | Input Floating |
| 0             | 1        | Input Pull-Up  |
| 1             | 0        | Output LOW     |
| 1             | 1        | Output HIGH    |

<br>

## Input Floating vs Input Pull-Up

Suppose we have a button connected to an input pin like the following image.
If the button is pressed the input pin will be connected to GND and thus detect LOW voltage level and put 0 in its corresponding bit in `Input Pin Register`.
But if the button is not pressed, the input pin will be connected to air and we won't have a certain prediciton on what it will detect as noise can cause it to detect
either LOW or HIGH voltage levels.

![input_floating](https://user-images.githubusercontent.com/58588893/180160243-e42def97-675e-44b9-97f3-53bd01e56002.png)<br>

An easy solution to this problem is use a Pull-Up resistance. We put before the button a node connected to VCC and add a resistance so we don't create a short circuit.
Therefore when the button is not pressed, input pin will detect a HIGH voltage level and when the button is pressed it will detect a LOW voltage level.<br><br>

We don't need to add a Pull-Up resistance ourselves as they are built-in the microcontroller at every input pin. We can activate them by putting 1 in the `Data Register` while the pin is in input mode.

![input_pullup](https://user-images.githubusercontent.com/58588893/180161175-4c7f5b3e-b6e1-40e8-bee5-b1355785e88f.jpg)


[Jump back to the top](#table-of-contents)<br>
---

# Digital Input
[Jump back to the top](#table-of-contents)<br>
---

# Analog to Digital Converter ADC
[Jump back to the top](#table-of-contents)<br>
---

# Timers and millis()
[Jump back to the top](#table-of-contents)<br>
---

# Pulse Width Modulation PWM
[Jump back to the top](#table-of-contents)<br>
---

# Serial Communication UART
[Jump back to the top](#table-of-contents)<br>
---

# Userful Links
[List of microcontrollers supported by `Arduino`](https://github.com/per1234/ino-hardware-package-list/blob/master/ino-hardware-package-list.tsv)
[Jump back to the top](#table-of-contents)<br>
---


















