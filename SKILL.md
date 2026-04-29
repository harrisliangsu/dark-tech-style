---
name: dark-tech-style
description: 暗色科技风 HTML 一页应用的视觉风格系统。当用户需要做架构图、技术全景页、产品 Landing、Dashboard、控制台、Roadmap、技术汇报页、One-Pager、Showcase、深色主题信息密集型页面时，必须使用此技能保证视觉一致性。触发词包括：架构图、技术全景、Landing 页、Dashboard、产品介绍页、技术汇报、暗色主题、深色科技风、cyber 风、tech style、dark theme。即使用户没有明确说"用 dark-tech-style"，只要是构造一个结构化的、信息密集的、偏技术调性的网页，都应当默认采用这套风格。
---

# Dark Tech Style

一套用于构建暗色科技风 HTML 页面的设计系统。提取自一份高质量架构全景页，覆盖架构图、技术全景、Landing、Dashboard、Roadmap 等场景。

## 使用方式

**总是优先采用 `assets/tokens.css` 中已定义的 token 和组件类**，不要重新发明颜色或圆角。如果用户没有特别指定风格但要做一个偏技术调性的页面，就把这套风格作为默认。

最快路径：
1. 读 `assets/tokens.css`，把整个 `:root { ... }` 块和重置/基础部分原样塞进 `<style>`
2. 参考 `assets/starter.html` 的结构，按需要的章节挑选组件拼装
3. 如果用户给了内容，把内容填入这套结构；不要为了"丰富"而无中生有加章节

## 风格指纹（一段话理解）

近黑三级背景（`#0a0c14` → `#10121c` → `#161924`），几乎不可见的 6% 白色边框（hover 升到 12%），超粗 800 字重 + 强烈负字距（-0.02em ~ -0.03em）的大标题，配 7 色高亮系（橙/蓝/绿/金/紫/红/青）每色都有 15% 透明的 `dim` 变体作软背景。每个 section 都有「11px UPPERCASE kicker 标签 + clamp 大标题 + 二级文字副标题」三件套。数字和关键词用 135° 渐变文字。导航玻璃态（backdrop-blur 20px）。卡片 14px 圆角，hover 边框透明度上升。代码/文件名等宽字体，正文 SF Pro / PingFang。

## 设计 Token 速查

读完 `tokens.css` 你就有了，这里是关键速查：

**背景**（从外到内越浅）`--bg-deepest` → `--bg-surface`（用作内嵌面板/tab/代码块背景）→ `--bg-card` → `--bg-card-hover`

**文字** `--text-primary`（标题/数据）→ `--text-secondary`（正文）→ `--text-tertiary`（说明/scrollbar）

**边框** `--border`（默认）→ `--border-hover`（hover）

**高亮 7 色**：`--accent-{orange,blue,green,gold,purple,red,cyan}`，每个都有对应的 `-dim` 变体（15% 透明）。**给每个 section / 类别选一个固定颜色**，不要在同一个 section 里混色。

**圆角** `--radius: 14px`（卡片）/ `--radius-sm: 8px`（按钮、小标签）

## 颜色使用法则

这是这套风格最容易做坏的地方，请认真对待：

1. **每个 section 或类别绑定一种 accent**。比如「需求阶段」用 orange，「编码阶段」用 green，「审查阶段」用 purple。同一类别里所有元素（kicker 颜色、卡片左边框、徽章、icon、数字渐变）都用这一种 accent。
2. **`dim` 变体只用作软背景**（badge 底色、icon 容器底色），不要用作文字。
3. **白色文字不要纯白**，用 `--text-primary` (`#e2e5ef`)，纯白会和 800 字重叠加显得过亮刺眼。
4. **不要新发明颜色**。如果觉得 7 色不够用，先想想是不是 section 切得太细了。
5. **状态语义**：成功 = green，警告 = gold，错误/硬约束 = red，信息/链接 = blue，进度/演进 = purple。

## 标准组件清单

`tokens.css` 已经定义好以下组件类，直接用：

| 组件 | 类名 | 用途 |
|---|---|---|
| 玻璃态导航 | `.nav` `.nav-logo` `.nav-links` | 顶部 56px 固定导航 |
| Hero 容器 | `.hero` `.hero-badge` `.hero-desc` `.hero-stats` | 首屏，自带椭圆光晕 |
| 渐变文字 | `.grad-{orange,blue,green,purple}` | 数字、关键词高亮 |
| Section 三件套 | `.section-label` `.section-title` `.section-subtitle` | 每个章节的头部 |
| 卡片 | `.card` + 可选 `.card-rail-{color}` | 主要容器；rail 版有 3px 左边框 |
| 网格 | `.grid-2` `.grid-3` `.grid-4` | 768px 以下自动单列 |
| Tab 切换 | `.tab-bar` + `.tab-btn` / `.tab-btn.active` | 多视图切换 |
| 徽章 | `.badge` | 11px 小标签，背景用 `-dim` 配色 |
| 类别圆点 | `.pillar-dot` | 10px 实心圆，标识类别色 |
| 时间轴 | `.timeline-item` `.timeline-num` `.timeline-line` | 数字圆角 + 垂直连接线 |
| 进度条 | `.progress-bar` `.progress-fill` | 6px 高，1s 动画 |
| 流水线箭头 | `.flow-container` `.flow-phase` `.flow-arrow` | 横向阶段流 |
| 终端 mock | `.terminal` `.terminal-header` `.terminal-body` `.terminal-prompt` | 三圆点 header + 等宽命令体 |
| 动画 | `.fade-up`、`@keyframes pulse` | 进场动画、状态点呼吸 |

