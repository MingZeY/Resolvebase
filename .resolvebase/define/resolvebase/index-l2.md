# 二级索引

## 本质

二级索引位于 `index/<类目名>.md`，管理某个类目下的全部 [[define/resolvebase/define|定义]]、[[define/resolvebase/method|方法]]和 [[define/resolvebase/state|状态]]文件。它区别于 [[define/resolvebase/index-l1|一级索引]]，直接包含文件条目。

## 约束

- **仅含本类目条目**：只能包含 `define/<类目名>/...`、`method/<类目名>/...`、`state/<类目名>/...` 路径的文件。跨类目引用被禁止。
- **类型分组**：按 `# Define`、`# Method`、`# State` 三个分组组织条目（可为空分组，但不能缺失分组标题）。
- **条目标题格式**：`## <文件名>`。
- **条目 link 格式**：`link: [[<类型>/<类目名>/<文件名>]]`。
- **可达性**：必须可从 `index/index.md` 出发到达，否则视为孤立。

## 子索引

当二级索引条目数过多（任一分组 ≥10 条且有子领域分界）时，可拆分为子索引 `index/<类目名>-<子领域>.md`。

- 子索引是 [[define/resolvebase/index-l2|二级索引]]的延伸，同样只能包含所在类目的条目。
- 子索引必须在父二级索引中有指向条目（`link: [[index/<类目名>-<子领域>]]`），否则孤立不可达。
- 从 [[define/resolvebase/index-l1|一级索引]]出发，经二级索引→子索引的路径，必须能到达所有条目。
