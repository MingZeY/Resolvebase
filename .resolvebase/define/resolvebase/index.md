# 索引

## 本质

索引文件是 Resolvebase 空间中的目录系统，用于快速定位 [[define/resolvebase/define|定义]]、[[define/resolvebase/method|方法]]和 [[define/resolvebase/state|状态]]文件的位置。索引不包含知识内容本身，只维护条目到文件路径的映射。

## 核心特征

- **层级结构**：索引系统分为 [[define/resolvebase/index-l1|一级索引]]和 [[define/resolvebase/index-l2|二级索引]]两层。
- **导航入口**：从 `index/index.md` 出发，沿引用链可到达所有已索引的文件。
- **类型分组**：二级索引按 [[define/resolvebase/define|定义]] / [[define/resolvebase/method|方法]] / [[define/resolvebase/state|状态]]分组管理条目。

## 内容边界

索引文件的内容是条目列表，每个条目包含文件名、描述（`description`）和链接（`link`）。索引自身不包含知识内容，只定位知识位置。

## 引用约束

索引文件以 `[[link]]` 形式引用其他文件，但**禁止被**[[define/resolvebase/define|定义文件]]、[[define/resolvebase/method|方法文件]]和 [[define/resolvebase/state|状态文件]]反向引用。
