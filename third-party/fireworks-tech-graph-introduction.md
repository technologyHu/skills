# fireworks-tech-graph 介绍

## 基础信息

| 项目 | 内容 |
| --- | --- |
| Skill 名称 | `fireworks-tech-graph` |
| 显示名称 | Fireworks Tech Graph |
| 所属分类 | 开发工具 / 文档处理 / 可视化 |
| 适用平台 | Claude Code / Codex / 其他支持 skill 的 AI 助手 |
| 当前版本 | main 分支 (2026-06-03) |
| 维护者 | yizhiyanhua-ai (Organization) |
| 来源 | 开源项目 |
| GitHub 仓库 | https://github.com/yizhiyanhua-ai/fireworks-tech-graph |
| 其他来源链接 | npm: @yizhiyanhua-ai/fireworks-tech-graph |
| 许可证 | MIT |
| 更新时间 | 2026-06-09 |

## 简介

`fireworks-tech-graph` 是一个用于**从自然语言描述生成高质量 SVG+PNG 技术图表**的 skill。它适合在**撰写技术文档、设计系统架构、绘制流程图**等场景中使用，可以帮助 AI 助手快速将文字描述转换为专业的可视化图表，无需手动绘制或学习 DSL 语法。

项目核心亮点：
- **8 种视觉风格** — 从扁平图标到暗黑终端、从蓝图到玻璃拟态
- **14 种图表类型** — 完整支持所有 UML 图表类型
- **AI/Agent 领域模式** — 内置 RAG、Agentic Search、Mem0、Multi-Agent 等架构模板
- **语义化图形词汇** — LLM 用双线矩形、Agent 用六边形、向量存储用带环圆柱

## 适用场景

- **架构设计**：用户需要绘制系统架构图、微服务架构、数据流图时触发
- **流程可视化**：绘制业务流程、决策流程、API 调用序列等
- **AI 系统文档**：绘制 RAG 流程、Agent 架构、多智能体协作等 AI 领域图表
- **技术演示**：生成可用于博客、幻灯片、README 的专业图表
- **UML 建模**：生成类图、组件图、部署图、时序图等标准 UML 图表

## 不适用场景

- 需要交互式动画或动态图表的场景（输出为静态 SVG/PNG）
- 需要精确像素级控制的手绘风格图表
- 需要实时协作编辑的场景（建议使用 draw.io 或 Figma）
- 超大规模复杂系统图（建议拆分为多个子图）

## 详细功能介绍

### 核心能力

- **自然语言输入**：用户用中英文描述系统，skill 自动识别图表类型、布局、风格，生成 SVG 并导出 1920px 高清 PNG。无需学习 Mermaid 语法或点击 GUI。
- **8 种视觉风格**：Style 1-7 为模板驱动（Flat Icon、Dark Terminal、Blueprint、Notion Clean、Glassmorphism、Claude Official、OpenAI Official），Style 8 (Dark Luxury) 为 AI 手工定制风格。每种风格有独立的颜色令牌和排版规范。
- **AI/Agent 领域知识**：内置 RAG Pipeline、Agentic Search、Mem0 Memory、Multi-Agent、Tool Call Flow 等常见架构模式，支持语义化图形（LLM=双线矩形、Agent=六边形、Vector Store=带环圆柱）。
- **完整 UML 支持**：支持全部 14 种 UML 图表类型，包括类图、组件图、部署图、包图、时序图、状态机图等。

### 工作流程

1. **识别意图**：skill 触发后解析用户描述，识别图表类型（架构图、流程图、时序图等）和目标风格。
2. **加载参考资源**：从 `references/` 目录加载对应风格的颜色令牌、形状规范、模板示例。
3. **生成 SVG**：基于语义化形状词汇和箭头系统，生成结构化的 SVG 图表。
4. **导出 PNG**：使用 cairosvg（推荐）/ rsvg-convert / puppeteer 将 SVG 渲染为 1920px 高清 PNG。
5. **输出文件**：返回 SVG 文件（可编辑）和 PNG 文件（可直接嵌入文档）。

### 内置资源

| 资源类型 | 路径 | 用途 |
| --- | --- | --- |
| `SKILL.md` | `SKILL.md` | 核心 skill 定义：图表类型、布局规则、形状词汇、触发条件 |
| 风格参考 | `references/style-*.md` | 8 种视觉风格的详细规范：颜色令牌、SVG 模式、模板 |
| 图标库 | `references/icons.md` | 40+ 产品图标（OpenAI、Anthropic、Pinecone、Kafka 等） |
| 模板文件 | `templates/*.svg` | 各类图表的起始模板 |
| 示例样本 | `fixtures/*.json` | 回归测试用的样式样本 |
| 导出脚本 | `scripts/*.sh` | SVG 验证、PNG 导出、批量测试脚本 |

### 输入与输出

| 类型 | 说明 |
| --- | --- |
| 输入 | 自然语言描述（中英文），可指定风格、输出路径 |
| 输出 | SVG 文件（矢量，可编辑）+ PNG 文件（1920px 高清，可直接使用） |
| 副作用 | 会在指定目录创建文件，需要 cairosvg/rsvg-convert/puppeteer 等渲染工具 |

## 安装方法

### 前置条件

