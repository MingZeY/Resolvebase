# 文件命名规则

## 本质

文件命名规则规定 Resolvebase 空间中文件和目录的命名方式，确保名称语义清晰且符合用户的语言习惯。

## 用户空间命名规则

除 Resolvebase 系统文件的其余所有文件和目录，其命名须符合用户的语言习惯（与用户交互时使用的语言一致）。

- 若用户使用中文交互 → 文件名使用中文
- 若用户使用英文交互 → 文件名使用英文
- 目录名同理

**示例**（中文用户）：
- 正确：`define/项目架构/模块设计.md`
- 错误：`define/project-arch/module-design.md`

**原始名称保留规则**（适用于用户空间文件命名）：

尽管文件名整体应遵循用户语言习惯，但以下类型的内容在出现在中文文件名中时，**不强制翻译**，须保留其原始名称：

- **代码标识符**：方法名、变量名、类名、函数名、接口名、模块名等，直接使用源代码中的原始名称。例如：`UserService.md`、`handleClick.md`
- **学科专业术语**：许多概念在学科中被广泛接受为英文名称（如 `WebSocket`、`TCP/IP`、`OAuth2`、`RESTful`、`DFS` 等），直接使用原始术语，不强行翻译
- **文件扩展名/格式名**：如 `JSON`、`CSV`、`Markdown` 等

此规则的核心原则是：**名称是对事物的引用，翻译会破坏引用的准确性**。只有在用户明确给出了相关翻译且翻译是行业通用的情况下，才使用翻译后的名称。

**示例**（中文用户，含代码/术语）：
- 正确：`define/认证/AuthService.md` — `AuthService` 是类名，保留原样
- 正确：`define/网络/WebSocket协议.md` — `WebSocket` 是专业术语，保留原样
- 正确：`define/数据结构/BFS算法.md` — `BFS` 是术语缩写，保留原样
- 错误：`define/认证/认证服务.md` — 将类名 `AuthService` 强行翻译，丢失引用准确性

## Resolvebase 系统文件命名规则

[[index/resolvebase]](resolvebase 二级索引)的所有子孙依赖项（即从 `index/resolvebase.md` 出发通过 link/require 可到达的全部文件）必须保持英文命名。

**系统文件范围**（受保护）：
- `index/index.md` — 一级索引
- `index/resolvebase.md` — resolvebase 二级索引
- `define/resolvebase/*.md` — 所有 resolvebase 定义文件
- `method/resolvebase/*.md` — 所有 resolvebase 方法文件
- `state/resolvebase/*.md` — 所有 resolvebase 状态文件

**命名约束**：
- 文件名使用小写英文，单词间用连字符 `-` 连接
- 目录名使用小写英文
- 示例：`define_grammar_check.md`、`manage-index.md`、`index-hierarchy.md`

## 安全修改规则

### 系统文件保护

任何对 Resolvebase 系统文件（上述 [[define/resolvebase/file-naming#Resolvebase 系统文件命名规则|系统文件范围]]）的修改，无论出于何种理由（用户要求、Agent 自主决策、语法修正等），**必须**：

1. **显式提醒用户风险**：说明即将修改哪些文件、修改原因、以及修改可能带来的影响。
2. **取得用户明确同意**：用户确认后方可执行修改。用户拒绝则放弃修改。
3. **禁止绕过**：不得通过任何方式（如子 Agent、批量操作等）绕过此保护规则。

**风险说明要素**：
- 修改范围：列出所有将变更的系统文件路径
- 影响分析：说明改动如何影响 resolvebase 自身的运行逻辑
- 回滚方式：说明如何撤销本次改动

### 用户文件

非系统文件（用户空间文件）的修改不受此规则限制，按正常流程执行。
