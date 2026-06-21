# 一级索引

## 本质

一级索引位于 `index/index.md`，是 Resolvebase 空间的**唯一主入口**。它区别于 [[define/resolvebase/index-l2|二级索引]]，不直接管理文件条目，而是将请求路由到各二级索引。
[[define]]
## 约束

- **只能引用二级索引**：每个条目必须是 `link: [[index/<类目名>]]` 格式。不得直接引用 [[define/resolvebase/define|定义]]、[[define/resolvebase/method|方法]]或 [[define/resolvebase/state|状态]]文件。
- **禁止类型分组**：不得出现 `# Define`、`# Method`、`# State` 等分组标题。
- **条目标题格式**：`# <类目名>`。
- **类目对应**：每个类目必须存在对应的 [[define/resolvebase/index-l2|二级索引]]文件 `index/<类目名>.md`。不存在则须先创建。
- **禁止死链**：引用不存在的类目视为违规。