## 章节模式（按需挑选）

一个完整页面常见的章节顺序，**不需要全部都用**，按内容多少挑：

1. **Hero**：badge → 大标题（一段渐变 + 一段普通）→ 一句话描述 → 4 个 stat 数字
2. **Executive Summary**：2×2 卡片网格，每张卡片一个 pillar-dot + 标题 + 一段说明
3. **Tab + Detail**：顶部 tab 切换不同维度，下面动态展示当前 tab 的卡片详情
4. **Pipeline / Flow**：横向阶段卡 + 箭头连接，可点击展开详情
5. **Layered Architecture**：纵向层叠卡片，每层 `.card-rail-{color}` + 内嵌 `.grid-3` 列出文件/模块
6. **Three-pillar / Defense-in-depth**：3 列卡片，每张大 emoji + 彩色标题 + 说明
7. **Maturity Model**：纵向卡片列表，当前等级用边框加粗标记 + "当前位置" 徽章 + 进度条
8. **Gap Analysis**：CSS Grid 模拟的紧凑表格（48px 序号列 + 110px 名称 + 80px 等级徽章 + 1fr 已有 + 1fr 待建）
9. **Roadmap / Timeline**：`.timeline-item` 串联，每个阶段下嵌套子任务卡片
10. **Distance Radar**：6 项维度，每项一个进度条 + 已建/待建并列两栏
11. **KPI**：3 列分组，每组一个标题色 + 多个 "名称 / 大数字 / 描述" 行
12. **Quick Start (Terminal)**：`.terminal` mock，命令前缀 `$`，命令体绿色等宽
13. **Footer**：1px 上边框 + 居中两行小字（品牌 + 作者/年份）

## 字体规范

- **西文 + 中文**默认：`-apple-system, 'SF Pro Display', 'Helvetica Neue', 'PingFang SC', 'Microsoft YaHei', sans-serif`
- **代码 / 文件名 / 命令**：`'SF Mono', 'Fira Code', 'Cascadia Code', Menlo, monospace`
- **大标题**：`font-weight: 800`，`letter-spacing: -0.02em` 到 `-0.03em`，`line-height: 1.1` ~ `1.2`
- **kicker 标签**：`font-size: 11px`，`font-weight: 600`，`letter-spacing: 0.12em`，`text-transform: uppercase`
- **正文行高**：`1.6`（紧）到 `1.7`（描述/段落）

## 实施流程

接到一个页面需求时：

1. **确认结构**：把用户内容拆成 3-8 个章节，从「章节模式」清单里挑对应组件。如果用户给的是一篇文档，先把信息分组（核心理念 / 架构 / 流程 / 数据 / 路线图 / 安装），每组对应一个章节。
2. **绑定颜色**：给每个章节/类别分配一个 accent，写下来不要混。一般 hero 用 orange/blue（暖/冷调主导），后续章节按语义分配。
3. **拼装页面**：粘贴 `tokens.css` 内容到 `<style>`，参考 `starter.html` 拼装章节，**保留 inline style 的格式风格**（这套风格大量使用 inline style 来精细控制颜色变体，不需要为此抽 class）。
4. **填内容**：用户给的具体文案 / 数字 / 模块名直接填进去。不要为了对齐而编造数据。
5. **检查**：

   - 全部颜色都来自 token 吗？（grep 找硬编码 hex）
   - 每个 section 有 kicker 三件套吗？
   - 大标题字重 800 了吗？
   - 数字用渐变了吗？

## 输出格式

默认输出**单文件 HTML**（CSS 内联在 `<style>` 里），方便用户直接 `open` 预览。如果用户特别要求或页面规模很大（>1500 行），可以拆出 `tokens.css` 单独引用。

复杂交互（tab 切换、点击展开）默认用 React 18 + Babel CDN（参考原始风格的实现）。简单静态页用纯 HTML+CSS 即可，不要为了静态展示引入 React。

## 反模式

- 不要用 Material Design / Bootstrap 的颜色（蓝色不是 `#1976d2`，是 `#3b82f6`）
- 不要用纯黑 `#000` 作背景，会显得廉价；用 `--bg-deepest` (`#0a0c14`)
- 不要给卡片加阴影；这套风格用边框透明度，不用 box-shadow
- 不要用 emoji 作为主要图标系统；如果需要图标，用 lucide / feather 风格的线性 SVG（stroke-width 2）
- 不要让 section padding 小于 `60px 24px`；信息要呼吸
- 不要在同一个 section 里混用多个 accent；混色 = 失败
