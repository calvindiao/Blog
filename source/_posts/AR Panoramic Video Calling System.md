---
title: AR Panoramic Video Calling System (Rokid AR + Insta360 + Cloud Streaming)
date: 2025-12-09 17:28:33
updated: 2025-12-09
tags: [AR, VR, Unity, XR, Video Streaming, HLS, VolcEngine, Insta360, Rokid]
---

This is my M.Eng. master project. I built an **AR panoramic video calling system** that enhances an “immersive calling” experience: users can wear **Rokid Air AR glasses** and look around a remote environment in **360°**, as if stepping into the other person’s room. 🤩

<p class="excerpt-cover" align="center">
  <img src="/assets/AR/arcover.png" width="70%">
</p>

<!-- more -->

<style>
.excerpt-cover { display: none !important; }
</style>

The system follows a modular **capture → cloud distribution → playback** workflow: an **Insta360 X2** captures the scene and pushes the stream to the cloud, a cloud streaming platform transcodes/distributes it, and a **Unity-based AR calling app** renders the live panorama on Rokid with head-tracked viewing. 

---

### 🧠 Software Development

- Built the **Rokid AR Calling App** in **Unity (Android)** with Rokid UXR SDK integration for stereo rendering and **3DoF head tracking**. 
- Integrated **AVPro Video** as the live playback engine (HLS/M3U8), decoding the stream and mapping frames onto the inner surface of a sphere so the user stands inside a panoramic dome.
- Implemented **contact management** with JSON-based storage.
- Optimized call startup with a **preloading strategy** to avoid long waits/black screens by instantiating key resources (panorama materials/UI/plugin interfaces) in advance. 

---

### ⚙️ System & Cloud Design

- Used a cloud live streaming platform (VolcEngine) to ingest, transcode, and distribute the panoramic stream. The camera pushes via **RTMP**, while clients pull via **HLS (M3U8)** for broad compatibility. 
- Configured **push/pull domains** and DNS **CNAME** records (e.g., `push.example.com`, `pull.example.com`), enabling stable publishing and playback URLs for the AR app. 
- Leveraged CDN routing/edge selection so the client can fetch segments from an optimal node, improving stability under variable network conditions. 

---

### 💡 Project Highlights

- **Immersive rendering path:** MediaPlayer decodes the live stream → sphere mapping creates a full 360° environment, removing the “flat video window” feeling. 
- **Fast call establishment & stability validation:** after tapping “Call”, connection typically completes in **~3 to 5 seconds** while playback stayed smooth without obvious stutter. 
- **Cross-device extensibility:** the modular capture–cloud–playback workflow is designed to be reusable across AR and VR devices (e.g., AR - VR, AR - AR, VR - VR).

---

### 📸 Project Gallery

<p align="center">
  <img src="/assets/AR/workflow.png" width="70%">
  <br>
  <em>Workflow of the Panoramic Calling System</em>
</p>
<p align="center">
  <img src="/assets/AR/result2.png" width="70%">
  <br>
  <em>User wearing Rokid Air glasses during an AR Calling session</em>
</p>

<p align="center">
  <img src="/assets/AR/UML.jpeg" width="70%">
  <br>
  <em>UML of the AR Application</em>
</p>








---

### 🎥 Demo Video

<p align="center">
  <iframe width="720" height="405" 
          src="https://www.youtube.com/embed/shrMtn-MXbk"
          title="AR Panoramic Calling Demo"
          frameborder="0"
          allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
          allowfullscreen>
  </iframe>
    <br>
  <em>AR Panoramic Calling Demo</em>
</p>


---

### 🧪 Results & Limitations

- **Latency tradeoff (HLS):** an inherent **~2 to 5s** delay is expected; and cross-region routes can further increase delay.
- **Device constraints:** Rokid Air relies on a phone for compute; long sessions (~20 min) can cause heat and performance dips, with frame rate typically **15–30 fps** and occasional stutter during fast motion. 

---

*This project demonstrates an end-to-end XR pipeline designed for a stronger sense of remote presence than traditional video calls.*
