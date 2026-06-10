# Excalidraw Diagram Skill 介绍

## 基础信息

| 项目 | 内容 |
| --- | --- |
| Skill 名称 | `excalidraw-diagram` |
| 显示名称 | Excalidraw Diagram Skill |
| 所属分类 | 开发工具 / 文档处理 |
| 适用平台 | Claude Code / OpenCode / 任何支持 skills 的编码代理 |
| 当前版本 | main 分支 |
| 维护者 | coleam00 |
| 来源 | 第三方开源项目 |
| GitHub 仓库 | https://github.com/coleam00/excalidraw-diagram-skill |
| 其他来源链接 | 不适用 |
| 许可证 | 未指定 |
| 更新时间 | 2026-06-10 |

## 简介

`excalidraw-diagram` 是一个用于从自然语言描述生成美观实用的 Excalidraw 图表的 skill。它适合在需要可视化架构、流程、数据流等场景中使用，可以帮助编码代理生成具有视觉论证能力的图表，而非简单的方框箭头图。

## 适用场景

- 需要将系统架构、数据流、时序图等概念可视化为图表
- 创建技术文档时需要配套的示意图
- 需要生成带有真实代码片段和 JSON 负载的技术图表
- 希望图表样式符合品牌定制化需求

## 不适用场景

- 需要复杂 3D 渲染或动画效果的可视化
- 实时协作绘图（该 skill 仅生成静态图表）
- 需要高度定制化矢量图形设计的场景

## 详细功能介绍

### 核心能力

- **视觉论证设计**：每个形状/形状组都反映其所代表的概念——一对多用扇形展开，序列用时间线，聚合用收敛布局，而非统一的卡片网格。
- **证据产物嵌入**：技术图表可包含真实代码片段和实际 JSON 负载，增强图表的信息密度和实用性。
- **内置视觉验证**：基于 Playwright 的渲染管线让代理能够查看自己的输出，捕获布局问题（文本重叠、箭头错位、间距不均），并在交付前循环修复。

### 工作流程

1. 解析用户的自然语言描述，提取核心概念和关系
2. 根据概念特性选择合适的视觉表达方式（扇形、时间线、收敛等）
3. 生成符合 Excalidraw JSON 格式的图表数据
4. 通过渲染管线生成 PNG 预览，检测布局问题
5. 迭代修复问题，最终交付图表文件

### 内置资源

| 资源类型 | 路径 | 用途 |
| --- | --- | --- |
| `SKILL.md` | `SKILL.md` | 设计方法论和工作流程说明 |
| 颜色配置 | `references/color-palette.md` | 品牌颜色配置（可自定义） |
| 元素模板 | `references/element-templates.md` | 各类元素的 JSON 模板 |
| JSON Schema | `references/json-schema.md` | Excalidraw JSON 格式参考 |
| 渲染脚本 | `references/render_excalidraw.py` | 将 .excalidraw 渲染为 PNG |
| Python 依赖 | `references/pyproject.toml` | Python 依赖配置（playwright） |

### 输入与输出

| 类型 | 说明 |
| --- | --- |
| 输入 | 自然语言描述的图表需求 |
| 输出 | Excalidraw JSON 文件和 PNG 预览图 |
| 副作用 | 会启动 Playwright 浏览器进行渲染 |

## 安装方法

### 前置条件

- Python 环境（用于渲染管线）
- uv 包管理器
- Playwright（用于视觉验证）

### 安装步骤

1. 确认来源地址：

   ```text
   GitHub 仓库：https://github.com/coleam00/excalidraw-diagram-skill
   ```

2. 获取 skill：

   ```bash
   git clone https://github.com/coleam00/excalidraw-diagram-skill.git
   ```

3. 放置到 Claude Code skills 目录：

   ```bash
   cp -r excalidraw-diagram-skill .claude/skills/excalidraw-diagram
   ```

4. 确认目录结构：

   ```text
   excalidraw-diagram/
   |-- SKILL.md
   `-- references/
       |-- color-palette.md
       |-- element-templates.md
       |-- json-schema.md
       |-- render_excalidraw.py
       |-- render_template.html
       `-- pyproject.toml
   ```

5. 设置渲染管线：

   ```bash
   cd .claude/skills/excalidraw-diagram/references
   uv sync
   uv run playwright install chromium
   ```

### 安装验证

重启 Claude Code 后，尝试请求生成一个简单图表，检查是否正常触发 skill。

## 使用方法

### 触发方式

用户可以通过以下方式触发该 skill：

- 描述任务：「创建一个 Excalidraw 图表，展示...」
- 明确点名：「使用 excalidraw-diagram 生成...」

### 使用示例

#### 示例 1：架构图

用户请求：

```text
创建一个 Excalidraw 图表，展示 AG-UI 协议如何将事件从 AI 代理流式传输到前端 UI
```

预期行为：

```text
Claude Code 将解析架构关系，生成包含数据流向、组件关系的 Excalidraw 图表，
并通过渲染管线验证布局，最终交付 .excalidraw 文件和 PNG 预览。
```

#### 示例 2：品牌定制图表

用户请求：

```text
使用公司品牌颜色生成一个微服务架构图
```

预期行为：

```text
Claude Code 将读取 color-palette.md 中的品牌配置，生成符合品牌视觉风格的图表。
用户可预先编辑该文件以自定义颜色方案。
```

## 配置说明

| 配置项 | 是否必需 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `color-palette.md` | 否 | 内置配色 | 修改此文件可自定义所有图表的颜色方案 |

## 常见问题

### 渲染失败怎么办？

确保已正确安装 Playwright 和 chromium 浏览器。运行：
```bash
cd .claude/skills/excalidraw-diagram/references
uv run playwright install chromium
```

### 如何自定义颜色？

编辑 `references/color-palette.md` 文件，替换为你品牌的颜色配置。所有后续生成的图表都会使用新配色。

## 风险与限制

- 渲染管线需要安装 Playwright，会增加约 200MB 的依赖
- 复杂图表可能需要多次迭代才能达到理想布局
- 当前不支持实时协作功能

## 维护与更新

- 更新颜色配置时，只需修改 `references/color-palette.md`
- 如需更新整个 skill，重新从 GitHub 拉取最新版本即可

## 参考链接

- GitHub 仓库：https://github.com/coleam00/excalidraw-diagram-skill
- Excalidraw 官网：https://excalidraw.com
- Claude Code 文档：https://docs.anthropic.com/en/docs/claude-code
