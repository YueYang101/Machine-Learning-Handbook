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
| [shared-control.html](shared-control.html#stages) | 共享控制路线：从 To the Noise and Back 到 EMG 灵巧手；下属 Stage 1.x 小阶段统一入口，历史架构与当前进度分开 |
| ↳ [l20-robust-grasp-stage1.html](l20-robust-grasp-stage1.html) | Stage 1.1 数采与标签：已有单 cube 的 95 条 pinch PoC；保留采集协议，正式数据验收另记 |
| ↳ [l20-stage1-2-training.html](l20-stage1-2-training.html) | Stage 1.2 意图预测与模型比较：已有终点回归与序列生成对照，区分输入历史、预测提前量与输出目标 |
| ↳ [l20-stage1-3-shared-grasp.html](l20-stage1-3-shared-grasp.html) | Stage 1.3 意图条件的共享抓取控制：已有残差 RL 与仲裁 PoC，物理后端差异限制收益结论，完整任务仍待验证 |
| ↳ [l20-stage1-alternatives.html](l20-stage1-alternatives.html) | Stage 1.2 配套候选：几何评分、递归贝叶斯、VLM 先验及融合；按问题选用，均待验证 |
| ↳ [l20-grasp-sources-review.html](l20-grasp-sources-review.html) | 配套选型综述：人手 Retarget / 模型生成 / 数学优化，数据库、方法与已有资产审计；按需查阅，不作为同时执行的任务 |

### 待验证方案

配套候选随所属路线维护；下列保留独立的缺陷分析与验证方案。

| 页面 | 内容 |
|---|---|
| [retargeting-research.html](retargeting-research.html) | Retargeting 的局限与候选解法（配套 [hand-control.html](hand-control.html)）：小指 curl 与侧摆的统一根因 · 六条待验证候选与判据 · AnyTeleop / dex-retargeting 详档与整包引进的裁决 |

## 实验记录

| 页面 | 内容 |
|---|---|
| [l20-stage1-2-results.html](l20-stage1-2-results.html) | Stage 1.2 结果：意图预测／人类模型建模——95 条 pinch 示教留一 session 的阶梯结果、影子手逐帧预测视频、序列生成器与输入消融、数据侧发现、Stage 1.3 第二步物理回放预检；2026-09-14 追加：实时预测进头显（影子手／接触点、可切换预测器、与数采隔离）与「预测物体上的点」两次消融（接触头以平均先验落地） |
| [l20-stage1-3-results.html](l20-stage1-3-results.html) | Stage 1.3 结果：共享抓取残差 RL 首轮——L20SharedPinch 环境实现与录像核对、零残差基线、门控残差 20M 步与 α=0 的配对比较（1–7 个百分点）、α≡1 对照臂 +8–16 个百分点（授权上限是主因）、按指门控／速度缩放臂、α 扫描（收益在 0.3–0.5 饱和、门控低 6–8 点、平均位姿目标 = oracle，不需预测器）、真机接线（影子仿真 + 部署包络）、预测器接入（对手指动作无影响、只影响门控时机）、接触点目标臂、jax 与 Warp 后端不等价（离群的是 jax；Warp 下纯人手回放已 98%–100%，手指残差无东西可补）、berlin 与 4090 运行方式、视频 |
| [dexhand-rl.html](dexhand-rl.html) | 灵巧手 RL 实验记录：锤钉与抓取，每个 reward 版本的视频与失败解剖 |
| [dexhand-engineering.html](dexhand-engineering.html) | 灵巧手工程记录：Quest 真人搬运与物理力审计、RT 已试／未验证对照、新手势测试；历史碰撞简化与 JAX→Warp 迁移 |
| [hand-control.html](hand-control.html) | Hand Control 技术路线手册：EMG + Quest 手部追踪 + L20 遥操作 |
