## 3.1 EKF下的问题描述与协方差推导

在KF滤波器中所用的运动方程和测量方程都是线性函数，但是在一些非线性情况下，如转弯、控制信号周期变换等，上述的KF滤波器中的线性函数就变成了非线性存在，直接套用KF就会出现较大偏差。也就是上面提到的运动方程和观测方程变为了如下非线性函数组合的形式，对于运动方程：

$$
x_t=f(x_{t-1},u_t)+\omega_t
$$

EKF算法的思想便是对于非线性函数在某一点上进行泰勒展开，这样使用n阶多项式的形式逼近原来的函数，对于上述函数非线性函数 $f(x_{t-1},u_t)$ 在上一次卡尔曼滤波结果估计结果 $\bar{x}_{t-1}$ 处展开得到：

$$
\left.f(x,u)\right|_{x=\bar{x}_{t-1},u=u_t}=f(\bar{x}_{t-1},u_t)+\left.\frac{\partial f}{\partial x}\right|_{x=\bar{x}_{t-1},u=u_t}(x-\bar{x}_{t-1})+\left.\frac{\partial f}{\partial u}\right|_{x=\bar{x}_{t-1},u=u_t}(u-u_t)+O(x-\bar{x}_{t-1})+O(u-u_t)\qquad\text{(23)}
$$

$$
\approx f(\bar{x}_{t-1},u_t)+\left.\frac{\partial f}{\partial x}\right|_{x=\bar{x}_{t-1},u=u_t}(x-\bar{x}_{t-1})\qquad\text{(24)}
$$

$$
\approx f(\bar{x}_{t-1},u_t)+F_t(x-\bar{x}_{t-1})\qquad\text{(25)}
$$

其中，$`F_t=\left.\frac{\partial f}{\partial x}\right|_{x=\bar{x}_{t-1},u=u_t}`$。则近似得到在上一次卡尔曼估计结果 $\bar{x}_{t-1}$ 处的泰勒一阶逼近的运动方程：

$$
x_t\approx f(\bar{x}_{t-1},u_t)+F_t(x-\bar{x}_{t-1})+\omega_t
$$

由之前的真值与预测值的协方差定义得到（其中 $`\hat{x}_t=f(\bar{x}_{t-1},u_t)`$）：

$$
\hat{P}_t=E((x_t-\hat{x}_t)(x_t-\hat{x}_t)^T)\qquad\text{(26)}
$$

$$
=E((F_t(x-\bar{x}_{t-1})+\omega_t)(F_t(x-\bar{x}_{t-1})+\omega_t)^T)\qquad\text{(27)}
$$

$$
=F_t\bar{P}_{t-1}F_t^T+Q_t\qquad\text{(28)}
$$

对应的非线性观测方程变为：

$$
\dot{x}_t=g(x_t)+v_t
$$

同样需要对 $g(x_t)$ 进行泰勒展开，展开的位置是 $\hat{x}_t$ 处（当前时刻预测结果）：

$$
\left.g(x)\right|_{x=\hat{x}_t}=g(\hat{x}_t)+\left.\frac{\partial g}{\partial x}\right|_{x=\hat{x}_t}(x-\hat{x}_t)+O(x-\hat{x}_t)\qquad\text{(29)}
$$

$$
\approx g(\hat{x}_t)+\left.\frac{\partial g}{\partial x}\right|_{x=\hat{x}_t}(x-\hat{x}_t)\qquad\text{(30)}
$$

$$
\approx g(\hat{x}_t)+G_t(x-\hat{x}_t)\qquad\text{(31)}
$$

其中，$`G_t=\left.\frac{\partial g}{\partial x}\right|_{x=\hat{x}_t}`$。则观测方程在当前时刻预测结果 $\hat{x}_t$ 处的泰勒一阶近似化结果为：

$$
\dot{x}_t\approx g(\hat{x}_t)+G_t(x-\hat{x}_t)+v_t
$$

同样按照上一节中对于测量误差计算协方差：

$$
\dot{P}_t=G_t\hat{P}_tG_t^T+R_t
$$




### Step1：预测阶段

得到运动预测状态：$`\hat{x}_t=f(\bar{x}_{t-1},u_t)`$

得到当前运动状态协方差：$`\hat{P}_t=F_t\bar{P}_{t-1}F_t^T+Q_t`$

---

### Step2：更新阶段

计算卡尔曼增益：$`K_t=\hat{P}_tG_t^T(G_t\hat{P}_tG_t^T+R_t)^{-1}`$

得到卡尔曼最终估计结果：$`\bar{x}_t=\hat{x}_t+K_t(\dot{x}_t-g(\hat{x}_t))`$

更新卡尔曼最终估计结果协方差：$`\bar{P}_t=\hat{P}_t-K_tG_t\hat{P}_t`$

---

### Step3：结果返回

结果返回：$`\bar{x}_t,\bar{P}_t`$
