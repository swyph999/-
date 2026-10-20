### 海森矩阵百度百科定义，性质和使用。https://baike.baidu.com/item/%E9%BB%91%E5%A1%9E%E7%9F%A9%E9%98%B5/2248782
### 海森矩阵（Hessian矩阵）及其应用。https://blog.csdn.net/liangyihuai/article/details/159431944
### 雅可比矩阵（Jacobian Matrix）。https://zhuanlan.zhihu.com/p/1969812752055902350



  
## 三、梯度、雅可比矩阵、海森矩阵的关系

| 概念 | 定义 | 作用 |
| --- | --- | --- |
| 梯度（Gradient） | $\nabla f = \left[\frac{\partial f}{\partial x_1}, \ldots, \frac{\partial f}{\partial x_n}\right]^T$ | 标量函数的一阶导数向量 |
| 雅可比矩阵（Jacobian） | $J = \frac{\partial \mathbf f}{\partial \mathbf x},\quad J_{ij} = \frac{\partial f_i}{\partial x_j}$ | 向量函数的一阶导数矩阵 |
| 海森矩阵（Hessian） | $H = \nabla^2 f,\quad H_{ij} = \frac{\partial^2 f}{\partial x_i \partial x_j}$ | 标量函数的二阶导数矩阵 |

例如：

1. **梯度**

   对于标量函数 $f(x_1,x_2,\ldots,x_n)$，梯度 $\nabla f$ 是由各个一阶偏导数组成的列向量。  
   其中，第 $i$ 个分量 $\frac{\partial f}{\partial x_i}$ 表示：**在其他变量保持不变时，函数值对变量 $x_i$ 的局部变化率**。因此，梯度描述了函数值对各个变量微小变化的局部敏感程度。

3. **雅可比矩阵**

   对于向量函数 $\mathbf f(\mathbf x)=[f_1(\mathbf x),f_2(\mathbf x),\ldots,f_m(\mathbf x)]^T$，雅可比矩阵 $J$ 是一个 $m\times n$ 的一阶偏导数矩阵。

   其中，**每一行**是一个分量函数 $f_i$ 的梯度的转置，描述该函数对各个输入变量的局部敏感程度；**每一列**描述同一个输入变量 $x_j$ 的微小变化对各个输出分量的局部影响。

4. **海森矩阵**

   对于标量函数 $f(x_1,x_2,\ldots,x_n)$，海森矩阵 $H=\nabla^2f$ 是一个 $n\times n$ 的二阶偏导数矩阵，也就是**梯度的雅可比矩阵**。
   
   它描述梯度如何随各个变量变化，反映函数的局部曲率。**对角元素**描述函数对某个变量的变化率，如何随该变量自身变化；**非对角元素**描述函数对某个变量的变化率，如何随另一个变量变化。
