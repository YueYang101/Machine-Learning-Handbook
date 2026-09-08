# Machine Learning Handbook · 编写规则

> 本文件是本仓库**唯一的规则来源**，面向所有 AI coding agent 与人类协作者。
> 根目录的 `AGENTS.md`（Codex 等）与 `CLAUDE.md`（Claude Code）只是自动加载用的指针，
> `README.md` 与 `index.html` 只维护页面索引；内容以本文件为准。改规则只改这里，不在指针或索引中复制摘要。

个人机器学习笔记站，GitHub Pages 直接发布（push 到 `main` 即上线）。
页面是放在仓库根目录的纯静态 HTML，CSS 与页面逻辑内联；实验图片和视频可以放在本地 `assets/<page-slug>/`。
没有构建步骤、没有框架；MathJax CDN 是唯一默认允许的外部运行时依赖，不引图表库或外链图床。

改动这个仓库前先读完本文件。下面的规则不是建议，是约定——破坏其中任何一条都会让站点在导航、风格或可读性上出现裂缝。

---

## 1. 分类规则

站点有三个顶层分类，在 `index.html` 里各是一个标签页（`#theory` / `#plans` /
`#experiments`），面板内以 `<h2>` 呈现分类名：

```
理论 THEORY                  → 概念、推导、别人方法的局限与变体地图
├─ 基础概念      → foundations.html（清单页）
├─ 主流理论      → 一个方法从头推到尾
│    └─ 相关研究  → 缩进挂在它所属的方法下面
└─（不含我们自己的实验设计）

实验计划 PLANNED             → 方案与判据已定，还没有数据
├─ 研究路线      → 论文地图 + 自己的架构与实验设计
│    ├─ 项目选型综述 → literature review + 资产审计 + 当前取舍
│    └─ 当前一步    → 3–5 个动作、最小交付物与真实状态
└─ 待验证方案    → 针对某个已知缺陷的候选清单，每条带验证判据

实验记录 EXPERIMENTS         → 自己跑出来的：版本、曲线、视频、失败解剖
```

**「实验计划」与「实验记录」的分界线是数据，不是完成度。**一页写得再完整，
只要它的结论还没有被自己跑出来的数字支撑，它就在计划区。

### 新页面归到哪一类——按顺序问这五个问题

1. **它是被两篇以上笔记重复用到的底层工具吗？**（KL 散度、贝叶斯、马尔科夫、Bellman、重要性采样……）
   → **基础概念**。一条一页，登记进 `foundations.html`，不要塞进用到它的那篇笔记里。
2. **它是把某个方法从头推到尾吗？**（Diffusion Policy、PPO 学习路线）
   → **主流理论**。
3. **它有自己跑出来的数据吗？**（曲线、视频、benchmark 数字、失败回放）
   → 有 = **实验记录**。没有则继续往下问。
4. **没有数据的那一半，看它在描述谁的工作：**
   - 描述**别人的**方法、局限、变体 → **理论 → 相关研究**，在 `index.html` 里用 `.sub`
     缩进挂到那个方法下面，不单独占一张卡片（例：`ppo-variants-research.html`）。
   - 描述**我们自己**要做什么——架构设计、实验协议、候选修法清单 → **实验计划**，
     单独占一张卡片（例：`l20-robust-grasp.html`、`retargeting-research.html`）。
   - 为某个项目选择数据、模型与工程底座的 **literature review**，主要产出是「我们采用谁、如何接入、何时启用」→ **实验计划 → 研究路线的配套选型综述**。不能只因引用很多论文就挪进理论区；与母计划、操作说明双向索引。
   一页两者都有时按**主要产出**判：读者是来看「这个方法有什么已知问题」，
   还是来看「我们接下来要跑什么」。
5. **它是某一页的配套 research 页吗？**（无论落在哪个分类）
   → 两页必须**双向链接**，并各用一句话说清分工，见下面的跳转规则。

### 分类的边界情况

- 一篇笔记同时讲方法推导和实验结果 → 按**主要产出**归类，另一半拆出去或在文中交叉链接。
- 实验计划页跑出数据后 → 移到实验记录区，并在原位置留一句指向新页的话；
  计划页本身只保留还没有数据的条目。
- 长期维护的 runbook 不因某次执行有数据而整页搬走：保留协议 URL，在实验记录区另建带 run ID 的结果页，双向链接。引用历史资产的核验结果，也不等于当前实验已经执行。
- 拿不准 = 先放实验计划，它是最不容易误导读者的默认值——把没跑过的东西
  摆在实验记录里，比归错类更糟。

---

### 项目文档分工与执行粒度（2026-09-08，按用户反馈收敛）

