---
title: Exploration of a Sound Localization Solution for the Beacon Group in the 15th National University Intelligent Vehicle Competition
date: 2020-07-26 23:20:53
updated: 2020-07-28
mathjax: true
---

# Exploration of a Sound Localization Solution for the Beacon Group in the 15th National University Intelligent Vehicle Competition

### Rules Download

Here is the full content translated into English while retaining the original images and formatting.

------

# Preliminary Exploration of a Sound Localization Solution for the Beacon Group in the 15th National College Student Intelligent Vehicle Competition

### Rules Download

[15th National College Student Intelligent Vehicle Competition Rules for Speed Racing](https://smartcar.cdstm.cn:8083/ueditor/jsp/upload/file/1583802788498046326.pdf){% btn 'https://smartcar.cdstm.cn:8083/ueditor/jsp/upload/file/1583802788498046326.pdf',比赛规则（全）,far fa-hand-point-right,block %}

## Excerpts from Beacon Group Rules

### Track

![赛道引导方式](http://img.pandior.ink/image-20200726234102135.png?imageMogr2/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzQyNkZFQQ==/dissolve/58/gravity/SouthEast/dx/20/dy/20|imageslim)

Analysis: Compared to other groups without specific track requirements, the "freedom" here emphasizes the importance of **obstacle avoidance**, as the vehicle might tilt or encounter other unexpected situations. The guidance methods include **RF signals** and **sound signals**, which will be analyzed below.

<img src="http://img.pandior.ink/image-20200727171321369.png?imageMogr2/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzQyNkZFQQ==/dissolve/58/gravity/SouthEast/dx/20/dy/20|imageslim" alt="信标形状" style="zoom: 25%;" />

### Competition Tasks

![](http://img.pandior.ink/image-20200726234658264.png)

![任务细则](http://img.pandior.ink/image-20200726234725143.png?imageMogr2/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzQyNkZFQQ==/dissolve/58/gravity/SouthEast/dx/20/dy/20|imageslim)

Analysis:

1. Vehicle dimensions are restricted to within 30cm on each side.
2. Main control MCU is restricted to the `Infineon TC26X` series microcontroller:
   - Infineon's chip is a **dual-core MCU** (a first for us).
   - The main frequency is **200MHz**, which is relatively low.
3. Competition format includes two stages: a preliminary qualification round and a head-to-head race.
   - Due to the pandemic this year, the head-to-head race was canceled, and only the light-extinguishing speed was considered.
4. Vehicle model: H model.
   - The H model uses Mecanum wheels, enabling omnidirectional movement.
   - Naturally, we chose the expensive diamond version of the H model, but due to special circumstances, we hadn’t received it by the end of July.

![H车模](http://img.pandior.ink/image-20200727000930827.png?imageMogr2/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzQyNkZFQQ==/dissolve/58/gravity/SouthEast/dx/20/dy/20|imageslim)

5. RF signals are frequency-modulated Chirp signals ranging from 50Hz to 2000Hz, as shown below:

![RF信号](http://img.pandior.ink/image-20200727161724761.png?imageMogr2/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzQyNkZFQQ==/dissolve/58/gravity/SouthEast/dx/20/dy/20|imageslim)

## Solution Analysis

*Existing solutions in the competition include, but are not limited to, the following.&*

**<font color="#dd0000">Special thanks to all the teachers for their creative ideas that inspired our solutions~:cherry_blossom:</font>**

According to the principle of sound distance measurement, the distance `D` is given by:
$$
D=(t_{receive}-t_{send})*V_{sound} 
$$
Assuming the sound undergoes only amplitude attenuation, time delay, and Gaussian white noise during transmission:
$$
f_{r}(t)=A\cdot f_{s}(t-t_{0})+n_{0}(t)
$$
By performing a cross-correlation operation between the received signal and the original transmitted signal:
$$
R_{r,s}(t)=\int_{-\infty }^{+\infty }f_{s}(\tau )\cdot  f_{r}(\tau -t)d\tau
$$
The peak of the correlation result corresponds to the actual signal delay.



### 方案一：FM信号与MIC信号进行互相关运算

#### 方案概述

*这个方案为我们目前正在使用的方案。*

利用`RDA5807`接收的**FM信号**和麦克风阵列接收到的**音频信号**进行**互相关**运算。

![RDA5807](http://img.pandior.ink/image-20200727164409598.png?imageMogr2/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzQyNkZFQQ==/dissolve/58/gravity/SouthEast/dx/20/dy/20|imageslim)

#### 优劣分析

+ 优点

  + FM信号以电磁波形式在空间传播，传播速度为**光速**，可作为参考信号
  + 声音传播速度约为340m/s，通过互相关运算求出峰值对应的下标结合采样率f<sub>采样</sub>，可求出定位精度为V<sub>声音</sub>/f<sub>采样</sub>
  + 具有一定的**容错率**，即使在麦克风旁边放歌也可以精准定位

+ 缺点

  + 对声音传播要求比较高，无回声，无较大干扰噪声
  + 单片机内部RAM资源有限，最大仅支持2048个点运算，限制了通过提高采样率达到提高精度的方式
  + 喇叭麦克风组成的系统并非**纯延迟系统**，该系统对于不同的频率有着不同的**幅频特性**和**相频特性**

+ 优化方案

  + 通过FFT算法，将互相关运算先转为**频域共轭相乘**再通过IFFT求解互相关，FFT（快速傅里叶变化）将DFT（离散傅里叶变换）时间复杂度从*O(N<sup>2</sup>)*降至***O(NlogN)***，由于舍弃误差，FFT还会比DFT精确很多。

  + 采取**楼氏硅麦**取代目前智能车各大店铺售卖的基于`MAX9814`咪头接收器，硅麦相对于驻极体麦克风（咪头），具有体积小，产品一致性好，稳定等特点，主要用于高端设备。（实验结果确实如此，硅麦测距数值比咪头稳定很多）

    <img src="http://img.pandior.ink/image-20200727115050206.png?imageMogr2/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzQyNkZFQQ==/dissolve/58/gravity/SouthEast/dx/20/dy/20|imageslim" alt="驻极体麦克风" style="zoom:50%;" />

    

  <img src="http://img.pandior.ink/image-20200727115145961.png?imageMogr2/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzQyNkZFQQ==/dissolve/58/gravity/SouthEast/dx/20/dy/20|imageslim" alt="硅麦" style="zoom: 67%;" />

  + 为了获得更陡峭极值的互相关函数可以使用广义互相关*（generalized cross-correlation）*，**在频域使用一个加权函数白化输入信号**（目前使用的一般互相关算法数值比较稳定，虽然有些许噪声，但是信噪比还在可接受范围，最多跳跃一个值，后续根据情况决定是否引入加权函数）
  + 使用`TC264DA`芯片，相比于`TC264D`，DA多了硬件FFT以及512KB的EMEM存储空间
    + 此硬件FFT最大支持1024个点，~~基本没用~~
    + CPU访问512KB的EMEM内存空间花费的时间是访问自己内存空间的3倍
  + 增加采样周期，也就是提高扫频的时间长度，在一定程度上可以抑制环境噪声的影响，但比赛的竞技性质决定我们最多采集两个周期的信号（实际情况证明两个周期的互相关结果明显优于采集一个周期运算结果）

#### MATLAB仿真结果

~~原始信号并没有使用变频信号，因为懒，反正差不多~~~

![仿真结果](http://img.pandior.ink/image-20200801115559780.png?imageMogr2/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzQyNkZFQQ==/dissolve/58/gravity/SouthEast/dx/20/dy/20|imageslim)

#### 方案结果

![整体结构](http://img.pandior.ink/image-20200728213957515.png?imageMogr2/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzQyNkZFQQ==/dissolve/58/gravity/SouthEast/dx/20/dy/20|imageslim)

![测距结果](http://img.pandior.ink/image-20200728213913512.png?imageMogr2/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzQyNkZFQQ==/dissolve/58/gravity/SouthEast/dx/20/dy/20|imageslim)

###  方案二：将FM信号与MIC信号转换成方波进行输入捕获

#### 方案概述

`RDA5807`、硅麦都是将FM信号转换成变化的电压信号，然后通过ADC读取对应的电压大小。此时我们可以通过一个滞回比较器将正弦波信号转换成方波信号，通过输入捕获，仅采集FM任意一小节波形对应的频率，然后在声音的“方波“中寻找与之对应的频率波形从而算出相位差。

<img src="http://img.pandior.ink/QQ图片20200728210226.png?imageMogr2/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzQyNkZFQQ==/dissolve/58/gravity/SouthEast/dx/20/dy/20|imageslim" alt="手机控制器" style="zoom:25%;" />

<img src="http://img.pandior.ink/测试电路.jpg?imageMogr2/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzQyNkZFQQ==/dissolve/58/gravity/SouthEast/dx/20/dy/20|imageslim" alt="测试电路" style="zoom:67%;" />

<img src="http://img.pandior.ink/示波器图片.jpg?imageMogr2/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzQyNkZFQQ==/dissolve/58/gravity/SouthEast/dx/20/dy/20|imageslim" alt="示波器原始波形" style="zoom: 67%;" />

<img src="http://img.pandior.ink/image-20200728210741188.png?imageMogr2/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzQyNkZFQQ==/dissolve/58/gravity/SouthEast/dx/20/dy/20|imageslim" alt="通过滞回比较器的波形图" style="zoom: 80%;" />

可以看见波形并不是非常的理想，$t_{pd}$（Propagation delay time）过大，但是比较器采用的是TI的`TL3201`，根据芯片手册理论值应为50ns左右，后续有时间研究一下这个问题。

![datasheet部分](http://img.pandior.ink/image-20200728211221158.png?imageMogr2/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzQyNkZFQQ==/dissolve/58/gravity/SouthEast/dx/20/dy/20|imageslim)

#### 优劣分析

+ 优点

  + 这个方法求解时间差的速度非常的快，理论上最大时间$\triangle  t$为

    
    $$
    \triangle  t=\frac{L_{max}}{V_{voice}}
    $$

+ 缺点

  + 容错率过低，一旦**对应FM频率的麦克风波形**没捕捉到结果会相差很大（这点可以通过剪枝解决，如一旦发现麦克风频率低于捕获FM的频率就重新捕获FM信号）
  + 变频信号有部分信号对应的幅度过小导致无法上拉比较器

  + 并非理想比较器，总之就是**理想很丰满，现实很骨感**

  <img src="http://img.pandior.ink/image-20200728213550222.png?imageMogr2/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzQyNkZFQQ==/dissolve/58/gravity/SouthEast/dx/20/dy/20|imageslim" alt="变频信号对应的方波波形" style="zoom:67%;" />

  + 将死区空间设小以后非常容易受噪声干扰

### 方案三：采用纯麦克风阵列定位

#### 方案概述

属于弱化版方案一，主要利用GCC-PHAT算法

<img src="http://img.pandior.ink/image-20200728215616767.png?imageMogr2/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzQyNkZFQQ==/dissolve/58/gravity/SouthEast/dx/20/dy/20|imageslim" alt="求解角度" style="zoom:50%;" />

<img src="http://img.pandior.ink/image-20200728215658434.png?imageMogr2/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzQyNkZFQQ==/dissolve/58/gravity/SouthEast/dx/20/dy/20|imageslim" alt="角度大致匹配" style="zoom:50%;" />



### 方案四：利用鉴相器AD8302输出相位信息

*这个方案是在群里潜水看他们聊天看到的，回头验证一下看看有没有可行性*

