# Specs 目录结构示例

```
specs/
├── arch/
│   ├── design.md          # 架构设计文档
│   └── rule.md            # 架构规则文档
└── feat/
    ├── feat_001_user_auth/      # 用户认证特性
    │   ├── design.md            # 特性设计文档
    │   └── rule.md              # 特性规则文档
    ├── feat_002_data_sync/      # 数据同步特性
    │   ├── design.md
    │   └── rule.md
    ├── feat_003_notification/   # 通知系统特性
    │   ├── design.md
    │   └── rule.md
    └── feat_004_analytics/      # 数据分析特性
        ├── design.md
        └── rule.md
```

## 目录说明

### arch 目录
存放架构相关的文档：
- `design.md` - 整体架构设计说明
- `rule.md` - 架构层面的约束和规则

### feat 目录
存放各功能特性的文档，子目录命名规则：`feat_{index}_{feat_name}`

- `{index}` - 三位数字编号，从 001 开始递增
- `{feat_name}` - 特性名称，使用下划线分隔单词

每个特性子目录包含：
- `design.md` - 该特性的设计文档
- `rule.md` - 该特性的业务规则和约束
