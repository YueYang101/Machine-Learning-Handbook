# Machine-Learning-Handbook

个人机器学习笔记，单文件 HTML，可直接在浏览器打开（公式用 MathJax，动画为原生 canvas，无构建步骤）。

**在线阅读：** https://yueyang101.github.io/Machine-Learning-Handbook/
**编写规则：** [STYLE.md](STYLE.md) —— 分类、跳转、样式与写作约定，改动前先读。

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
| [ppo-learning.html](ppo-learning.html) | PPO 学习路线：MDP → Bellman → MC/TD → Policy Gradient → Actor-Critic → GAE → TRPO → PPO（Stage 1 已完成） |
| [ppo-variants-research.html](ppo-variants-research.html) | *相关研究* · PPO 的局限、变体与灵巧抓取证据地图 |

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
