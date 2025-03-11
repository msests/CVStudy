
## 1. 什么是DCT？

离散余弦变换（Discrete Cosine Transform）是一种将**时域信号**转换为**频域**的数学工具。常用于：
- 图像/音频压缩（如JPEG、MP3）
- 信号处理
- 数据特征提取

[离散余弦变换可视化讲解_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1bc411q7YG/)

## 2. 一维DCT基础公式

对于长度为$N$的序列$\{x_0,x_1,...,x_{N-1}\}$，其DCT变换为：

$$
X_k = \alpha(k) \sum_{n=0}^{N-1} x_n \cos\left( \frac{\pi}{N} \left(n+\frac{1}{2}\right)k \right)
$$

其中：
- $k = 0,1,...,N-1$（频率分量索引）
- $\alpha(k) = \begin{cases}  \sqrt{\frac{1}{N}}, & k=0 \\ \sqrt{\frac{2}{N}}, & k \neq 0  \end{cases}$

> 前面的$\alpha(k)$用于归一化，将$[n,\cos\left( \frac{\pi}{N} \left(n+\frac{1}{2}\right)k \right)]$转换为$\mathbb{R}^N$中的单位向量。

## 3. 三步理解DCT

### 步骤1：准备余弦基函数

构建一组不同频率的余弦波形：
$$
\cos\left( \frac{\pi}{N} \left(n+\frac{1}{2}\right)k \right)
$$
- $n$：时域位置（0到N-1）
- $k$：控制频率的系数

### 步骤2：信号投影

将原始信号$x_n$与每个基函数做**点乘**，得到对应频率成分$X_k$

### 步骤3：归一化处理

通过$\alpha(k)$系数：
- 保证能量守恒
- 使变换可逆

## 4. 举个栗子🌰

假设信号$[2, 3, 4, 1]$，计算$X_0$：

$$
X_0 = \sqrt{\frac{1}{4}} \left(2\cdot1 + 3\cdot1 + 4\cdot1 + 1\cdot1\right) = \frac{1}{2}(10) = 5
$$

## 5. 二维DCT（图像处理）

对$N \times N$图像，先对每行做一维DCT，再对每列做一维DCT：

$$
X_{u,v} = \alpha(u)\alpha(v) \sum_{i=0}^{N-1}\sum_{j=0}^{N-1} x_{i,j} \cos\left[\frac{\pi}{N}(i+\frac{1}{2})u\right] \cos\left[\frac{\pi}{N}(j+\frac{1}{2})v\right]
$$

## 6. DCT的三大特点

1. **能量集中**：大部分信息集中在低频分量

2. **实数运算**：输入输出均为实数

3. **可逆性**：通过IDCT可完美重建原始信号

## 7. 实际应用

- JPEG压缩：将图像分块8×8做DCT

- 视频编码：去除空间冗余

- 语音识别：提取MFCC特征

`注：实际计算推荐使用FFT加速，手工计算仅适合理解原理`