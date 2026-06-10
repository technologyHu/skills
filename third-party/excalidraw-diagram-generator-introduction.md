# Skill 介绍：excalidraw-diagram-generator

## 基础信息

| 项目 | 内容 |
| --- | --- |
| Skill 名称 | `excalidraw-diagram-generator` |
| 显示名称 | Excalidraw Diagram Generator |
| 所属分类 | 开发工具 / 图表生成 |
| 适用平台 | Codex / Claude Code 等 AI CLI 工具 |
| 当前版本 | awesome-copilot main 分支 |
| 维护者 | GitHub (awesome-copilot 项目) |
| 来源 | 开源项目 |
| GitHub 仓库 | https://github.com/github/awesome-copilot |
| 其他来源链接 | 不适用 |
| 许可证 | MIT |
| 更新时间 | 2026-06-10 |

## 简介

`excalidraw-diagram-generator` 是一个用于从自然语言描述生成 Excalidraw 格式图表的 skill。它适合在需要可视化流程、系统架构、实体关系或概念层次时使用，可以帮助 AI 助手快速创建专业级的图表文件，用户可直接在 Excalidraw 中打开编辑。

## 适用场景

- 用户需要创建流程图、架构图、思维导图、ER 图、类图、时序图等可视化图表
- 需要将复杂的系统设计、业务流程或数据关系以图形化方式呈现
- 希望快速生成可编辑的 `.excalidraw` JSON 文件，而非手动绘制
- 需要使用 AWS/GCP/Azure 等云服务图标创建专业的云架构图

## 不适用场景

- 需要复杂手绘效果或精细美术设计的图表
- 包含大量元素（超过 20 个）的复杂图表，建议拆分为多个子图
- 需要嵌入图片或特殊字体的场景（当前不支持）
- 需要实时协作编辑的场景（生成后需在 Excalidraw 中打开）

## 详细功能介绍

### 核心能力

- **多类型图表支持**：支持流程图、关系图、思维导图、架构图、数据流图、泳道图、类图、时序图、ER 图等 9 种图表类型，覆盖绝大多数可视化需求。
- **自然语言理解**：自动分析用户描述，识别图表类型、关键元素和关系，无需用户提供结构化输入。
- **专业图标库集成**：支持加载 Excalidraw 图标库（如 AWS/GCP/Azure 架构图标），通过 Python 脚本高效添加图标，避免大量 token 消耗。

### 工作流程

1. **理解请求**：分析用户描述，确定图表类型、关键元素和关系。
2. **提取结构化信息**：根据图表类型提取步骤、实体、分支、连接等必要信息。
3. **生成 Excalidraw JSON**：创建符合规范的 `.excalidraw` 文件，包含元素定位、样式设置和连接关系。
4. **验证与交付**：确保元素不重叠、文本可读、连接逻辑正确，并告知用户如何打开编辑。

### 内置资源

| 资源类型 | 路径 | 用途 |
| --- | --- | --- |
| `SKILL.md` | `skills/excalidraw-diagram-generator/SKILL.md` | 核心说明、触发条件和执行流程 |
| `scripts/` | `skills/excalidraw-diagram-generator/scripts/` | 包含 `split-excalidraw-library.py`、`add-icon-to-diagram.py`、`add-arrow.py` 等工具脚本 |
| `references/` | `skills/excalidraw-diagram-generator/references/` | Excalidraw JSON schema、元素类型规范 |
| `templates/` | `skills/excalidraw-diagram-generator/templates/` | 流程图、关系图、思维导图模板 |
| `libraries/` | `skills/excalidraw-diagram-generator/libraries/` | 可选的图标库目录 |

### 输入与输出

| 类型 | 说明 |
| --- | --- |
| 输入 | 自然语言描述（如"创建一个用户注册流程图"），可选的图标库配置 |
| 输出 | `.excalidraw` JSON 文件，可在 https://excalidraw.com 或 VS Code 扩展中打开 |
| 副作用 | 仅生成文件，不修改现有文件或启动服务 |

## 安装方法

### 前置条件

- Python 3.x（用于运行图标处理脚本）
- 支持 skill 机制的 AI CLI 工具（如 Codex、Claude Code）

### 安装步骤

1. 确认来源地址：

   ```text
   GitHub 仓库：https://github.com/github/awesome-copilot
   Skill 路径：skills/excalidraw-diagram-generator/
   ```

2. 获取 skill：

   ```bash
   git clone https://github.com/github/awesome-copilot.git
   ```

3. 放置到 skills 目录：

   ```bash
   cp -r awesome-copilot/skills/excalidraw-diagram-generator ~/.codex/skills/
   # 或根据所用工具的 skills 目录配置
   ```

