# Embedded Spatial Measurement System

A custom-built **embedded LiDAR-style spatial measurement system** that uses a **VL53L1X Time-of-Flight (ToF) sensor** and a motorized scanning mechanism to capture environmental geometry and reconstruct 3D spatial maps.

The system performs continuous **360° planar scans in the Y-Z plane**. By repositioning the scanner along the X-axis at fixed intervals, multiple 2D scans can be combined to generate a 3D representation of the surrounding environment.

The project combines **embedded firmware, sensor interfacing, motor control, data acquisition, memory management, and 3D point-cloud reconstruction**.

## Overview

```text
                    Physical Environment
                            |
                            v
                  +-------------------+
                  |   VL53L1X ToF     |
                  |      Sensor       |
                  +-------------------+
                            |
                           I2C
                            |
                            v
                  +-------------------+
                  |   Microcontroller |
                  |                   |
                  | Sensor Interface  |
                  | Motor Control     |
                  | Data Acquisition  |
                  | Memory Management |
                  +-------------------+
                     |             |
                   GPIO           UART
                     |             |
                     v             v
              +-----------+   +----------+
              |  Stepper  |   | Host PC  |
              |   Motor   |   | / Python |
              +-----------+   +----------+
                                  |
                                  v
                         +----------------+
                         | 3D Point Cloud |
                         | Reconstruction |
                         +----------------+
                                  |
                                  v
                           Spatial Map
```

## Motivation

Commercial LiDAR systems can be expensive and difficult to access for student projects. The goal of this project was to develop a **low-cost embedded alternative** while gaining practical experience with:

* Embedded sensing
* Time-of-Flight measurement
* I2C communication
* Stepper motor control
* GPIO interfaces
* Data acquisition
* Embedded memory management
* UART communication
* 3D spatial reconstruction

The resulting system demonstrates how relatively inexpensive embedded components can be combined to create a functional spatial scanning platform.

## Key Features

* 360° motorized spatial scanning
* VL53L1X Time-of-Flight distance sensing
* I2C sensor communication
* Stepper motor control through GPIO
* Fixed-angle measurement sampling
* Onboard measurement storage
* UART data transmission
* Python-based 3D reconstruction
* Point-cloud visualization
* Y-Z planar scanning
* X-axis scan repositioning
* Indoor environment reconstruction

## Hardware Components

| Component             | Purpose                                         |
| --------------------- | ----------------------------------------------- |
| VL53L1X ToF Sensor    | Distance measurement                            |
| Microcontroller       | Sensor interface, control, and data acquisition |
| Stepper Motor         | 360° rotational scanning                        |
| Push Button           | Start/stop scan control                         |
| Structural Components | Sensor and motor mounting                       |
| Host Computer         | Data processing and visualization               |

The mechanical structure was constructed using a combination of **wood, 3D-printed components, and Lego elements**.

## VL53L1X Time-of-Flight Sensor

The **VL53L1X** provides distance measurements by determining the time required for emitted light to travel to an object and return to the sensor.

The sensor supports multiple distance modes:

| Mode   | Maximum Range |
| ------ | ------------: |
| Short  |        136 cm |
| Medium |        290 cm |
| Long   |        360 cm |

The selected mode provides a tradeoff between **measurement range and spatial resolution**, depending on the scanning environment.

The microcontroller communicates with the sensor through **I2C**.

```text
+----------------+              +----------------+
| Microcontroller|              |    VL53L1X     |
|                |              |                |
| I2C Controller | <----------> | ToF Sensor     |
+----------------+              +----------------+
```

## 360° Scanning Mechanism

A stepper motor rotates the ToF sensor through a complete **360° sweep**.

Distance measurements are collected at fixed angular increments, allowing the system to associate each measurement with a known scanning angle.

```text
                  Sensor
                    *
                    |
                    |
            \       |       /
             \      |      /
              \     |     /
               \    |    /
                \   |   /
                 \  |  /
                  \ | /
                   \|/
              -----+-----
                   |
             Scanner Center
```

Each measurement therefore contains information about both:

* Distance from the sensor
* Angular position of the sensor

This allows the planar geometry to be reconstructed.

## Scanning Methodology

The system uses a multi-stage scanning process.

### Step 1. Planar Scan

The stepper motor rotates the ToF sensor through 360°.

Distance measurements are collected at predefined angular increments.

```text
             Y-Z Plane

                  *
              *       *
           *             *
         *                 *
        *        SENSOR     *
         *                 *
           *             *
              *       *
                  *
```

This produces a 2D representation of the environment within the scanning plane.

### Step 2. Store Measurements

Distance measurements and their associated scan positions are stored onboard.

The firmware manages the measurement collection process while ensuring that sensor data is captured at the required intervals.

### Step 3. Reposition Along X

After completing a planar scan, the scanner is manually repositioned along the **X-axis**.

For example:

```text
Scan 1       Scan 2       Scan 3       Scan 4
  |            |            |            |
  v            v            v            v
 X = 0 cm    X = 30 cm    X = 60 cm    X = 90 cm
```

### Step 4. Combine Planar Scans

Multiple Y-Z scans are combined using their known X-axis positions.

```text
        X
        ^
        |
Scan 4  |       / /
        |      / /
Scan 3  |     / /
        |    / /
Scan 2  |   / /
        |  / /
Scan 1  | / /
        +-----------------> Y
       /
      /
     v
     Z
```

This produces a three-dimensional representation of the scanned environment.

