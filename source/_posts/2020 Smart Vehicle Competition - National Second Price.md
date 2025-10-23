---
title: My first Smart Vehicle Competition (2020) - National Second Price
date: 2020-9-23 13:48:03
tags:
---

We designed and built a **Mecanum-wheeled smart vehicle capable of rapidly locating and autonomously positioning an acoustic beacon**.  

<!-- more -->

The project integrated multiple hardware and software technologies, covering **signal processing**, **control algorithms**, **embedded system design**, and **mechanical optimization**.

---

### 🧠 Software Development

- Implemented a multi-modal perception and control system, including **PID closed-loop control** and **Kalman filtering** for optimized attitude estimation and speed control.  
- Developed the main control logic in **C/C++**, supporting real-time algorithm debugging and optimization.  
- Integrated an **OpenMV (Python)** module for visual-assisted navigation, achieving **object recognition and localization**.  
- Applied **FFT** and **cross-correlation algorithms** for sound source localization, estimating direction by analyzing phase differences across a multi-microphone array.  
- Independently implemented a **gcc-path-based path planning algorithm**, improving trajectory tracking and obstacle avoidance efficiency.

---

### ⚙️ Hardware and Mechanical Design

- Completed the **mechanical structure design and modeling** of the entire vehicle, optimizing Mecanum wheel drive and chassis stability.  
- Designed **multi-layer PCB boards** integrating a **minimal MCU control unit**, **MOSFET driver circuits**, and **multi-channel power management modules**.  
- Implemented **high-speed signal shielding and protection circuits** to ensure stable operation under complex electromagnetic conditions.  
- Utilized an **IMU sensor** and **microphone array** for multi-source data fusion, enabling high-precision sound localization and motion control.

---

### 🚀 Future Improvements

- Introduce **path prediction and dynamic obstacle avoidance algorithms** for more intelligent navigation.  
- Develop a **PC-based monitoring system or web control interface** to support real-time system visualization and debugging.

---

### 📸 Project Gallery

<p align="center">
  <img src="https://img.pandior.ink/blog/20200925_143817.jpg" width="70%">
  <br>
  <em>Overhead view of the our vehicle</em>
</p>

---

### 🎥 Competition Video

<p align="center">
  <iframe width="720" height="405" 
          src="https://www.youtube.com/embed/9fxU5Fqx_os" 
          title="National Finals Video"
          frameborder="0"
          allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
          allowfullscreen>
  </iframe>
    <br>
  <em>🏆 National Finals Video</em>
</p>

---

*This project demonstrates a full-stack integration of embedded systems, perception algorithms, and mechanical design to achieve autonomous sound source localization.*
