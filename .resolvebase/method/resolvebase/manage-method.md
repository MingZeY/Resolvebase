# 管理方法文件

## 输入
- `操作类型`：新增 / 修改 / 删除
- `分类模块`：所属分类模块名
- `文件名`：不含 `.md`
- `文件内容`（新增/修改时）：符合 [[method/resolvebase/method_grammar_check]] 的方法描述

## 输出
- 操作完成：文件已变更 + [[define/resolvebase/index|索引]]已同步
- 或：操作被拒绝 + 原因

## 过程

### 新增

1. 通过 [[method/resolvebase/lookup]] 查 `method/<分类模块>/<文件名>.md` 是否已存在。若存在 → 拒绝，返回"文件名重复"。
2. 通过 [[method/resolvebase/lookup]] 查 `<分类模块>` 是否存在。若不存在 → 按 [[method/resolvebase/manage-resolvebase]] 判断是否新建。
3. 通过 [[method/resolvebase/method_grammar_check]] 校验 `文件内容`。不通过 → 拒绝并附违规列表。
4. 创建文件，写入内容。
5. 通过 [[method/resolvebase/manage-index]] 在子索引追加条目。

### 修改

1. 通过 [[method/resolvebase/lookup]] 查目标是否存在。不存在 → 拒绝。
2. 读取当前内容。若修改了输入/输出 → 搜索 `.resolvebase` 找到所有调用方，评估兼容性。
3. 通过 [[method/resolvebase/method_grammar_check]] 校验修改后内容。不通过 → 拒绝。
4. 核心逻辑根本变化 → 考虑新建而非覆盖。
5. 写入。
6. 通过 [[method/resolvebase/manage-index]] 更新索引 `description`。

### 删除

1. 通过 [[method/resolvebase/lookup]] 查目标是否存在。不存在 → 拒绝。
2. 搜索 `.resolvebase` 确认无引用。被引用 → 先解除引用或拒绝。
3. 删除文件。
4. 通过 [[method/resolvebase/manage-index]] 移除索引条目。
