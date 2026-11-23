# ControlTheoryNote

控制相关学习笔记，使用 LaTeX 编写，侧重公式推导。

## 笔记目录

| 主题 | 笔记 | 内容 |
| --- | --- | --- |
| 模型预测控制 (MPC) | [MPC_01](MPC/MPC_01.pdf) ([源码](MPC/MPC_01.tex)) | 最优控制与代价函数、MPC 滚动时域优化思路、将 MPC 代价函数推导为二次型形式 |
| 卡尔曼滤波 (KF) | [KF_01](KalmanFilter/KF_01.pdf) ([源码](KalmanFilter/KF_01.tex)) | 问题描述、数据融合、卡尔曼增益推导、先验估计协方差推导、卡尔曼滤波五步流程 |

## 内容概要

### MPC_01：代价函数推导

- 最优控制：用带权重的二次型代价函数 $J = \int E^TQE + U^TRU \, ds$ 描述多目标约束问题
- MPC 算法：对离散线性系统 $X_{k+1} = AX_k + BU_k$，每个时刻求解有限时域内的最优输入，只执行第一步，然后滚动
- 公式变形：把状态和输入序列堆叠成 $\hat{X}_k$、$\hat{U}_k$，将累加形式的代价函数化为二次型 $J = \hat{X}_k^T G \hat{X}_k + \hat{U}_k^T H \hat{U}_k + 2\hat{X}_k^T E \hat{U}_k$

### KF_01：卡尔曼滤波推导

- 对含过程噪声 $w$ 和测量噪声 $v$ 的线性系统，融合先验估计与测量值得到后验估计
- 以估计误差协方差矩阵的迹 $tr(P_k)$ 最小为目标，求导推出卡尔曼增益 $K_k$
- 推导先验估计误差协方差 $P_{\bar{k}} = AP_{k-1}A^T + Q$
- 汇总为五步流程：先验估计 → 先验误差协方差 → 卡尔曼增益 → 后验估计 → 更新误差协方差

## 编译

笔记使用 `ctexart` 文档类，需要安装带中文支持的 TeX 发行版（如 TeX Live）。在笔记所在目录下执行：

```bash
cd MPC
xelatex MPC_01.tex
xelatex MPC_01.tex   # 第二遍用于生成交叉引用和书签
```

## 参考资料

- [DR_CAN 的控制理论系列视频（Bilibili）](https://www.bilibili.com/video/BV1SQ4y1Y7FG)
- [贝叶斯滤波：为什么是两个高斯分布相乘](https://blog.csdn.net/varyshare/article/details/97642209)
- [高斯分布相乘仍是高斯分布](https://blog.csdn.net/michaelhan3/article/details/85453368)
- [最小化方差与极大似然估计的联系](https://zhuanlan.zhihu.com/p/105496881)
