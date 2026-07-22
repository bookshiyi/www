---
title: 基于Matlab的心电信号去噪系统设计
tags:
  - DSP
  - Matlab
  - 基线漂移
  - 小波去噪
  - 心电信号
  - 数字信号处理
comments: false
categories:
  - 数字信号处理
  - 算法
date: 2016-01-25 15:16:47
---

        实测的心电信号中常常存在一些强干扰和噪声，如何在强背景干扰和噪声下准确提取出有用的心电信号，是心脏类疾病预测和诊断的一个重要内容。本文提出了一种心电信号的去噪系统设计方法，对原始心电信号进行频谱分析后，确定噪声主要存在的频带：原始信号中主要包含了极强的50Hz工频干扰、低频肌电干扰带来的基线漂移、白噪声。设计低通滤波器和陷波器，对原始信号进行预处理，旨在滤除信号中的高频噪声和工频干扰；设计算法，对信号中的中低频白噪声进行抑制；设计基线补偿算法，消除信号中低频的基线漂移现象；仿真结果表明，20组差异明显的实测的带噪心电信号经本系统处理后，得到的信号波形均十分清晰，且信号的特征值保留完整，为临床医生的判断提供了有利的依据。

### 0       引言

        目前，全球心脏类疾病的发病率和死亡率一直居高不下,一直是当代人类健康的首要威胁之一，所以心电信号在医学领域就变得有非常重要的意义，但是由于心电信号本身十分较弱（10pV~5mV）,难以检测，再加之人体自身的肌电干扰、室内的工频干扰以及周围其他的电磁干扰，导致在传感器输出端心电信号几乎淹没在噪声里面，所以对心电信号分析和去噪具有很高的实用价值和重要意义。

        本文设计了一套心电心号的处理系统，包括：线性相位FIR低通滤波器和陷波器，抑制工频干扰及其他噪声,对原始心电信号进行预处理；小波去噪，对原始信号进行小波分解后，进行阈值处理，再做小波重构处理，以此去除信号中的白噪声；基线矫正：通过计算信号变化趋势的方法来消除信号中的线性趋势。最终可以把绝大多数的原始心电信号较为完整的提取出来且几乎不损失信号的特征值。

### 1       心电信号频谱分析

        通过对心电信号的频谱分析，找出其噪声和干扰的主要分布频带范围，以此来设计相应的滤波器。

