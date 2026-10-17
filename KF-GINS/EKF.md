## 3.1 EKF下的问题描述与协方差推导

在KF滤波器中所用的运动方程和测量方程都是线性函数，但是在一些非线性情况下，如转弯、控制信号周期变换等，上述的KF滤波器中的线性函数就变成了非线性存在，直接套用KF就会出现较大偏差。也就是上面提到的运动方程和观测方程变为了如下非线性函数组合的形式，对于运动方程：

$$
x_t = f(x_{t-1},u_t) + \omega_t
$$

EKF算法的思想便是对于非线性函数在某一点上进行泰勒展开，这样使用n阶多项式的形式逼近原来的函数，对于上述非线性函数 $f(x_{t-1},u_t)$ 在上一次卡尔曼滤波结果估计结果 $\bar{x}_{t-1}$ 处展开得到：

$$
\begin{aligned}
\left.f(x,u)\right|_{x=\bar{x}_{t-1},\,u=u_t}
&= f(\bar{x}_{t-1},u_t) \\
&\quad + \left.\frac{\partial f}{\partial x}\right|_{\substack{x=\bar{x}_{t-1}\\u=u_t}}(x-\bar{x}_{t-1}) \\
&\quad + \left.\frac{\partial f}{\partial u}\right|_{\substack{x=\bar{x}_{t-1}\\u=u_t}}(u-u_t) \\
&\quad + \mathcal{O}(\cdots)
\end{aligned}
$$

**(23)**

$$
\begin{aligned}
&\approx f(\bar{x}_{t-1},u_t) \\
&\quad + \left.\frac{\partial f}{\partial x}\right|_{\substack{x=\bar{x}_{t-1}\\u=u_t}}(x-\bar{x}_{t-1})
\end{aligned}
$$

**(24)**

$$
\approx f(\bar{x}_{t-1},u_t) + F_t(x-\bar{x}_{t-1})
$$

**(25)**

其中，

$$
F_t=\left.\frac{\partial f}{\partial x}\right|_{\substack{x=\bar{x}_{t-1}\\u=u_t}}
$$

则近似得到在上一次卡尔曼估计结果 $\bar{x}_{t-1}$ 处的泰勒一阶逼近的运动方程：

$$
x_t \approx f(\bar{x}_{t-1},u_t) + F_t(x-\bar{x}_{t-1}) + \omega_t
$$

由之前的真值与预测值的协方差定义得到（其中 $\hat{x}_t = f(\bar{x}_{t-1},u_t)$）：

$$
\hat{P}_t=E\left((x_t-\hat{x}_t)(x_t-\hat{x}_t)^T\right)
$$

**(26)**

$$
\begin{aligned}
&=E\Bigl(\bigl(F_t(x-\bar{x}_{t-1})+\omega_t\bigr) \\
&\qquad\quad\cdot\bigl(F_t(x-\bar{x}_{t-1})+\omega_t\bigr)^T\Bigr)
\end{aligned}
$$

**(27)**

$$
=F_t\bar{P}_{t-1}F_t^T+Q_t
$$

**(28)**

对应的非线性观测方程变为：

$$
\dot{x}_t=g(x_t)+v_t
$$

同样需要对 $g(x_t)$ 进行泰勒展开，展开的位置是 $\hat{x}_t$ 处（当前时刻预测结果）：

$$
\begin{aligned}
\left.g(x)\right|_{x=\hat{x}_t}
&=g(\hat{x}_t) \\
&\quad + \left.\frac{\partial g}{\partial x}\right|_{x=\hat{x}_t}(x-\hat{x}_t) \\
&\quad +\mathcal{O}(x-\hat{x}_t)
\end{aligned}
$$

**(29)**

$$
\begin{aligned}
&\approx g(\hat{x}_t) \\
&\quad+\left.\frac{\partial g}{\partial x}\right|_{x=\hat{x}_t}(x-\hat{x}_t)
\end{aligned}
$$

**(30)**

$$
\approx g(\hat{x}_t)+G_t(x-\hat{x}_t)
$$

**(31)**

其中，

$$
G_t=\left.\frac{\partial g}{\partial x}\right|_{x=\hat{x}_t}
$$

则观测方程在当前时刻预测结果 $\hat{x}_t$ 处的泰勒一阶近似化结果为：

$$
\dot{x}_t\approx g(\hat{x}_t)+G_t(x-\hat{x}_t)+v_t
$$

同样按照上一节中对于测量误差计算协方差：

$$
\dot{P}_t=G_t\hat{P}_tG_t^T+R_t
$$
