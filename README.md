# Gesture-Based Pneumatic Control System

A pneumatic cylinder control setup where a webcam detects hand gestures, Python processes the finger positions, and an Arduino controls LEDs and a solenoid-operated valve to move the cylinder.

The idea is to use hand gestures as a contactless input instead of a physical switch. Python handles the computer vision, while the Arduino manages the hardware outputs.

## How it works

A webcam captures live video of the user's hand. Using OpenCV and CVZone's `HandDetector`, the program detects the hand and identifies which fingers are raised. The `fingersUp()` function returns a list representing the finger positions, and we use `sum()` to calculate the total number of raised fingers.

The detected finger count is then passed to a separate Python file, `controller.py`. This file uses PyFirmata to communicate with the Arduino running StandardFirmata, allowing Python to control the Arduino's digital output pins.

Five LEDs provide visual feedback based on the detected finger count. As more fingers are raised, additional LEDs turn on. This provides a simple visual indication of the gesture recognized by the system.

The relay is used to control a 24V solenoid-operated 5/2 directional control valve connected to a double-acting pneumatic cylinder. When five fingers are detected, the relay energizes the valve to command cylinder extension. When no fingers are detected, the relay de-energizes, allowing the valve's spring-return position to command retraction.

## Steps in order

1. Capture live video from the webcam
2. Detect the hand using CVZone
3. Identify raised fingers and calculate the finger count
4. Pass the detected gesture to `controller.py`
5. Communicate with the Arduino using PyFirmata
6. Switch the LEDs according to the finger count
7. Activate or deactivate the relay based on the gesture
8. Operate the pneumatic cylinder through the directional control valve

## What we used

- USB webcam
- Arduino Uno
- Double-acting pneumatic cylinder
- 5/2 solenoid-operated directional control valve
- Relay module
- LEDs with current-limiting resistors
- Python
- OpenCV and CVZone
- PyFirmata and Arduino StandardFirmata
- 24V DC power supply for the valve, if specified by the valve's rating

## Challenges

- **Real-time gesture detection:** Getting reliable finger detection from the webcam feed.
- **Software–hardware communication:** Connecting Python's gesture recognition output to Arduino through PyFirmata.
- **Gesture-to-output mapping:** Ensuring the LEDs and relay respond correctly to the detected finger count.
- **Pneumatic integration:** Connecting the relay-controlled solenoid valve to the double-acting cylinder and verifying the extension and retraction directions.
- **Electrical interfacing:** Keeping the Arduino control signals separate from the valve's 24V power circuit and ensuring the relay module is compatible with the control voltage.

