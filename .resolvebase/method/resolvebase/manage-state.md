# 管理状态文件

## 输入
- `操作类型`：新增 / 更新 / 归档
- `分类模块`：所属分类模块名
- `文件名`：不含 `.md`
- `状态内容`（新增/更新时）：当前状态描述 + 目标状态 + 日志条目

## 输出
- 操作完成：文件已变更 + [[define/resolvebase/index|索引]]已同步
- 或：操作被拒绝 + 原因

## 过程

### 新增

1. 通过 [[method/resolvebase/lookup]] 查 `state/<分类模块>/<文件名>.md` 是否已存在。若存在 → 拒绝，返回"文件名重复"。
2. 通过 [[method/resolvebase/lookup]] 查 `<分类模块>` 是否存在。若不存在 → 按 [[method/resolvebase/manage-resolvebase]] 判断是否新建。
3. 通过 [[method/resolvebase/state_grammar_check]] 校验 `状态内容`。不通过 → 拒绝并附违规列表。
4. 创建文件，写入内容。
5. 通过 [[method/resolvebase/manage-index]] 在子索引追加条目。

### 更新

1. 通过 [[method/resolvebase/lookup]] 查目标是否存在。不存在 → 拒绝。
2. 读取当前内容，在"日志"追加 `- [<ISO日期>] <变更描述>`（不修改历史）。
3. 更新"快照"的"更新时间"和"当前状态"。
4. 状态到达目标 → 日志追加"→ 达到目标状态"。
5. 关联变化 → 更新"关联"章节。
6. 通过 [[method/resolvebase/state_grammar_check]] 校验更新后内容。不通过 → 拒绝。
7. 写入。
8. 通过 [[method/resolvebase/manage-index]] 更新索引 `description`。

### 归档

1. 通过 [[method/resolvebase/lookup]] 查目标是否存在。不存在 → 拒绝。
2. 读取，日志追加 `- [<当前日期>] 归档：<原因>`。
3. 将文件从 `state/<分类模块>/<文件名>.md` 移至 `define/<分类模块>/<文件名>.md`（转为"已解决状态记录" [[define/resolvebase/define|定义]]）。
4. 通过 [[method/resolvebase/define_grammar_check]] 校验归档后的定义文件。不通过 → 拒绝。
5. 通过 [[method/resolvebase/manage-index]] 从状态分组移除条目，在定义分组新增条目。

> 直接删除（不归档）须确认无引用，遵循 [[method/resolvebase/manage-resolvebase]] 删除条件。
