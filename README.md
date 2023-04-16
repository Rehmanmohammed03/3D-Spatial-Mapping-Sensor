# 3D-Lidar-Scanner
# Embedded Spatial Measurement System

The embedded spatial measurement system was designed and built using a time-of-flight sensor to acquire information about the area around it. A rotary mechanism was used to provide a 360-degree measurement of distance within a single vertical geometric plane (y-z), while fixed distance samples were integrated along the orthogonal axis (x-axis). Mapped spatial information was stored in onboard memory and later communicated to a personal computer or web application for reconstruction and graphical presentation.

## Objective

The project was undertaken with the objective of creating a less expensive and smaller custom system suitable for indoor exploration and navigation, as commercial Light Detection and Ranging (LIDAR) equipment was deemed too expensive and bulky. The project was designed as a way for students to gain insight into how commercial/industrial data acquisition systems operate while gaining the capability to collect data using a microcontroller and process and communicate that data.

## Project Approach

The project involved a design-test-build approach, with lectures, studios, labs, and assigned work to complete the recommended milestones. The required tasks, corresponding to the steps illustrated in Figure 1, were:

- Quantifying the analog signal - range of amplitude, frequency, source, impedance (continuous signal)
- Building/selecting the appropriate transducer - pressure, sound, temperature, etc.
- Preconditioning the signal - amplifying, filtering, and/or level shifting to conform to ADC design
- Analog-to-Digital Conversion (ADC) - determining voltage range (min, max), resolution, sampling frequency (discrete data)
- Data processing - reading data from ADC and storing/processing/transmitting under time constraints to return to the ADC for the next conversion
- Control/communication - implementing an algorithm that meets the objective with hardware and timing constraints.

## Components

Core components of the project included:

- Digital I/O
- Momentary push button to start and stop the data acquisition process
- Microcontroller
- Other electronic components

The project used the VL53L1X Time of Flight (ToF) sensor on a predesigned breakout board mounted to a stepper motor for measuring planar spatial distance. The sensor was rotated through 360 degrees while collecting measurements. The data sheet for the ToF sensor lists three distance modes: 136cm (4.5ft), 290cm (9.5ft), and 360cm (11.8ft), and selecting the mode was one of the design decisions that had to be made for the project implementation. All communication between the ToF sensor and the microcontroller was done using a serial interface (I2C).

For displacement, the stepper motor/time of flight sensor combo was moved manually, and readings were gathered at regular distances (e.g., every 30 cm). The assembly of these components was also considered as a part of the final design, which may have required minor construction with wood, plastic, 3D printing, Lego pieces, etc., for which the students were responsible.

The resulting embedded system integrated measurement modalities and device control, allowing it to be used to map indoor environments, such as hallways, for use as a component of other systems (e.g., robotics navigation, autonomous drone, layout mapping, etc.).
# Embedded Spatial Measurement System

The embedded spatial measurement system was designed and built using a time-of-flight sensor to acquire information about the area around it. A rotary mechanism was used to provide a 360-degree measurement of distance within a single vertical geometric plane (y-z), while fixed distance samples were integrated along the orthogonal axis (x-axis). Mapped spatial information was stored in onboard memory and later communicated to a personal computer or web application for reconstruction and graphical presentation.

## Objective

The project was undertaken with the objective of creating a less expensive and smaller custom system suitable for indoor exploration and navigation, as commercial Light Detection and Ranging (LIDAR) equipment was deemed too expensive and bulky. The project was designed as a way for students to gain insight into how commercial/industrial data acquisition systems operate while gaining the capability to collect data using a microcontroller and process and communicate that data.

## Project Approach

The project involved a design-test-build approach, with lectures, studios, labs, and assigned work to complete the recommended milestones. The required tasks, corresponding to the steps illustrated in Figure 1, were:

- Quantifying the analog signal - range of amplitude, frequency, source, impedance (continuous signal)
- Building/selecting the appropriate transducer - pressure, sound, temperature, etc.
- Preconditioning the signal - amplifying, filtering, and/or level shifting to conform to ADC design
- Analog-to-Digital Conversion (ADC) - determining voltage range (min, max), resolution, sampling frequency (discrete data)
- Data processing - reading data from ADC and storing/processing/transmitting under time constraints to return to the ADC for the next conversion
- Control/communication - implementing an algorithm that meets the objective with hardware and timing constraints.

## Components

Core components of the project included:

- Digital I/O
- Momentary push button to start and stop the data acquisition process
- Microcontroller
- Other electronic components

The project used the VL53L1X Time of Flight (ToF) sensor on a predesigned breakout board mounted to a stepper motor for measuring planar spatial distance. The sensor was rotated through 360 degrees while collecting measurements. The data sheet for the ToF sensor lists three distance modes: 136cm (4.5ft), 290cm (9.5ft), and 360cm (11.8ft), and selecting the mode was one of the design decisions that had to be made for the project implementation. All communication between the ToF sensor and the microcontroller was done using a serial interface (I2C).

For displacement, the stepper motor/time of flight sensor combo was moved manually, and readings were gathered at regular distances (e.g., every 30 cm). The assembly of these components was also considered as a part of the final design, which may have required minor construction with wood, plastic, 3D printing, Lego pieces, etc., for which the students were responsible.

The resulting embedded system integrated measurement modalities and device control, allowing it to be used to map indoor environments, such as hallways, for use as a component of other systems (e.g., robotics navigation, autonomous drone, layout mapping, etc.).
