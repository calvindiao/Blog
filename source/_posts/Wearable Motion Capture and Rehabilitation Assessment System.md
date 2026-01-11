---
title: Wearable Motion Capture and Rehabilitation Assessment System
date: 2022-5-20 5:06:03
updated: 2022-5-23
tags: [Embedded, C/modern C++, Real-time, STM32, Wearable, IMU, Kalman Filter, Motion Capture, MATLAB, Rehab]
permalink: /wearable-rehab-mocap/
---

I built a  **high-precision wearable motion capture & rehabilitation assessment system** designed for **stroke patients** to perform **home-based rehab training** with **3D motion reconstruction**.  

<p class="excerpt-cover" align="center">
  <img src="/assets/mocap/prototype.png" width="55%">
</p>


<!-- more -->

<style>
.excerpt-cover { display: none !important; }
</style>
The system integrates multiple **hardware** and **software** technologies, covering **multi-IMU sensing**, **quaternion-based Kalman fusion**, **wireless streaming (UART)**, and a **PC-side inverse kinematics (IK) evaluation tool** (MATLAB + OpenSim) to visualize motion and quantify joint **ROM (Range of Motion)**. The goal was simple: make rehab feedback **more objective, more accessible, and easier to use**. 🦾

---

### 🧩 System Overview

**Workflow: Capture → Fusion → Transmit/Store → IK Analysis → Rehab Metrics**

- Wearable device captures motion using **9-axis IMU modules**
- Firmware performs **real-time fusion** and outputs limbs angles
- Data is **wirelessly (UART) transmitted** to PC and also **logged to SD card**
- PC tool performs **inverse kinematics Algorithm** to replay motion and compute **ROM metrics**

---

### 🧠 Software Development

<p align="center">
  <img src="/assets/mocap/Kalman filter.png" width="70%">
  <br>
  <em>Kalman Filtering Algorithm</em>
</p>

- Implemented a **Quaternion-based Kalman Filtering algorithm** to fuse data from accelerometers, gyroscopes, and magnetometers, effectively solving Euler angle gimbal lock and sensor drift issues. 
- Developed the embedded firmware in **C/C++**on the **STM32L0 platform**, managing task scheduling and low-power operation. 
- Built a host analysis system using **MATLAB** to perform **Inverse Kinematics (IK)** Algorithm. This allows for precise reconstruction of limbs motions based on sensor data. 
- Ported the **FATFS file system** to enable high-speed, real-time offline storage of motion data onto an SD card via the SDIO interface. 

---

### ⚙️ Hardware and Mechanical Design

<p align="center">
  <img src="/assets/mocap/hardware workflow.png" width="70%">
  <br>
  <em>Hardware Workflow</em>
</p>

- Designed a distributed hardware architecture using three **STM32L071 (Low Power)** MCUs. Two units act as sensor nodes (processing **IMU** data), while the central unit handles data aggregation and transmission. 

- Designed **custom PCB boards** integrating **TPS5430 power management** for stable voltage regulation and signal isolation to prevent digital noise from affecting analog measurements. 

- Integrated a **2.4G wireless transmission module (NRF24L01 based)** to replace traditional wired connections, allowing patients unrestricted movement range during rehabilitation exercises. 

- Modeled and manufactured **3D-printed PLA enclosures** using **Fusion360**. The design features a magnetic slide-lid mechanism and ergonomic strap mounts for easy patient wearability. (Thanks for my best friend Ruizhe Zhou's helps!)

  <p align="center">
    <img src="/assets/mocap/3D Modeling.png" width="70%">
    <br>
    <em>3D-printed PLA enclosures</em>
  </p>

---

### 💡  Key Innovations

- The system achieves an average knee joint angle measurement error of only **3°** through rigorous static and dynamic testing, meeting high accuracy. 
- **Inverse Kinematics Integration**: Unlike simple angle measurement devices, this system utilizes motion capture data for inversion. This provides doctors with clinically relevant **Range of Motion (ROM)** data for remote diagnosis. 
- The system focuses on **home-based rehabilitation**. It is lightweight, wireless, and includes a "push-pull" magnetic switch structure designed specifically for ease of use by stroke patients. 

---

### 📸 Project Gallery

<p align="center">
  <img src="/assets/mocap/prototype.png" width="65%">
  <br>
  <em>Prototype</em>
</p>
<p align="center">
  <img src="/assets/mocap/prototype2.jpg" width="60%">
  <br>
  <em>Overhead view of the Wearable Device</em>
</p>
<p align="center">
  <img src="/assets/mocap/hardware.png" width="60%">
  <br>
  <em>Hardware PCB</em>
</p>
<p align="center">
  <img src="/assets/mocap/angle test.jpg" width="60%">
  <br>
  <em>Angle Test</em>
</p>








---

### 🎥 Competition Video

<p align="center">
  <iframe width="720" height="405" 
          src="https://www.youtube.com/embed/eKBgN3s-vVk"           
          title="Wearable Motion Capture Demo Video"
          frameborder="0"
          allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
          allowfullscreen>
  </iframe>
    <br>
  <em>Demo Video</em>
</p>




---

*This project aims to solve the issue of limited medical resources for stroke patients by enabling effective, unsupervised home rehabilitation training. It also demonstrates a full-stack integration of low-power embedded systems, sensor fusion algorithms, and animational modeling to achieve autonomous rehabilitation assessment.*
