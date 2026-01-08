---
title: The 16th Smart Car Competition (2021) - National Second Prize
date: 2021-8-23 17:28:41
updated: 2021-8-23
tags: [embedded, C/CPP, PCB, PID, System]
permalink: /smart-car-2021/
---

Participating again for the second year, we developed a **self-balancing electric motorcycle** that autonomously follows an electromagnetic track using self-designed magnetic sensors. Without the aid of a flywheel, the vehicle maintains stability through precise **real-time control algorithms**.

<p class="excerpt-cover" align="center">
  <img src="/assets/2021/20210816_030631.jpg" width="70%">
</p>

<!-- more -->

<style>
.excerpt-cover { display: none !important; }
</style>

This project integrated a wide range of hardware and software technologies, including **electromagnetic signal processing**, **advanced fuzzy PID algorithms**, **power management IC design**, **schematic and PCB design**, and **embedded system integration** with MCU minimal circuit design, **I²C/UART/SPI** communication, and **DMA**-based data buffering.

---

### 🧠 Software Development

- Implemented a **Kalman filtering algorithm** to estimate the motorcycle’s accurate tilt angle and attitude based on **IMU sensor fusion**.

- Developed all control logic in **C/C++**, ensuring efficient real-time performance on the embedded MCU platform.

- Designed a **fuzzy PID control algorithm** to handle the nonlinear coupling between tilt angle and steering dynamics, enhancing stability and responsiveness.

  

---

### ⚙️ Hardware and Mechanical Design

- Completed the **mechanical structure design** and **3D modeling** of the vehicle, optimizing the self-balancing mechanism for a lightweight and compact structure. (See Below Picture)
- Designed **multi-layer PCB boards** integrating a **minimal MCU control unit**, **MOSFET driver circuits**, and **multi-channel power management modules**.  
- Implemented **analog–digital separation** in the PCB design, isolating **power and signal analog circuits** from **digital MCU sections** to reduce interference and improve system stability.

---

### 💡 Competition-winning Features

- Achieved an elegant and stable mechanical design, where precise weight distribution and a refined self-balancing structure significantly reduced the load of the balance control algorithm.

- Designed a **miniaturized PCB**, effectively reducing overall vehicle weight and enhancing the system’s compactness and aesthetic integration.

  

---

### 📸 Project Gallery

<p align="center">
  <img src="/assets/2021/20210824_190540.jpg" width="80%">
  <img src="/assets/2021/IMG_20210814_051006.jpg" width="80%">
  <img src="/assets/2021/IMG_20210814_051429.jpg" width="80%">
  <img src="/assets/2021/photo.jpg" width="80%">
  <br>
  <em>Overhead view of the our vehicle</em>
</p>


---

### 🎥 Competition Video

<p align="center">
  <iframe width="720" height="405" 
          src="https://www.youtube.com/embed/M-G5Jj6L29o" 
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
  <img src="/assets/2021/team photo.jpg" width="70%">
  <br>
  <em>Part of Team photo</em>
</p>



<p align="center" style="display:flex; justify-content:center; gap:10px;">
  <img src="/assets/2021/sixteenth First Prize in East China.jpg" width="30%">
  <img src="/assets/2021/sixteenth First Prize in China.jpg" width="30%">
</p>
<p align="center">
  <em>🏆 First Prize in East China and National Second Prize Certificates 🏆</em>
</p>





---

*This project showcases a end-to-end embedded system design, including sensor fusion, real-time control, PCB design, and mechanical optimization, to achieve stable self-balancing and autonomous track following.*
