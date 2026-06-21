# 管理 Resolvebase 空间

## 输入
- `操作类型`：新增 / 修改 / 删除 / 创建分类模块 / 拆分分类模块
- `操作目标`：文件路径 或 分类模块名
- `操作内容`（可选）：文件内容

## 输出
- 操作完成：文件已变更 + [[define/resolvebase/index|索引]]已同步
- 或：操作被拒绝 + 原因

## 过程

1. **系统文件保护检查**：判断 `操作目标` 是否属于 Resolvebase 系统文件（`index/*.md`、`define/resolvebase/*.md`、`method/resolvebase/*.md`、`state/resolvebase/*.md`，参见 [[define/resolvebase/file-naming#Resolvebase 系统文件命名规则|系统文件范围]]）。若是，**必须**显式提醒用户风险（修改范围、影响分析、回滚方式）并取得明确同意后方可继续。用户拒绝则终止操作。

2. 根据 `操作类型` × `操作目标` 的类型，路由到子方法：

   | 操作 | 目标类型 | 执行 |
   |---|---|---|
   | 新增/修改/删除 | [[define/resolvebase/define|定义]] | [[method/resolvebase/manage-define]] |
   | 新增/修改/删除 | [[define/resolvebase/method|方法]] | [[method/resolvebase/manage-method]] |
   | 新增/修改/归档 | [[define/resolvebase/state|状态]] | [[method/resolvebase/manage-state]] |
   | 增/改/删条目 | [[define/resolvebase/index|索引]] | [[method/resolvebase/manage-index]] |
   | 创建/拆分 | 分类模块 | 继续执行步骤 3 |

3. 创建分类模块：
   - 验证：领域边界与现有模块正交、≥2 个文件（含预期）、非一次性。不满足则拒绝。
   - 按需创建 `define/<模块>/`、`method/<模块>/`、`state/<模块>/`。
   - 通过 [[method/resolvebase/lookup]] 查 `index/<模块>.md`，不存在则创建。
   - 通过 [[method/resolvebase/manage-index]] 在根索引添加模块入口。
   - 通过 [[method/resolvebase/index_grammar_check]] 校验根索引和新建子索引。不通过 → 回滚。

4. 拆分分类模块：
   - 验证：任一类型文件 ≥10 且有子领域分界线、或语义膨胀、或引用混乱。不满足则拒绝。
   - 有触发条件但无自然分界线 → 通过 [[method/resolvebase/manage-state]] 记录为待优化项。
   - 有自然分界线 → 创建子目录，迁移文件，通过 [[method/resolvebase/manage-index]] 更新父索引并创建子索引，确保从 `index/index.md` 可达。
   - 通过 [[method/resolvebase/index_grammar_check]] 校验父索引和新建子索引。不通过 → 回滚。

5. 后置验证：每个操作完成后，确认文件变更与索引同步是原子的（全部完成或全部回滚）。
