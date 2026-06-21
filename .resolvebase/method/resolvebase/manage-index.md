# 管理索引文件

## 输入
- `操作类型`：添加条目 / 更新条目 / 删除条目 / 拆分子索引 / 添加类目
- `目标索引`：`index/index.md`（[[define/resolvebase/index-l1|一级索引]]）或 `index/<模块>.md`（[[define/resolvebase/index-l2|二级索引]]）
- `条目信息`：类型（[[define/resolvebase/define|定义]]/[[define/resolvebase/method|方法]]/[[define/resolvebase/state|状态]]）、description、link、require（可选）

## 输出
- 操作完成：索引已变更 + 引用链完整
- 或：操作被拒绝 + 原因

## 过程

### 添加类目

1. 通过 [[method/resolvebase/lookup]] 查一级索引中该类目是否已存在。存在 → 拒绝。
2. 创建二级索引文件 `index/<类目名>.md`，写入 Define / Method / State 空分组。
3. 在一级索引 `index/index.md` 追加条目：
   ```markdown
   # <类目名>
   description: <说明>
   link: [[index/<类目名>]]
   ```
   ⚠️ 一级索引（[[define/resolvebase/index-l1|一级索引]]）只能引用二级索引，禁止直接引用定义/方法/状态文件。
4. 通过 [[method/resolvebase/index_grammar_check]] 校验一级索引和新二级索引。不通过 → 回滚。

### 添加条目

1. 确定操作目标为一/二级索引。若为一级索引 → 拒绝（一级索引只能通过"添加类目"操作修改）。
2. 通过 [[method/resolvebase/lookup]] 查目标二级索引是否存在。不存在 → 执行"添加类目"。
3. 验证待添加条目的 link 属于本类目（`[[<类型>/<类目名>/<文件名>]]`）。跨类目 → 拒绝（二级索引仅含本类目条目）。
4. 分析目标文件过程中引用的 `[[link]]`，确定 `require` 前置依赖（若有）。
5. 在二级索引对应类型分组下追加条目：
   ```markdown
   ## <文件名>
   description: <一句话概括>
   link: [[<类型>/<类目名>/<文件名>]]
   require: [[...]], [[...]]
   ```
6. 通过 [[method/resolvebase/index_grammar_check]] 校验索引文件。不通过 → 记录违规项。
7. 检查是否触发拆分阈值（任一分组 ≥10 条且有子领域分界）。是→执行拆分。

### 更新条目

1. 通过 [[method/resolvebase/lookup]] 查目标二级索引及条目是否存在。任一不存在 → 拒绝。
2. 验证更新后的 link 仍属于本类目（`[[<类型>/<类目名>/<文件名>]]`）。跨类目变更 → 拒绝。
3. 按变更更新：标题变→改 `description`；路径变→改 `link`；依赖变→改 `require`。
4. 通过 [[method/resolvebase/index_grammar_check]] 校验更新后的索引。不通过 → 回滚。
5. 保存。

### 删除条目

1. 通过 [[method/resolvebase/lookup]] 查目标二级索引是否存在。不存在 → 拒绝。
2. 移除目标条目。
3. 分组变空 → 移除分组标题。
4. 索引全空 → 删除二级索引文件，从一级索引移除对应类目入口，返回。
5. 通过 [[method/resolvebase/index_grammar_check]] 校验变更后的索引。不通过 → 回滚。
6. 保存。

### 拆分子索引

1. 创建新子索引 `index/<类目名>-<子领域>.md`，保持 Define / Method / State 空分组结构。
2. 迁移条目到对应的子索引分组下。
3. **关键**：在父二级索引添加指向新子索引的条目，确保从 `index/index.md` 可达（子索引是二级索引延伸，须在父索引有入口，否则孤立）：
   ```markdown
   ## <子领域>
   description: <说明>
   link: [[index/<类目名>-<子领域>]]
   ```
4. 未执行步骤 3 → 新索引孤立，其中所有条目对导航不可见。
5. 通过 [[method/resolvebase/index_grammar_check]] 校验全部变更。不通过 → 回滚。
6. 保存全部。
