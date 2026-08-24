# Machine Learning Handbook · 编写规则

> 本文件是本仓库**唯一的规则来源**，面向所有 AI coding agent 与人类协作者。
> 根目录的 `AGENTS.md`（Codex 等）与 `CLAUDE.md`（Claude Code）只是自动加载用的指针，
> 内容以本文件为准；改规则改这里，不要改指针。

个人机器学习笔记站，GitHub Pages 直接发布（push 到 `main` 即上线）。
**每个页面都是一个自包含的单文件 HTML**，放在仓库根目录，没有构建步骤、没有框架、没有外部 JS 依赖（MathJax CDN 除外）。

改动这个仓库前先读完本文件。下面的规则不是建议，是约定——破坏其中任何一条都会让站点在导航、风格或可读性上出现裂缝。

---

## 1. 分类规则

站点只有两个顶层分类，在 `index.html` 里以 `<h2>` 呈现：

```
理论 THEORY & RESEARCH
├─ 基础概念      → foundations.html（清单页）
├─ 主流理论      → 一个方法从头推到尾
│    └─ 相关研究  → 缩进挂在它所属的方法下面
└─ 研究路线      → 论文地图 + 自己的架构设计，还没有数据

实验 EXPERIMENTS  → 自己跑出来的：版本、曲线、视频、失败解剖
```

### 新页面归到哪一类——按顺序问这四个问题

1. **它是被两篇以上笔记重复用到的底层工具吗？**（KL 散度、贝叶斯、马尔科夫、Bellman、重要性采样……）
   → **基础概念**。一条一页，登记进 `foundations.html`，不要塞进用到它的那篇笔记里。
2. **它是把某个方法从头推到尾吗？**（Diffusion Policy、PPO 学习路线）
   → **主流理论**。
3. **它有自己跑出来的数据吗？**（曲线、视频、benchmark 数字、失败回放）
   → 有 = **实验**；没有、只有论文调研和架构设计 = **研究路线**。
   判据是数据，不是完成度。标了「方案稿 / 尚未跑实验」的一律进研究路线。
4. **它是围绕某个已有方法展开的调研 / 局限分析 / 变体地图吗？**
   → **相关研究**，在 `index.html` 里用 `.sub` 缩进挂到那个方法下面，不单独占一张卡片。

### 分类的边界情况

- 一篇笔记同时讲方法推导和实验结果 → 按**主要产出**归类，另一半拆出去或在文中交叉链接。
- 研究路线页跑出数据后 → 移到实验区，并在原位置留一句指向新页的话。
- 拿不准 = 先放研究路线，它是最不容易误导读者的默认值。

---

## 2. 跳转规则（导航契约）

**`index.html` 是唯一入口。任何新页面必须在同一次改动里登记进 index，否则等于没发布。**

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

`--bg --panel --ink --sub --muted --line --line2 --blue --orange --green --red --magenta --yellow`
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

---

## 4. 写作规则

1. **大白话在前，推导在后。** 长小节开头先给一个 `.key.good` 总览框或 `.chain` 主线图，让人三十秒知道整节在干什么，然后再逐步展开。读者应该能只读前面那段就走。
2. **公式之间必须有 `.why`。** 每一步都要回答「为什么必须走这一步」，而不是罗列变形。连续两个 `$$` 之间没有解释文字 = 不合格。
3. **宁可多写一层，也不用错误的简化说法。** 例：不能说「$L_0$ 因为 $x_0$ 是确定值所以没有分布可比」——正确说法是它是 telescoping 的边界项，且硬凑 KL 的对象是点质量、KL 发散。遇到流传很广但不准确的解释，**明确指出它错在哪**。
4. **每个概念标「用在哪」。** 基础概念页尤其：写完定义后必须说清哪几页在用它、用在第几节。清单页可以反过来当索引读。
5. **数字必须可核对。** 引用实验数字要能追到曲线/视频/代码常量；引用论文结论要给链接。推导里的算例先自己算一遍再写。
6. **动画按解析解实时模拟，不用示意贴图。** 这是本站的一条硬标准，图里画的必须是真算出来的。
7. **中文为主，术语保留英文。** `policy`、`advantage`、`trust region`、`telescoping` 这类词不翻译，避免和文献对不上。
8. **失败要写。** 实验记录里失败版本的解剖比成功结果更有价值，不要只留最终版。

---

## 5. 图表规则

- **交互 / 模拟** → 原生 `<canvas>` + JS，读 CSS 变量取色（`getComputedStyle` 读 `--blue` 等），监听 `resize` 和 `prefers-color-scheme` 重绘。参考 `kl-divergence.html` 末尾的 `mk()` / `redrawAll()` 骨架。
- **静态结构示意** → 内联 `<svg>`，用 `currentColor` + `opacity` 取色，`viewBox` + `width:100%` 自适应。参考 `basic-theorems.html`。
- 不引任何图表库，不用外部图片托管。
- 图注（`.cap` / `<figcaption>`）要写**这张图在说什么**，不是重复标题。

---

## 6. 外部导入的页面

从别处生成、带自己整套配色的页面（如 `ppo-learning.html`、`ppo-variants-research.html`、`l20-robust-grasp.html`）：

- **保留原配色**，不强行改成手册主题——它们自成体系，改一半反而更乱。
- 但**必须补齐导航契约**：顶部 `.bk` 回链（用该页自己的 CSS 变量写样式）、footer 回链、以及与相关页面的双向链接。
- 文件名改成 kebab-case 的语义化名字（`ppo_learning_stage1.html` → `ppo-learning.html`），因为文件名会进 URL。
- 源文件从 `~/Downloads` 移进仓库后删掉原件，避免两份漂移。**移动前先 diff 确认仓库副本包含全部原始内容。**

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
□ 顶部 .bk 回链 + footer 回链都在
□ 相关研究 / 上下级页面双向链接已建立
□ 链接与锚点校验通过（脚本见下）
□ 本地 python3 -m http.server 预览过，深色浅色都看过
□ 公式渲染正常，表格在窄屏能横向滚动
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
print('broken:', bad)
```

---

## 9. Git

- 直接提交到 `main`，push 即发布。
- commit message 用中文，第一行说清**改了什么**，正文说清**为什么**和影响范围。推导类改动要写清楚改了哪一节、原来的说法错在哪。
- **不要主动 push**，除非明确要求。
- 大改动（重构导航、重排推导）单独成一个 commit，不要和内容修补混在一起。