1. **高浓度、渐进展开。** 主计划只写最终目标、三步左右的主线和当前唯一优先事项，以一屏要点为目标。文献放独立子页，真实实验另记日志；不要把研究地图变成同时执行的任务清单。
2. **stage 只展开当前一步。** 用 3–5 个动作写清做什么、用什么现有资产、交付什么及当前状态。不要在尚未执行时预写十步工程清单、全部问题和故障分支。只有用户明确要求某项实施细节，或实验已经走到该处，才继续展开。
3. **不预测所有问题，不预填配置。** 尚未进入训练就不把 reward 权重、PPO 预算、观测维度和统计门槛写成既定要求。实际实现／运行时记录生效参数、单位、指标定义与分母；改变已运行协议时保留版本和原因。备选方法不是当前承诺。
4. **计划台账不冒充实验 log**。只有实际运行且有原始证据的行才能标「通过／失败」；否则标「待执行／待适配／未核验」。日志至少含日期、run ID、代码与资产版本、实际配置、样本分母、结果位置、失败原因和下一步。文档修改日期不是训练日期，公式算例不是实验成绩。
5. Handbook **只保存说明、推导、协议与结果摘要**，不替实现项目创建训练脚本、可执行配置或伪造 checkpoint。可约定未来产物名，但必须标注「待生成」。除非用户明确要求实现，不修改其他项目代码、不启动训练。
6. 扩展已有研究前，先核验用户指定的相邻项目：README、关键代码、带日期的配置／原始结果。区分「资产存在」「能按原本体复现」「已迁移到当前本体」。过期 README 不能覆盖较新的原始记录；单次成功、六向重力测试、动态抗扰和端到端 pick 的成绩不可互换。
7. 文献选型至少记录标题、作者、年份／发表状态、一手来源、方法输入输出、代码／权重／数据可用性、接入当前本体的缺口。区分 cross-object 与 cross-embodiment，不能把「跨本体论文」写成「任意新手直接即用」。不以论文自称 SOTA、星数或年份代替同协议比较与复用证据。
8. **需要做比较时，分清来源与控制器。** 人类数据、生成模型和优化器可组合；比较 controller 时固定初态和测试条件。这是实验公平性原则，不要求第一轮接齐所有方法。
9. **以最新 PoC 边界为准。** 当前 Stage 1.1 仅做单一 cube 的多样抓姿与意图预测，先回归，验证不满足需求后再考虑分类；不要把承重、稳定性、抗扰或 pick 重新加为前置验收。生成姿态、预测意图与稳定控制是不同验证目标，不能互相替代。

## 2. 跳转规则（导航契约）

**`index.html` 是公开站点入口。任何新增、重命名、删除或重新分类的页面，都必须在同一次改动里同步 `index.html` 与 `README.md`；两处分类和描述必须一致，否则等于没发布。**新增分类还要同步本文件 §1 的分类树与判定问题——三处任何一处漏改，下一个人就会按旧规则归错类。

### 每一页都必须有的两个回链

顶部，`.kicker` 之前：

```html
<a class="bk" href="index.html">← Machine Learning Handbook</a>
```

如果这一页有上级页（基础概念条目的上级是 `foundations.html`），先写上级再写主页：

```html
<a class="bk" href="foundations.html">← 基础概念清单</a> · <a class="bk" href="index.html">Machine Learning Handbook</a>
```

footer 里再放一次回主页链接。两处都要，因为长页读到底不会有人往回滚。

### 页面之间的链接

| 关系 | 要求 |
|---|---|
| 基础概念条目 ↔ 清单页 | 条目顶部指向 `foundations.html`；清单页登记该条目，并写明「**被用在** → 谁在用它」 |
| 相关研究 ↔ 它所属的方法 | **双向**。研究页顶部写「前置阅读：<方法页>」，方法页正文写「配套 research 页：<研究页>」 |
| 引用一个基础概念 | 第一次出现时链接过去，**不在本页重复推导**。需要用到结论就直接引结论 |
| 引用同一站内某节 | 用带锚点的相对链接，如 `diffusion-policy.html#m4`。目标 `id` 必须真实存在 |
| 两页讲同一件事的不同切法 | 互相链接并**用一句话说清区别**，不要只丢个链接 |

### 锚点规则

- 每个 `<h2>` 都要有稳定的 `id`，一旦被别处链接就**不再改名**。
- 站内链接一律相对路径，不写域名——本地 `python3 -m http.server` 预览要能跑通。
- 外部链接（arXiv 等）直接写全 URL，不需要 `target="_blank"`。

---

## 3. 页面结构模板

### 页面家族

- 新建理论/基础页面默认采用下述**手册标准样式**：浅色与暗色 token、840px 阅读栏、编号章节、解释框、公式与交互图。
- 已有研究 dossier、深色课程页和工程实验日志可以保留自洽主题，但不得因此绕过导航、响应式、无障碍与证据规则。
- 同一页面只保留一个稳定 URL。升级旧内容时优先原地替换，除非新旧页面有明确不同的阅读任务。