- **运行环境**：Python 3.x（用于 cairosvg）或 Node.js（用于 puppeteer）
- **PNG 渲染器**（三选一）：
  - cairosvg（推荐）：`pip install cairosvg`
  - rsvg-convert：macOS `brew install librsvg`，Ubuntu `sudo apt install librsvg2-bin`
  - puppeteer：`npm install puppeteer`（约 150MB Chromium）
- **平台**：Windows / macOS / Linux

### 安装步骤

1. 确认来源地址：

   ```text
   GitHub 仓库：https://github.com/yizhiyanhua-ai/fireworks-tech-graph
   npm 包：@yizhiyanhua-ai/fireworks-tech-graph
   ```

2. 使用 skills 命令安装：

   ```bash
   npx skills add yizhiyanhua-ai/fireworks-tech-graph
   ```

3. 或直接克隆到 skills 目录：

   ```bash
   git clone https://github.com/yizhiyanhua-ai/fireworks-tech-graph.git ~/.claude/skills/fireworks-tech-graph
   ```

4. 确认目录结构：

   ```text
   fireworks-tech-graph/
   ├── SKILL.md
   ├── agents/
   │   └── openai.yaml
   ├── references/
   │   ├── style-1-flat-icon.md
   │   ├── style-2-dark-terminal.md
   │   ├── ...
   │   └── icons.md
   ├── scripts/
   │   ├── generate-diagram.sh
   │   └── validate-svg.sh
   ├── templates/
   └── assets/
       └── samples/
   ```

5. 重启或刷新 AI 助手，使 skill 元数据重新加载。

### 安装验证

验证渲染器已安装：

```bash
python3 -c "import cairosvg; print(cairosvg.__version__)"
# 或
rsvg-convert --version
```

预期结果：显示版本号即表示安装成功。

## 使用方法

### 触发方式

用户可以通过以下方式触发该 skill：

- **明确点名**：`使用 fireworks-tech-graph 画一个架构图`
- **描述任务**：`生成一个 RAG 流程图`、`画一个微服务架构图`、`创建一个时序图`
- **指定风格**：`用 dark terminal 风格画一个 Agent 架构图`

### 使用示例

#### 示例 1：生成 RAG 流程图

用户请求：

```text
Draw a RAG pipeline flowchart
```

预期行为：

```text
skill 识别为 Data Flow Diagram，使用默认 Style 1 (Flat Icon)
生成包含 Query → Embed → VectorSearch → Retrieve → LLM → Response 流程的 SVG
导出 1920px PNG
输出：rag-pipeline.svg / rag-pipeline.png
```

#### 示例 2：生成 Mem0 架构图（指定风格）

用户请求：

```text
Generate a Mem0 memory architecture diagram, dark style
```

预期行为：

```text
skill 识别为 Memory Architecture Diagram，使用 Style 2 (Dark Terminal)
生成包含 Input Layer、Memory Manager、Storage Layer、Output/Retrieval 四层的 SVG
使用语义化形状：Vector Store = 带环圆柱、Graph DB = 三圆簇
输出：mem0-architecture.svg / mem0-architecture.png
```

#### 示例 3：生成多智能体协作图

用户请求：

```text
Draw a Multi-Agent diagram: Orchestrator dispatches 3 SubAgents (search / compute / code execution), results aggregated
```

预期行为：

```text
skill 识别为 Agent Architecture Diagram
生成包含 Orchestrator（六边形）和三个 SubAgent 的协作流程图
使用语义化箭头表示委托和数据流
输出：multi-agent.svg / multi-agent.png
```

## 配置说明

| 配置项 | 是否必需 | 默认值 | 说明 |
| --- | --- | --- | --- |
| PNG 渲染器 | 是 | cairosvg | 可选 rsvg-convert 或 puppeteer |
| 输出目录 | 否 | 当前目录 | 可通过 `--output` 参数指定 |
| 风格选择 | 否 | Style 1 | 可通过 `--style` 或描述中指定 |

## 常见问题

### PNG 生成失败或空白

**原因**：未安装渲染器，或 SVG 中包含外部字体链接。

**解决**：安装 cairosvg（`pip install cairosvg`），确保 SVG 使用系统字体栈而非 `@import url()`。

### 文字或边框在 PNG 中缺失

**原因**：rsvg-convert 对 CSS 和 `<foreignObject>` 支持有限。

**解决**：切换到 cairosvg 渲染器，CSS 支持更好。

### 图表被截断

**原因**：SVG viewBox 高度设置过小。

**解决**：增加 `viewBox` 中的 height 值。

## 风险与限制

- 需要安装本地渲染器（cairosvg/rsvg-convert/puppeteer），不同渲染器的 CSS 支持程度不同
- 输出为静态图表，不支持交互或动画
- 对于超复杂系统图，建议拆分为多个子图以提高可读性
- Style 8 (Dark Luxury) 为 AI 手工生成，输出一致性略低于模板驱动的 Style 1-7

## 维护与更新

更新到最新版本：

```bash
npx skills add yizhiyanhua-ai/fireworks-tech-graph --force -g -y
```

或重新克隆仓库：

```bash
cd ~/.claude/skills/fireworks-tech-graph
git pull origin main
```

## 参考链接

- GitHub 仓库：https://github.com/yizhiyanhua-ai/fireworks-tech-graph
- npm 包页面：https://www.npmjs.com/package/@yizhiyanhua-ai/fireworks-tech-graph
- 官方案例：https://bradzhang.dev/en/case-studies/fireworks-tech-graph
- 维护者主页：https://bradzhang.dev/en