#### 1.1         心电心号的读取

        目前，在国际上的公认可用作标准心电数据库有三个，分别是美国麻省理工学院的MIT-BIH 数据库，[美国心脏学会](http://baike.baidu.com/subview/10276144/10439505.htm)的AHA数据库和欧洲AT-T心电数据库。近年来，美国麻省理工学院的MIT-BIH 数据库广泛应用于医疗行业。

        从MIT-BIH数据库下载20组心电信号数据，通过MATLAB中的xlsread函数将表格形式的原始数据导入到工作空间。

#### 1.2         心电心号频谱分析

![图片1](https://assets.bookshiyi.com/photo/2016/02/图片1-1.png)

图1 原始心电信号的时域波形和频谱图

Fig. 1 The original ecg signal in the time domain waveform and spectrum diagram

        通过对原始信号的时域波形观察可以发现：信号中的高频噪声较多，信号大多被淹没在噪声中，并且伴有基线漂移的现象，频谱图中可以发现信号在50Hz的频率处出现了极强烈噪声，据分析为工频干扰。

### 2       去噪系统设计

        根据对实测的原始心电信号进行频谱分析后，提出了以下设计方案：FIR低通滤波器，滤除信号中100HZ以上的高频噪声；FIR工频陷波器，抑制信号中的50HZ工频干扰；小波去噪：滤除信号中的白噪声；基线矫正：矫正由肌电干扰等带来的基线漂移现象。系统结构框图如图2所示：

![图片2](https://assets.bookshiyi.com/photo/2016/02/图片2-1.png)

图2 系统结构框图

Fig. 2   system block diagram

#### 2.1         FIR滤波器

        FIR滤波器，全称Finite Impulse Response，有限长单位冲激响应滤波器，又称为非递归型滤波器，是数字信号处理系统中最基本的元件，它能够在保证任意幅频特性的情况下具有严格的线性相频特性，同时其单位抽样响应是有限长的，因而滤波器是稳定的系统。因此，FIR滤波器在通信、图像处理、模式识别等领域都有着广泛的应用。

##### 2.1.1        窗函数法设计思路

        窗函数设计滤波器【文献1】的基本思想是，首先根据要求选择一个适当的低通滤波器，因为其脉冲响应是非因果且是无限长的，用最优化窗结构窗函数来截取它的脉冲响应，从而得到线性相位和因果的FIR滤波器。

        a)根据给定要求的理想频率响应 ![图片3](https://assets.bookshiyi.com/photo/2016/02/图片3-1.png)求出![图片4](https://assets.bookshiyi.com/photo/2016/02/图片4-1.png)

![图片5](https://assets.bookshiyi.com/photo/2016/02/图片5-1.png)

        b)用一个有限时长的“窗函数”序列 将 截断，窗的点数是N点。阶段后的序列为![图片10](https://assets.bookshiyi.com/photo/2016/02/图片10.png)

![图片6](https://assets.bookshiyi.com/photo/2016/02/图片6-1.png)

窗的点数N及窗的形状是两个极重要的参数。

        d)求出加窗后实际的频率响应![图片8](https://assets.bookshiyi.com/photo/2016/02/图片8-1.png)

![图片7](https://assets.bookshiyi.com/photo/2016/02/图片7-1.png)

并反复检验![图片8](https://assets.bookshiyi.com/photo/2016/02/图片8-1.png) 是否满足![图片9](https://assets.bookshiyi.com/photo/2016/02/图片9-1.png) ，不满足则改正窗形状或窗长的点数N。

表1 常见窗函数基本参数的比较【来自文献1】

Tab. 1 The comparison of common basic parameters window function

![b1](https://assets.bookshiyi.com/photo/2016/02/b1.png)

      常见窗函数的参数如表1所示，本文设计中使用了凯泽窗来设计FIR滤波器，凯泽窗是接近最优化窗结构的窗函数，它可以根据不同的参数调整滤波器滤波器的各项指标，而矩形窗、汉宁窗、海明窗和布莱克曼窗等窗的形状是固定的，一旦选取了某种窗函数，设计出的FIR滤波器在阻带的衰减就确定了。凯泽窗是一种应用广泛的可调窗，它可以通过改变窗函数的形状来控制窗函数旁瓣的大小，从而可以在设计中用滤波器的衰减指标来确定窗函数的形状。

##### 2.1.2        FIR低通滤波器设计

        理想线性相位低通滤波器的频率响应：

![图片11](https://assets.bookshiyi.com/photo/2016/02/图片11.png)

        单位抽样响应：

![图片12](https://assets.bookshiyi.com/photo/2016/02/图片12.png)

        利用matlab中的FDATool【文献2】工具，设置了滤波器的阶数N=20，通带截止频率95HZ，阻带截止频率100Hz，Beat=0.5，通过凯瑟窗方法得到的滤波器特性如图3所示：![图片13](https://assets.bookshiyi.com/photo/2016/02/图片13.png)

图3 低通FIR滤波器幅频特性曲线

Fig. 3 Low pass FIR filter amplitude-frequency characteristic curve

##### 2.1.3        FIR工频陷波器设计

        理想线性相位带阻滤波器的频率响应：

![图片14](https://assets.bookshiyi.com/photo/2016/02/图片14.png)

        单位抽样响应：

![图片15](https://assets.bookshiyi.com/photo/2016/02/图片15.png)

        由于市电电压的频率为50Hz，它会以电磁波的辐射形式，对人们的日常生活造成干扰，我们把这种干扰称之为工频干扰，故设计一种陷波器，滤除心电信号中的50Hz干扰，

        利用matlab中的FDATool工具，设置了滤波器的阶数N=60，Fc1=47Hz，Fc2=53Hz，Beta=0.3通过凯瑟窗方法得到的滤波器特性如图4所示：![图片16](https://assets.bookshiyi.com/photo/2016/02/图片16.png)

图4 50Hz的FIR陷波器幅频特性曲线

Fig. 4 50 Hz FIR trap amplitude-frequency characteristic curve

#### 2.2         小波去噪

        由于实测心电信号的信噪比较低，其特征波与部分干扰信号的频带相互重叠，普通的频带滤波方法不能有效的将两者完全分离。小波变换在传统的傅立叶变换基础上发展而来，具有多尺度多分辨率的优异特性和良好的时频局部化特性，所以小波去噪更适合处理心电信号与干扰信号频带重叠的滤波问题。

##### 2.2.1              离散小波变换及重构

        信号 ![图片17](https://assets.bookshiyi.com/photo/2016/02/图片17.png)的连续小波变换为：![图片18](https://assets.bookshiyi.com/photo/2016/02/图片18.png)

        对尺度因子a和平移参数b进行如下的离散采样：![图片19](https://assets.bookshiyi.com/photo/2016/02/图片19.png)

        则小波 ![图片20](https://assets.bookshiyi.com/photo/2016/02/图片20.png)变为：

![图片21](https://assets.bookshiyi.com/photo/2016/02/图片21.png)

        离散小波变换定义为：

![图片22](https://assets.bookshiyi.com/photo/2016/02/图片22.png)

        由离散小波变换 ![图片23](https://assets.bookshiyi.com/photo/2016/02/图片23.png)重构出原始信号 ：

![图片24](https://assets.bookshiyi.com/photo/2016/02/图片24.png)

        上式中 ![图片26](https://assets.bookshiyi.com/photo/2016/02/图片26.png)为![图片26](https://assets.bookshiyi.com/photo/2016/02/图片26.png) 的对偶框架。

#### 2.2.2              小波去噪算法设计

        首先对原始信号进行小波分解，经过累试发现dB6作为小波基对于分解带噪心电信号的效果较好，分解层数为5的时候，去噪效果较好，在保证了去噪效果的情况下节约了运算时间，各子带的频率范围如表2所示：

表2 5尺度分解子带系数的频率范围

Tab. 2 The frequency range of scale subband coefficients

![b2](https://assets.bookshiyi.com/photo/2016/02/b2.png)

        在阈值处理及重构阶段采用如下参数：使用minimax原则【文献4】（极值阈值估计）产生阈值， minimax方法比较保守，对噪声在信号的高频段分布较少时去噪效果较好，可以将微弱的信号提取出来；并进行硬阈值处理，使得波形变得硬朗而非平滑；阈值处理根据每层小波噪声水平进行调整，这样的方法可以适应多变且复杂的心电信号，使得滤波系统具有一定的普遍性。运用MATLAB中的小波工具箱，图形化操作的方式小波分解心电信号，如图4所示为心电信号在5尺度小波分解下的波形：

![图片27](https://assets.bookshiyi.com/photo/2016/02/图片27.png)

图5 5尺度下dB6小波分解信号的波形

Fig. 5 5 scales dB6 wavelet decomposition signal waveform

#### 2.3         基线矫正

        基线漂移是因呼吸、肢体活动等引起的ECG信号上下浮动的现象，常规的心电图仪长采用无源RC滤波的方式来抑制基线漂移，即病人保持不动，待基线稳定以后再进行测量，显然，这样的做法对于病人进行长期的监护是不合适的【文献6】。

##### 2.3.1              基线矫正的原理

        基线漂移的频率极低，普通的高通滤波器很难到达预期的滤波效果，所以提出了一种根据小波变换对信号进行长周期趋势估计【文献3】，再进行基线漂移的补偿。

##### 2.3.2              基线矫正算法的设计

        用dB6小波基8尺度分解信号，其近似信号的频带分布如表3所示：

表3 8尺度分解子带系数的频率范围

Tab.3 The frequency range of scale subband coefficients

![b3](https://assets.bookshiyi.com/photo/2016/02/b3.png)

        尺度为8的近似信号部分频带为0~0.9765625Hz，此频段多为信号的基线漂移趋势。所以在小波分解后将a8信号（主要基线漂移信号）直接去除即可。dB6小波在8尺度下分解信号的近似部分波形如图6所示：

![图片28](https://assets.bookshiyi.com/photo/2016/02/图片28.png)

图6 dB6小波在8尺度下分解信号的近似部分波形

Fig. 6 DB6 approximation of wavelet decomposition in 8 signal waveform

### 3       Matlab仿真

        如图7所示为心电信号去噪系统在Matlab中对信号滤波前后的仿真对比图：可以发现100Hz以上以及工频50Hz的噪声被完全滤除；白噪声被消除，波形变得十分清晰；基线漂移现象被较好的抑制。

![图片29](https://assets.bookshiyi.com/photo/2016/02/图片29.png)

图7 信号去噪前后的时域波形及频谱图

Fig. 7 Signal denoising before and after the time domain waveform and spectrum diagram

### 4       结论

        本文给出了基于MATLAB的心电信号去噪系统的设计方法：从带噪心电信号的读取及频谱分析，窗函数法设计FIR滤波器对心电信号进行预处理；运用小波去噪算法滤除信号中残存的白噪声；基线矫正算法用来抑制信号中由于呼吸、人身运动等带来的基线漂移现象。经验证该系统对大部分低信噪比的心电信号去噪效果十分显著。

![QQ拼音截图未命名](https://assets.bookshiyi.com/photo/2016/02/QQ拼音截图未命名.png)

Matlab源代码和原始心电信号数据(20组)

下载链接：[源码&数据_基于Matlab的心电信号去噪系统设计.rar](https://assets.bookshiyi.com/photo/2016/02/源码数据_基于Matlab的心电信号去噪系统设计.rar)