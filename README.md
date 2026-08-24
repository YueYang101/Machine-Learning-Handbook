# Machine-Learning-Handbook

个人机器学习笔记站，使用纯静态 HTML，可直接在浏览器打开；公式由 MathJax 渲染，交互图使用原生 canvas，实验图片与视频存放在本地 `assets/`，没有构建步骤。

- **在线阅读：** [yueyang101.github.io/Machine-Learning-Handbook](https://yueyang101.github.io/Machine-Learning-Handbook/)
- **唯一编写规范：** [STYLE.md](STYLE.md)
- **工具入口：** [AGENTS.md](AGENTS.md) 与 [CLAUDE.md](CLAUDE.md) 仅负责指向 `STYLE.md`，不重复维护规则。

## 站点入口

| 页面 | 内容 |
|---|---|
| [index.html](index.html) | GitHub Pages 首页与公开导航；分类层级与本索引保持同步 |

## 理论

### 基础概念

| 页面 | 内容 |
|---|---|
| [foundations.html](foundations.html) | 基础概念清单：被多篇笔记复用的底层工具索引，每条标注「谁在用它」 |
| [kl-divergence.html](kl-divergence.html) | KL 散度：信息量 → 编码长度 → 熵 → 交叉熵 → KL · Gibbs 非负性证明 · forward vs reverse KL 的失败模式 · 最大似然 ≡ 最小 KL · 高斯闭式解 |
| [basic-theorems.html](basic-theorems.html) | 基本定理：贝叶斯变换 · 马尔科夫性质与 POMDP · Bellman 最优性原则 · 高斯的 ∝exp 形式 |

### 主流理论

| 页面 | 内容 |
|---|---|
| [diffusion-policy.html](diffusion-policy.html) | Diffusion Policy 图解与完整推导：误区纠正、弹球比喻与方向场动画、正向/反向过程、从 $\log p_\theta(x_0)$ 到 $L_{\text{simple}}$ 的完整 loss 推导、DP 原论文要点、Flow Matching 对比 |
| [ppo-learning.html](ppo-learning.html) | 强化学习到 PPO：三支流演进、Policy Gradient / Actor-Critic / GAE / Natural Gradient / TRPO / PPO 完整推导、5 个交互图、连续控制实现与训练诊断 |
| ↳ [ppo-variants-research.html](ppo-variants-research.html) | **PPO 相关研究**：局限、变体与灵巧抓取证据地图；从 ratio / clip / advantage 已知处继续，不重复基础推导 |

### 研究路线

| 页面 | 内容 |
|---|---|
| [l20-robust-grasp.html](l20-robust-grasp.html) | L20 Robust Grasp V1 实验路线（方案稿）：人类抓姿 → L20 retarget → joint teacher → 外生 wrist 适配 → finger student |
| [shared-control.html](shared-control.html) | 共享控制路线：从 To the Noise and Back 到 EMG 灵巧手 |

## 实验

| 页面 | 内容 |
|---|---|
| [dexhand-rl.html](dexhand-rl.html) | 灵巧手 RL 实验记录：锤钉与抓取，每个 reward 版本的视频与失败解剖 |
| [dexhand-engineering.html](dexhand-engineering.html) | 灵巧手 RL 工程记录：碰撞简化与 JAX→Warp 迁移 |
| [hand-control.html](hand-control.html) | Hand Control 技术路线手册：EMG + Quest 手部追踪 + L20 遥操作 |