新建**手册标准样式**的页面时，直接把 `diffusion-policy.html` 或 `kl-divergence.html` 从第 1 行复制到 `</style>` 之前（不要写死行号，它会随样式增补而漂移），只改 `<title>`，然后追加本页特有的样式再收尾 `</style></head><body>`。这样全站配色、暗色模式、MathJax 配置自动一致。

```bash
# 在仓库根目录跑：取模板头部（不含结尾的 </style>，方便直接追加本页样式）
sed -n "1,$(($(grep -n '</style>' kl-divergence.html | head -1 | cut -d: -f1) - 1))p" kl-divergence.html > 新页.html
```

复制过来后**删掉模板页自己的专用样式**（`.pill`、`td.n` 这类），只保留 `:root` 变量和通用 class。

```html
<div class="wrap">
  <a class="bk" href="index.html">← Machine Learning Handbook</a>
  <div class="kicker">MACHINE LEARNING HANDBOOK · 分类名</div>
  <h1>主标题<br><span style="font-size:.72em;color:var(--sub)">副标题：这一页到底解决什么</span></h1>
  <p class="lede">这一页做什么、为谁写、读完能得到什么。</p>
  <div class="toc"><b>目录</b> · <a href="#s1">§1 …</a> · …</div>

  <h2 id="s1"><span class="n">§ 1</span>小节标题</h2>
  …
  <footer>… · <a href="index.html">← Machine Learning Handbook</a></footer>
</div>
```

### 共享 CSS 变量（不要引入新的颜色字面量）

`--bg --panel --panel2 --ink --sub --muted --line --line2 --blue --blue-fill --focus --orange --green --red --magenta --yellow --violet --cyan`
每个都在 `:root` 和 `@media (prefers-color-scheme: dark)` 下各定义一次。**任何颜色都必须走变量**，否则暗色模式会破。

### 通用 class

| class | 用途 |
|---|---|
| `.wrap` | 页面容器（840px；index 用 760px） |
| `.kicker` `.lede` `.toc` | 页眉小标、导语、目录 |
| `.key` `.key.good` `.key.bad` `.key.warn` | 结论框。good=正确做法/回报，bad=失败模式，warn=易错点 |
| `.math` + 内部 `.why` | 公式块；`.why` 是公式之间的解释段 |
| `.figwrap` + `.cap` | 图（canvas）+ 图注；`.figrow` 并排多图 |
| `.tw` 包 `<table>` | 表格横向滚动，手机上必须 |
| `.duo` | 两栏对照；`.algo` 算法/要点小卡 |
| `.bk` | 回链 |
| `.used` | 「被用在哪」标注（基础概念页） |
| `.chain` | 推导主线流程图（`.cr` 行 / `.cb` 方框 / `.ar` 箭头注） |

### 响应式与无障碍契约

- 正常文字与背景对比度至少 4.5:1；焦点轮廓与相邻背景至少 3:1。链接不能只靠很接近正文的颜色区分。
- 使用语义化 `nav`、`main`、heading、`label`、`caption` / `figcaption`；装饰性元素不进入键盘焦点序列。
- 原生按钮和主要控件的触控高度至少 44px，必须有 `:focus-visible`；range 使用原生键盘行为并保留可读 label。
- Canvas 必须有可读的 `role` / `aria-label`、正文图注和无 2D context 时的降级说明；可交互数据不能只靠颜色表达。
- 表格放进可横向滚动容器；多栏 grid 在窄屏降为单栏；Canvas 按 client width 与 DPR 重建 backing bitmap，DPR 上限 2。
- 动画遵守 `prefers-reduced-motion`，页面隐藏或图离屏时停止调度；恢复时重置时间基准，不能永久空跑 `requestAnimationFrame`。

---

## 4. 写作规则

1. **大白话在前，推导在后。** 长小节开头先给一个 `.key.good` 总览框或 `.chain` 主线图，让人三十秒知道整节在干什么，然后再逐步展开。读者应该能只读前面那段就走。
2. **公式之间必须有 `.why`。** 每一步都要回答「为什么必须走这一步」，而不是罗列变形。连续两个 `$$` 之间没有解释文字 = 不合格。
3. **宁可多写一层，也不用错误的简化说法。** 例：不能说「$L_0$ 因为 $x_0$ 是确定值所以没有分布可比」——正确说法是它是 telescoping 的边界项，且硬凑 KL 的对象是点质量、KL 发散。遇到流传很广但不准确的解释，**明确指出它错在哪**。
4. **每个概念标「用在哪」。** 基础概念页尤其：写完定义后必须说清哪几页在用它、用在第几节。清单页可以反过来当索引读。
5. **数字必须可核对。** 引用实验数字要能追到曲线/视频/代码常量；引用论文结论要给链接。推导里的算例先自己算一遍再写。
6. **数据图和模拟按真实公式计算，不用伪造贴图。** 能解析计算的动画必须实时计算；纯流程示意必须明确标注“示意”，不能伪装成实验结果。
7. **中文为主，术语保留英文。** `policy`、`advantage`、`trust region`、`telescoping` 这类词不翻译，避免和文献对不上。
8. **失败要写。** 实验记录里失败版本的解剖比成功结果更有价值，不要只留最终版。

