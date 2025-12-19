---

# 3D LiDAR Scanner

### Embedded Spatial Measurement System

## Overview

This project is a custom built embedded spatial measurement system that functions as a low cost LiDAR style scanner. It uses a time of flight (ToF) distance sensor combined with a rotary scanning mechanism to capture environmental geometry.

The system performs continuous 360 degree distance measurements within a single vertical plane (Y–Z). By manually repositioning the scanner at fixed intervals along the X axis, multiple planar scans are combined to reconstruct a three dimensional representation of the surrounding environment. Collected data is stored onboard and later transmitted to a computer or web application for visualization.

## Motivation

Commercial LiDAR systems are often expensive, bulky, and inaccessible for students. The goal of this project was to design a compact and affordable alternative while gaining hands on experience with real world embedded sensing, motor control, and data acquisition systems.

## System Architecture

The system integrates sensing, motion control, and data handling into a single embedded platform.

### Hardware Components

* **VL53L1X Time of Flight sensor** for distance measurements
* **Stepper motor** for precise 360 degree planar scanning
* **Microcontroller** for sensor interfacing, motor control, and communication
* **Momentary push button** to start and stop data acquisition
* **Structural components** including wood, 3D printed parts, and Lego elements

The VL53L1X sensor supports three distance modes, 136 cm, 290 cm, and 360 cm. Mode selection was based on range and resolution tradeoffs. The stepper motor rotates the sensor through a full sweep to capture planar distance data.

## Scanning Methodology

1. The sensor is rotated 360 degrees to capture distance measurements within the Y–Z plane
2. Distance data is sampled at fixed angular increments
3. The system stores each scan in onboard memory
4. The entire assembly is repositioned along the X axis at fixed intervals, such as every 30 cm
5. Multiple planar scans are combined to reconstruct a 3D spatial map

## Firmware and Data Processing

The embedded firmware is responsible for:

* Controlling stepper motor motion and angular resolution
* Managing I2C communication with the ToF sensor
* Sampling and storing distance measurements
* Handling user input for scan control
* Preparing data for transmission to an external system

Timing constraints, memory limitations, and sensor configuration were carefully managed to ensure reliable and repeatable measurements.

## Results

The system successfully generated three dimensional representations of indoor environments such as hallways. The resulting data demonstrates the feasibility of using low cost components to implement LiDAR style spatial scanning.

## Applications

This project serves as a foundation for more advanced spatial sensing systems, including:

* Robotic navigation and obstacle detection
* Autonomous drone path planning
* Indoor mapping and environment reconstruction
* Embedded perception systems

## Future Improvements

* Automate X axis movement using a linear actuator
* Improve spatial resolution and noise filtering
* Add real time visualization support
* Integrate SLAM or point cloud processing pipelines

## Technologies Used

* Embedded C or C++
* I2C communication
* Stepper motor control
* Time of Flight sensing
* Embedded systems design

---

Just tell me.
