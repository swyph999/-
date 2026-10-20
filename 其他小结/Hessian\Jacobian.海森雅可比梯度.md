### 海森矩阵百度百科定义，性质和使用。https://baike.baidu.com/item/%E9%BB%91%E5%A1%9E%E7%9F%A9%E9%98%B5/2248782
### 海森矩阵（Hessian矩阵）及其应用。https://blog.csdn.net/liangyihuai/article/details/159431944
### 雅可比矩阵（Jacobian Matrix）。https://zhuanlan.zhihu.com/p/1969812752055902350
梯度：标量函数的一阶导数，描述函数往哪个方向增长最快。  
雅可比矩阵：向量函数的一阶导数，把每个分量函数的梯度转置后按行排列。  
海森矩阵：标量函数的二阶导数，就是梯度的雅可比矩阵，描述梯度如何变化，也就是曲率。  
## 三、梯度、雅可比矩阵、海森矩阵的关系

| 概念 | 定义 | 作用 |
| --- | --- | --- |
| 梯度（Gradient） | $\nabla f = \left[\frac{\partial f}{\partial x_1}, \ldots, \frac{\partial f}{\partial x_n}\right]^T$ | 标量函数的一阶导数向量 |
| 雅可比矩阵（Jacobian） | $J = \frac{\partial \mathbf f}{\partial \mathbf x},\quad J_{ij} = \frac{\partial f_i}{\partial x_j}$ | 向量函数的一阶导数矩阵 |
| 海森矩阵（Hessian） | $H = \nabla^2 f,\quad H_{ij} = \frac{\partial^2 f}{\partial x_i \partial x_j}$ | 标量函数的二阶导数矩阵 |

例如：

- 若 $f(\mathbf x)$ 是标量函数，其梯度是列向量，雅可比是行向量，两者满足 $J_f = (\nabla f)^T$。
- 若 $\mathbf f(\mathbf x)$ 是向量函数，其雅可比矩阵的第 $i$ 行就是分量函数 $f_i$ 的梯度转置。
- 海森矩阵就是梯度的雅可比矩阵，描述梯度如何随参数变化，即函数的局部曲率。
