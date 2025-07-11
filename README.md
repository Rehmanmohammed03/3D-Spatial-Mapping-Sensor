3D LiDAR Scanner
Embedded Spatial Measurement System
<p align="center"> <img src="https://cdn.discordapp.com/attachments/514241789478174727/1097062007657734174/IMG_7747.png" alt="Embedded Spatial Measurement System" width="400"/> </p>
Overview
This embedded spatial measurement system was designed and built using a time-of-flight (ToF) sensor to capture environmental data. A rotary mechanism enabled 360-degree distance measurements within a single vertical geometric plane (Y-Z), while additional readings were taken at fixed intervals along the orthogonal X-axis. Spatial data was stored in onboard memory and later transmitted to a computer or web application for reconstruction and visualization.

Objective
The primary goal was to develop a cost-effective and compact alternative to commercial LiDAR systems, which are often bulky and expensive. This project gave students hands-on experience with real-world data acquisition systems, including working with microcontrollers for data collection, processing, and communication.

Project Methodology
The project followed a design-test-build process supported by lectures, labs, and milestone-driven assignments. Key technical steps included:

Signal quantification: Determining the amplitude, frequency range, source, and impedance of the analog signal.

Transducer selection/building: Choosing appropriate sensors (e.g., pressure, sound, temperature).

Signal preconditioning: Amplifying, filtering, and level-shifting to prepare for ADC.

Analog-to-Digital Conversion (ADC): Defining voltage range, resolution, and sampling frequency.

Data processing: Managing real-time data from the ADC for storage, analysis, and communication.

Control & communication: Implementing algorithms that operate within hardware and timing constraints.

System Components
Core hardware included:

A VL53L1X ToF sensor mounted on a stepper motor to scan planar distances.

A microcontroller for control and communication via I2C.

A momentary push button to start/stop data acquisition.

Supporting electronic components and structural materials (e.g., wood, 3D-printed parts, Lego).

The VL53L1X sensor offers three distance modes—136 cm, 290 cm, and 360 cm—requiring thoughtful mode selection during implementation. The stepper motor rotated the sensor 360° for full planar scanning. To extend measurements across the X-axis, the assembly was manually repositioned (e.g., every 30 cm) and additional data was collected.

Final Outcome
The resulting embedded system successfully integrated sensor control, spatial measurement, and data communication, enabling it to map indoor spaces such as hallways. It can serve as a component in broader applications like robotic navigation, autonomous drone pathfinding, and environmental layout mapping.
