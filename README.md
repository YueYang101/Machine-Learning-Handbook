# Machine-Learning-Handbook

个人机器学习笔记站，使用纯静态 HTML，可直接在浏览器打开；公式由 MathJax 渲染，交互图使用原生 canvas，实验图片与视频存放在本地 `assets/`，没有构建步骤。

- **在线阅读：** [yueyang101.github.io/Machine-Learning-Handbook](https://yueyang101.github.io/Machine-Learning-Handbook/)
- **唯一编写规范：** [STYLE.md](STYLE.md)
- **工具入口：** [AGENTS.md](AGENTS.md) 与 [CLAUDE.md](CLAUDE.md) 仅负责指向 `STYLE.md`，不重复维护规则。

## 站点入口

| 页面 | 内容 |
|---|---|
| [index.html](index.html) | GitHub Pages 首页与公开导航；理论 / 实验计划 / 实验记录 三个标签页（`#theory` / `#plans` / `#experiments` 可直接分享），分类层级与本索引及 `STYLE.md` §1 保持同步 |

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

## 实验计划

研究路线、项目选型综述和待执行操作说明。实际运行结果归「实验记录」；长期维护的 runbook 保留在计划区，与带 run ID 的结果页双向索引。

### 研究路线

| 页面 | 内容 |
|---|---|
| [l20-robust-grasp.html](l20-robust-grasp.html) | L20 Robust Grasp：三条长期主线——L20 robust grasp、真人手预训练并经 retargeting 迁移到 L20、面向残障用户的 online learning；当前短期先数采，再做 L20 抓姿训练 |
| [l20-robust-grasp-stage1.html](l20-robust-grasp-stage1.html) | Stage 1.1 数采（preparation 待验收）：10 条试跑回放 → 3 手形 × 4 方向 × 2 位置 × 10 重复，共 240 条平衡 L20 示教 + 24 条改意图／取消诊断 → 冻结字段、坐标、标签与 144／48／48 session 划分 |
| [l20-stage1-2-training.html](l20-stage1-2-training.html) | Stage 1.2 Training（首个 run 结果见 [l20-stage1-2-results.html](l20-stage1-2-results.html)）：两个方案并列——A 删除 gaze／物体分支的 VQ-VAE＋自回归 Transformer 预测未来序列；B 状态条件 Flow Matching 生成多个最终 L20 手姿候选；共享确定性基线与冻结划分 |
| [l20-stage1-3-shared-grasp.html](l20-stage1-3-shared-grasp.html) | Stage 1.3 意图条件的共享抓取控制（方案已记录，待执行）：复用 1.2 预测 → 候选选择与几何修正 → 目标条件闭环执行；T0–T3 分开验证预测与执行收益，按需升级 RL／残差；参考 DexGen 动作先验 |
| ↳ [l20-grasp-sources-review.html](l20-grasp-sources-review.html) | 配套项目选型综述（计划）：人类数据库与几何／捏合／接触／物理 retarget；模型生成与数学优化；既有 ORCA BODex 资产审计、L20 适配缺口；GraspADMM / DexEvolve / CoToGrasp 等近期进展；可用性与后续接口备忘；是独立文献库，不是并行待办 |
| [shared-control.html](shared-control.html) | 共享控制路线：从 To the Noise and Back 到 EMG 灵巧手 |

### 待验证方案

| 页面 | 内容 |
|---|---|
| [l20-stage1-alternatives.html](l20-stage1-alternatives.html) | Stage 1.2 其他方案（四条待验证）：与主方案共享 Quest 示教；几何评分、递归贝叶斯、VLM 语义先验及融合；统一完整抓姿、数据划分与误差／提前量对照 |
| [retargeting-research.html](retargeting-research.html) | Retargeting 的局限与候选解法（配套 [hand-control.html](hand-control.html)）：小指 curl 与侧摆的统一根因 · 六条待验证候选与判据 · AnyTeleop / dex-retargeting 详档与整包引进的裁决 |

## 实验记录

| 页面 | 内容 |
|---|---|
| [l20-stage1-2-results.html](l20-stage1-2-results.html) | Stage 1.2 结果：意图预测／人类模型建模——95 条 pinch 示教留一 session 的阶梯结果、影子手逐帧预测视频、序列生成器与输入消融、数据侧发现、Stage 1.3 第二步物理回放预检 |
| [dexhand-rl.html](dexhand-rl.html) | 灵巧手 RL 实验记录：锤钉与抓取，每个 reward 版本的视频与失败解剖 |
| [dexhand-engineering.html](dexhand-engineering.html) | 灵巧手工程记录：Quest 真人搬运与物理力审计、RT 已试／未验证对照、新手势测试；历史碰撞简化与 JAX→Warp 迁移 |
| [hand-control.html](hand-control.html) | Hand Control 技术路线手册：EMG + Quest 手部追踪 + L20 遥操作 |