## Firmware Architecture

The embedded firmware is responsible for coordinating sensing, motion, user input, memory, and communication.

```text
+----------------------+
|      Main Control    |
+----------+-----------+
           |
     +-----+-----+
     |           |
     v           v
+---------+   +-------------+
| Sensor  |   | Motor       |
| Driver  |   | Controller  |
+---------+   +-------------+
     |           |
     |           |
     +-----+-----+
           |
           v
    +-------------+
    | Measurement |
    | Storage     |
    +-------------+
           |
           v
    +-------------+
    | UART        |
    | Transmission|
    +-------------+
```

### Firmware Responsibilities

The firmware handles:

* VL53L1X initialization
* I2C communication
* Distance measurement acquisition
* Stepper motor control
* Angular scan positioning
* Measurement storage
* Push-button input
* Scan start/stop control
* UART data transmission

## I2C Communication

The microcontroller communicates with the VL53L1X through the **I2C bus**.

The firmware configures the sensor and retrieves distance measurements during each scanning cycle.

```text
Microcontroller
      |
      | SDA
      | SCL
      |
      v
VL53L1X
```

This provided hands-on experience with low-level digital communication between an embedded processor and external sensing hardware.

## Stepper Motor Control

The stepper motor provides controlled rotational movement of the sensor.

GPIO signals are used to control the motor driver and determine the scanning position.

The firmware coordinates motor movement with sensor acquisition so that measurements correspond to known angular positions.

```text
        Motor Controller
               |
              GPIO
               |
               v
        +-------------+
        |   Stepper   |
        |    Motor    |
        +-------------+
               |
               v
        Rotate Sensor
               |
               v
        Take Measurement
```

This synchronization between **motion and sensing** is critical for producing geometrically meaningful measurements.

## Data Acquisition

During a scan, the embedded system repeatedly performs:

```text
Move Motor
    |
    v
Reach Scan Position
    |
    v
Trigger / Read ToF Measurement
    |
    v
Store Distance
    |
    v
Move to Next Position
    |
    v
Repeat
```

The process continues until the sensor completes a full 360° sweep.

## UART Communication

Collected measurements are transmitted to an external computer through **UART**.

```text
+-------------+       UART       +----------------+
| Microcontroller | -----------> | Host Computer  |
+-------------+                  +----------------+
                                        |
                                        v
                                  Python Processing
```

This provides a simple interface for transferring embedded measurement data into the higher-level reconstruction pipeline.

## 3D Point-Cloud Reconstruction

The host-side software converts the collected measurements into spatial coordinates.

For a measurement at distance `r` and angle `θ`, the corresponding planar coordinates can be represented using:

```text
y = r cos(θ)

z = r sin(θ)
```

The scanner's X-axis position is then used as the third coordinate:

```text
x = scanner_position
```

The resulting points form a 3D point cloud:

```text
             Z
             ^
             |
             |       •
             |    •     •
             |  •         •
             | •           •
             +-----------------> Y
            /
           /
          /
         X
```

The reconstructed point cloud can then be visualized and analyzed using **Python and Open3D**.

## Python / Open3D Processing

The host-side processing pipeline is responsible for:

* Receiving measurement data
* Parsing scan measurements
* Associating measurements with scan angles
* Applying X-axis scan positions
* Converting measurements to Cartesian coordinates
* Generating point-cloud data
* Visualizing the reconstructed environment

```text
UART Data
    |
    v
Python Parser
    |
    v
Distance + Angle + X Position
    |
    v
Coordinate Transformation
    |
    v
3D Point Cloud
    |
    v
Open3D Visualization
```

## Memory and Timing Constraints

Because the system performs continuous sensing on an embedded platform, firmware design had to account for limited resources.

Important considerations included:

* Measurement storage capacity
* Sensor sampling timing
* Motor positioning delays
* Communication timing
* Processing overhead
* Reliable data acquisition

The firmware was designed to maintain consistent measurement timing and prevent data loss during scanning.

## Results

The system successfully generated **3D representations of indoor environments**, including hallway-like environments.

The resulting point clouds demonstrate that a low-cost ToF sensor and motorized scanning mechanism can be used to capture meaningful spatial geometry.

Example reconstruction workflow:

```text
Physical Environment
        |
        v
  360° Planar Scan
        |
        v
   Measurement Set
        |
        v
Move Scanner Along X
        |
        v
 Repeat Planar Scan
        |
        v
Combine Multiple Scans
        |
        v
  3D Point Cloud
```

## Applications

The system provides a foundation for several embedded perception applications:

* Robotic navigation
* Obstacle detection
* Indoor mapping
* Environment reconstruction
* Autonomous vehicle perception
* Drone path planning
* Embedded robotics
* Spatial sensing systems

## Technologies Used

### Embedded

* C / C++
* Microcontroller Firmware
* GPIO
* I2C
* UART
* Stepper Motor Control
* Time-of-Flight Sensing
* Embedded Memory Management

### Sensors & Hardware

* VL53L1X ToF Sensor
* Stepper Motor
* Microcontroller
* Push Button
* Custom Mechanical Assembly

### Software

* Python
* Open3D
* 3D Point-Cloud Processing
* Data Visualization

## Skills Demonstrated

* Embedded Systems Development
* C/C++ Firmware
* Sensor Integration
* I2C Communication
* UART Communication
* GPIO Programming
* Motor Control
* Data Acquisition
* Real-Time Embedded
