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

### 💡 Competition-winning Features

- The system employed **Dual MCU parallel computation**. One was dedicated to **vehicle control** and the other to **signal acquisition and processing**.  This separation significantly improved **system responsiveness** and **computational efficiency**.
- We dedicated and integrated a specialized **8-bit parallel ADC chip** for high-speed, high-precision data sampling, substantially improving signal accuracy compared to serial ADC solutions.
- Introduce **path prediction and dynamic obstacle avoidance algorithms** for more intelligent navigation.  

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
  <em>🏆 National Finals</em>
</p>


---



### 🏅 Team & Awards

<p align="center">
  <img src="https://img.pandior.ink/blog/1598536641490.jpeg" width="70%">
  <br>
  <em>Part of Team photo</em>
</p>



<p align="center" style="display:flex; justify-content:center; gap:10px;">
  <img src="https://img.pandior.ink/blog/%E7%AC%AC%E5%8D%81%E4%BA%94%E5%B1%8A%E6%99%BA%E8%83%BD%E8%BD%A6%E5%8D%8E%E4%B8%9C%E8%B5%9B%E5%8C%BA%E4%B8%80%E7%AD%89%E5%A5%96.jpg" width="30%">
  <img src="https://img.pandior.ink/blog/%E7%AC%AC%E5%8D%81%E4%BA%94%E5%B1%8A%E6%99%BA%E8%83%BD%E8%BD%A6%E5%85%A8%E5%9B%BD%E4%BA%8C%E7%AD%89%E5%A5%96.jpg" width="30%">
</p>
<p align="center">
  <em>🏆 First Prize in East China and National Second Prize Certificates 🏆</em>
</p>


---

*This project demonstrates a full-stack integration of embedded systems, perception algorithms, and mechanical design to achieve autonomous sound source localization.*
