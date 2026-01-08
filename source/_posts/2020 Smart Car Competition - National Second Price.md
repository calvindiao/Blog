---
title: The 15th Smart Car Competition (2020) - National Second Prize
date: 2020-9-23 13:48:03
updated: 2020-9-23
tags:
permalink: /smart-car-2020/
---

We designed and built a **Mecanum-wheeled smart vehicle capable of rapidly locating and autonomously positioning an acoustic beacon**.  

<p class="excerpt-cover" align="center">
  <img src="/assets/2020/20200925_143817.jpg" width="70%">
</p>

<!-- more -->

<style>
.excerpt-cover { display: none !important; }
</style>

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
  <img src="/assets/2020/20200609_223638.jpg" width="70%">
  <br>
  <em>Prototype</em>
</p>
<p align="center">
  <img src="/assets/2020/20200925_143817.jpg" width="70%">
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
  <img src="/assets/2020/1598536641490.jpeg" width="70%">
  <br>
  <em>Part of Team photo</em>
</p>



<p align="center" style="display:flex; justify-content:center; gap:10px;">
  <img src="/assets/2020/15th%20smart%20vehicle%20First%20Prize%20in%20East%20China.jpg" width="30%">
  <img src="/assets/2020/15th%20smart%20vehicle%20second%20national%20Prize.jpg" width="30%">
</p>
<p align="center">
  <em>🏆 First Prize in East China and National Second Prize Certificates 🏆</em>
</p>





---

*This project demonstrates a full-stack integration of embedded systems, perception algorithms, and mechanical design to achieve autonomous sound source localization.*
