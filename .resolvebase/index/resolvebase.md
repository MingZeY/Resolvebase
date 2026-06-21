# Define
description: resolvebase 的定义文件索引

## define.md
description: 定义文件概念：不可变共享知识单元
link: [[define/resolvebase/define]]
## method.md
description: 方法文件概念：可复用操作流程，输入→过程→输出
link: [[define/resolvebase/method]]
## state.md
description: 状态文件概念：运行时快照
link: [[define/resolvebase/state]]
## index.md
description: 索引概念：层级目录系统，定位定义/方法/状态文件
link: [[define/resolvebase/index]]
## index-l1.md
description: 一级索引概念：唯一主入口，仅引用二级索引
link: [[define/resolvebase/index-l1]]
## index-l2.md
description: 二级索引概念：管理某类目下全部定义/方法/状态条目
link: [[define/resolvebase/index-l2]]
## link-syntax.md
description: 链接语法规则：\[[path|display]] 格式，管道符分隔，锚点可选
link: [[define/resolvebase/link-syntax]]
## file-naming.md
description: 文件命名规则：用户空间遵循语言习惯，系统文件英文命名，系统文件修改须先警告用户
link: [[define/resolvebase/file-naming]]

# Method
description: resolvebase 的方法文件索引

## manage-resolvebase.md
description: 总入口：路由操作到子方法，管理分类模块
link: [[method/resolvebase/manage-resolvebase]]
## manage-define.md
description: 管理定义文件的增/删/改
link: [[method/resolvebase/manage-define]]
require: [[method/resolvebase/manage-resolvebase]], [[method/resolvebase/define_grammar_check]]
## manage-method.md
description: 管理方法文件的增/删/改
link: [[method/resolvebase/manage-method]]
require: [[method/resolvebase/manage-resolvebase]], [[method/resolvebase/method_grammar_check]]
## manage-state.md
description: 管理状态文件的新增/更新/归档
link: [[method/resolvebase/manage-state]]
require: [[method/resolvebase/manage-resolvebase]], [[method/resolvebase/state_grammar_check]]
## manage-index.md
description: 管理索引条目与类目的增/删/改/拆分，遵循索引层级规则
link: [[method/resolvebase/manage-index]]
require: [[method/resolvebase/manage-resolvebase]], [[method/resolvebase/index_grammar_check]], [[define/resolvebase/index]], [[define/resolvebase/index-l1]], [[define/resolvebase/index-l2]]
## lookup.md
description: 通过索引链+关键字搜索查找条目，解析 require
link: [[method/resolvebase/lookup]]
require: [[method/resolvebase/manage-resolvebase]], [[method/resolvebase/manage-index]]
## execution-protocol.md
description: 执行协议：宣告方法名称，使用 TodoWrite 跟踪步骤，支持子方法展开与纯文本 TODO 降级
link: [[method/resolvebase/execution-protocol]]
require: [[method/resolvebase/manage-resolvebase]]
## method_grammar_check.md
description: 校验方法文件语法：四段式、编号步骤、合法 link
link: [[method/resolvebase/method_grammar_check]]
require: [[method/resolvebase/manage-resolvebase]], [[method/resolvebase/lookup]]
## define_grammar_check.md
description: 校验定义文件语法：断言式、单概念、link 仅限 define/
link: [[method/resolvebase/define_grammar_check]]
require: [[method/resolvebase/manage-resolvebase]], [[method/resolvebase/lookup]]
## state_grammar_check.md
description: 校验状态文件语法：可验证快照、ISO日志、合法 link
link: [[method/resolvebase/state_grammar_check]]
require: [[method/resolvebase/manage-resolvebase]], [[method/resolvebase/lookup]]
## index_grammar_check.md
description: 校验索引文件语法：条目完整、类型分组、无死链、主入口可达、层级合规
link: [[method/resolvebase/index_grammar_check]]
require: [[method/resolvebase/manage-resolvebase]], [[method/resolvebase/lookup]], [[define/resolvebase/index]], [[define/resolvebase/index-l1]], [[define/resolvebase/index-l2]]

# State
description: resolvebase 的状态文件索引