---

## 5. 图表规则

- **交互 / 模拟** → 原生 `<canvas>` + JS，读 CSS 变量取色（`getComputedStyle` 读 `--blue` 等），监听容器尺寸和 `prefers-color-scheme` 重绘；离屏、后台与 reduced-motion 状态必须停动。参考 `ppo-learning.html` 的 Canvas 生命周期。
- **静态结构示意** → 内联 `<svg>`，用 `currentColor` + `opacity` 取色，`viewBox` + `width:100%` 自适应。参考 `basic-theorems.html`。
- 不引任何图表库，不用外部图片托管。
- 图注（`.cap` / `<figcaption>`）要写**这张图在说什么**，不是重复标题。

---

## 6. 外部导入的页面

从别处生成、带自己整套配色的页面（如 `ppo-learning.html`、`ppo-variants-research.html`、`l20-robust-grasp.html`）：

- **保留原配色**，不强行改成手册主题——它们自成体系，改一半反而更乱。
- 但**必须补齐导航契约**：顶部 `.bk` 回链（用该页自己的 CSS 变量写样式）、footer 回链、以及与相关页面的双向链接。
- 文件名改成 kebab-case 的语义化名字（`ppo_learning_stage1.html` → `ppo-learning.html`），因为文件名会进 URL。
- 导入前后先 diff，确认仓库副本包含全部原始内容。移动或删除 `~/Downloads` 等仓库外原件必须得到明确授权；默认只复制并报告来源，不能替用户清理。

---

## 7. 文件与资源

- 页面：仓库根目录，kebab-case，`.html`。
- 资源：`assets/<page-slug>/`（如 `assets/dexhand-rl/`）。视频用 mp4，注意单文件体积。
- `.DS_Store` 已在 `.gitignore` 里，不要提交。
- 不建子目录放页面——URL 越短越好，站点规模也还不需要。

---

## 8. 发布前检查清单

```
□ index.html 里登记了新页面，归类正确
□ README.md 与 index.html 同步，根目录每个内容页各登记一次
□ 顶部 .bk 回链 + footer 回链都在
□ 相关研究 / 上下级页面双向链接已建立
□ 链接与锚点校验通过（脚本见下）
□ 本地 python3 -m http.server 预览过，深色浅色都看过
□ 375px 与桌面宽度均检查；公式渲染正常，表格在窄屏能横向滚动
□ 键盘、focus、文字对比度、reduced-motion 与 Canvas 降级路径检查过
□ 控制台无 error/warning，页面 hidden/离屏时动画不会继续空跑
□ 数字与结论自己核对过
```

链接校验脚本（在仓库根目录跑）：

```python
import re, os, glob
ids = {os.path.basename(f): set(re.findall(r'id="([^"]+)"', open(f).read())) for f in glob.glob('*.html')}
bad = 0
for f in sorted(glob.glob('*.html')):
    s = open(f).read()
    for h in set(re.findall(r'href="([^"#][^"]*?)"', s)):
        if h.startswith(('http', 'mailto')): continue
        t = h.split('#')[0]
        if t and not os.path.exists(t): print('BROKEN', f, '->', h); bad += 1
    for a in set(re.findall(r'href="#([^"]+)"', s)):
        if a not in ids[os.path.basename(f)]: print('BROKEN ANCHOR', f, '#' + a); bad += 1
    for t, a in set(re.findall(r'href="([a-z0-9\-_]+\.html)#([^"]+)"', s)):
        if a not in ids.get(t, set()): print('BROKEN XANCHOR', f, '->', t + '#' + a); bad += 1
content_pages = set(ids) - {'index.html'}
for catalogue in ('index.html', 'README.md'):
    linked = set(re.findall(r'([a-z0-9\-]+\.html)', open(catalogue).read()))
    for page in sorted(content_pages - linked):
        print('MISSING FROM INDEX', catalogue, '->', page); bad += 1
print('broken:', bad)
```

---

## 9. Git

- 直接提交到 `main`，push 即发布。
- commit message 用中文，第一行说清**改了什么**，正文说清**为什么**和影响范围。推导类改动要写清楚改了哪一节、原来的说法错在哪。
- **不要主动 push**，除非明确要求。
- 大改动（重构导航、重排推导）单独成一个 commit，不要和内容修补混在一起。
