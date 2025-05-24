# Master-Slave Robotic Arm Project 

Author: Juan Martinez-Sagarra Coullaut-Valera

# Project Overview 

This repository contains the design and implementation of a modular master-slave robotic arm system controlled by a Raspberry Pi. The system uses a scaled-down master arm equipped with rotary encoders to control a larger slave arm that replicates its movements in real time. The project serves as a prototype for integration into a mobile quadruped or hexapod platform.

# Main goals:

Enable real-time teleoperation of a robotic arm

Achieve reliable manipulation of objects up to 500 g at a 30 cm reach

Provide a modular, expandable system for future mobile applications

# Slave Arm
Structure: 3D-printed matte black PLA, modular base, shoulder, elbow, wrist, gripper

Degrees of Freedom:

Base Yaw

Shoulder Pitch

Elbow Pitch

Wrist Pitch

Gripper (two-finger claw)

Actuators:

3x LewanSoul LX-16A smart servos (UART, ~17 kg·cm torque)

1x Hiwonder LX-15D smart servo (UART, ~17 kg·cm torque)

1x MG996R high-torque PWM servo (gripper actuation)


# Reach/Payload:

40 cm maximum reach

500 g payload at 30 cm

# Master Arm
Structure: Scaled-down mechanical replica of the slave arm; gripper replaced with pushbutton

Sensors:

4x AS5600 magnetic rotary encoders (12-bit, I2C, 0–360° absolute)

1x pushbutton for gripper toggle

Mounting: Panel-mounted for single-hand operation

Wiring and Communication
AS5600 encoders connected via TCA9548A I2C multiplexer

LX-16A and LX-15D servos connected via UART serial daisy-chain using USB-UART adapter

MG996R controlled using PWM from Raspberry Pi

Power Supply:

Raspberry Pi and sensors powered by 5V 5A supply

Servos powered by 7.4V Li-ion battery or 8V regulated adapter

Gripper button wired as GPIO input to Raspberry Pi

# Software Architecture
GUI implemented using Tkinter on Raspberry Pi

Features:

Manual slider controls for angle override

Teleop/Home toggle button (master arm control vs. preset positions)

Real-time debug log window

Automatic switch to Teleop when master arm is moved

Control Logic:

Encoders read via I2C, mapped to 0–180° angles

Servo commands sent over UART (LX servos) and PWM (MG996R)

Gripper controlled by pushbutton toggle

Libraries:

tkinter for GUI

adafruit-circuitpython-pca9685 (legacy, if used)

adafruit-blinka for I2C/SPI abstraction

Custom or open-source LX-16A/LX-15D servo control library

# Estimated Costs
Component	Qty	Est. Price
Raspberry Pi 4/5	1	$50–80
LewanSoul LX-16A Servos	3	$48 total
Hiwonder LX-15D Servo	1	$20
MG996R High-Torque Servo	1	$10
AS5600 Encoders	4	$20 total
TCA9548A Multiplexer	1	$6
UART-to-USB Adapter	1	$8
Power Supplies/Battery	1 set	$22–25
PLA Filament, Hardware	—	~$60
Total	—	~$250–280