4. 确认目录结构：

   ```text
   excalidraw-diagram-generator/
   |-- SKILL.md
   |-- scripts/
   |   |-- split-excalidraw-library.py
   |   |-- add-icon-to-diagram.py
   |   |-- add-arrow.py
   |   |-- README.md
   |   `-- .gitignore
   |-- references/
   |   |-- excalidraw-schema.md
   |   `-- element-types.md
   |-- templates/
   |   |-- flowchart-template.json
   |   |-- relationship-template.json
   |   `-- mindmap-template.json
   `-- libraries/
       `-- (可选图标库)
   ```

5. 重启或刷新 AI CLI 工具，使 skill 元数据重新加载。

### 安装验证

运行以下检查，确认 skill 文件完整：

```bash
ls -la ~/.codex/skills/excalidraw-diagram-generator/SKILL.md
python ~/.codex/skills/excalidraw-diagram-generator/scripts/add-icon-to-diagram.py --help
```

预期结果：

```text
SKILL.md 文件存在
Python 脚本可正常执行并显示帮助信息
```

## 使用方法

### 触发方式

用户可以通过以下方式触发该 skill：

- 明确点名：`使用 excalidraw-diagram-generator 创建一个流程图`
- 描述任务：`帮我画一个用户注册的流程图`、`创建一个系统架构图`、`生成一个思维导图`
- 提供相关文件：上传现有设计文档或需求说明

### 使用示例

#### 示例 1：创建流程图

用户请求：

```text
创建一个用户注册流程图，包含邮箱验证和密码设置步骤
```

预期行为：

```text
Codex 分析请求，识别为流程图类型，提取步骤：
"开始" -> "输入邮箱" -> "验证邮箱" -> "设置密码" -> "完成注册" -> "结束"
生成 user-registration-flow.excalidraw 文件，包含 6 个矩形框和 5 条连接箭头
```

#### 示例 2：创建 ER 图

用户请求：

```text
绘制 User、Post、Comment 三个实体之间的关系图
```

预期行为：

```text
Codex 识别为关系图，提取实体和关系：
- User 创建 Post (1:N)
- User 撰写 Comment (1:N)
- Post 包含 Comment (1:N)
生成 user-content-relationships.excalidraw，使用矩形表示实体，箭头表示关系并标注
```

#### 示例 3：创建 AWS 架构图（需图标库）

用户请求：

```text
创建一个 AWS 架构图，包含 Internet Gateway、VPC、ELB、EC2、RDS
```

预期行为：

```text
Codex 检查图标库是否可用：
- 如可用：使用 Python 脚本添加专业 AWS 图标
- 如不可用：提示用户配置图标库，或使用基础形状生成临时图表
生成包含标签和连接线的完整架构图
```

## 配置说明

| 配置项 | 是否必需 | 默认值 | 说明 |
| --- | --- | --- | --- |
| 图标库路径 | 否 | `libraries/` | 用于存放 `.excalidrawlib` 文件，按需配置 |
| Python 环境 | 否（推荐） | 系统默认 | 用于运行图标处理脚本，提升图标集成效率 |

### 图标库配置（可选）

如需使用专业图标库：

1. 访问 https://libraries.excalidraw.com/
2. 搜索并下载所需图标库（如 "AWS Architecture Icons"）
3. 放置到 `libraries/aws-architecture-icons/` 目录
4. 运行拆分脚本：

   ```bash
   python scripts/split-excalidraw-library.py libraries/aws-architecture-icons/
   ```

## 常见问题

### 图表元素重叠怎么办？

调整元素间距，推荐水平间距 200-300px，垂直间距 100-150px。如元素过多，建议拆分为多个子图。

### 文本显示不完整？

增加文本框宽度，或减小字体大小。推荐字体大小 16-24px 以保证可读性。

### 如何添加自定义图标？

下载 `.excalidrawlib` 文件后，使用 `scripts/split-excalidraw-library.py` 拆分为独立图标文件，即可通过脚本或手动方式集成到图表中。

## 风险与限制

- **复杂曲线简化**：自动生成的图表中，复杂曲线会被简化为直线或基本曲线
- **元素数量限制**：单个图表建议不超过 20 个元素，过多会影响清晰度
- **无自动碰撞检测**：需手动调整元素位置避免重叠
- **图标库需手动配置**：专业图标库需用户自行下载和配置

## 维护与更新

- 更新 `SKILL.md` 时，确保 frontmatter 中的 `name` 和 `description` 准确反映 skill 能力
- 修改 `scripts/` 后，建议运行示例验证脚本行为
- 新增图表类型时，同步更新模板文件和文档说明
- 图标库更新后，重新运行拆分脚本生成最新的图标索引

## 参考链接

- GitHub 仓库：https://github.com/github/awesome-copilot
- Excalidraw 官网：https://excalidraw.com
- Excalidraw 图标库：https://libraries.excalidraw.com
- Excalidraw VS Code 扩展：https://marketplace.visualstudio.com/items?itemName=excalidraw.excalidraw-vs
