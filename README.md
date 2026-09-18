# DuMate-Skills

DuMate 团队的 [Comate](https://comate.baidu.com/) Skills 集合，按能力域分类，收纳可复用的 AI 技能（Skill）。每个 Skill 都是一个自包含的目录，安装后可在 Comate 中按需触发。

## 什么是 Skill

Skill 是给 Comate 扩展专业能力的标准封装：一个 `SKILL.md`（描述何时触发、如何使用）加上可选的脚本与参考文档。Comate 会根据 `SKILL.md` 的 `description` 自动判断是否调用。

本仓库**只存放打包好的 Skill 压缩包（`.zip`）**，不放解压后的源码。每个 zip 解压后就是一个自包含的 Skill 目录：

```
<skill-name>/
├── SKILL.md            # 必需：YAML frontmatter(name, description) + 使用说明
├── scripts/            # 可选：可执行脚本（供 Skill 调用，无需装 SDK）
└── references/         # 可选：按需加载的参考文档
```

## 仓库结构

按能力域分类，新增 Skill 时把它的 zip 放进对应目录：

- `knowledge-base/` —— 知识库 / RAG：知识库增删改查、文档导入、检索问答
- `content-generation/` —— 内容生成：文档、PPT、图像、文案等
- `devops/` —— 研发工具：代码审查、流水线、卡片管理、部署
- `data-integration/` —— 数据集成：外部接口调用、数据同步、存储上传
- `productivity/` —— 效率办公：邮件、文档管理、日程、通知

> 空分类下的 `.gitkeep` 仅用于占位（Git 不跟踪空目录），放入 zip 后可删除。

### 已收录

- `knowledge-base/qianfan-knowledgebase.zip` —— 千帆 AppBuilder 知识库操作（建/查/改/删知识库、导入/上传/列/删文档、检索问答），零依赖 Node 脚本。

## 安装 Skill

Skill 分两种作用域，二选一放置：

- 个人（跨所有项目可用）：`~/.comate/skills/<skill-name>/`
- 项目（随仓库共享）：`<项目根>/.comate/skills/<skill-name>/`

> Windows 个人目录示例：`C:\Users\<用户名>\.comate\skills\<skill-name>\`
> 请勿写入 `~/.comate/skills/.system/`，该目录由 Comate 内置管理。

安装步骤：

1. 从对应分类下载目标 Skill 的 `.zip`。
2. 安装前先做安全扫描（Comate 内置 `baidu-skill-vetter`，或在安装时按提示扫描），确认无风险。
3. 解压，把解压出的 Skill 目录整个放到上面的作用域路径下。
4. 重新加载 Comate，即可在可用 Skill 列表中看到它。

## 使用

安装后无需手动调用——正常向 Comate 提出相关需求即可触发对应 Skill。若某个 Skill 依赖凭证（如 API Key），在其 `SKILL.md` 的「前置条件」里会写明如何配置（通常通过环境变量注入，凭证不落文件）。

## 贡献一个新 Skill

1. 在合适的分类目录下新建 `<skill-name>/`。
2. 写 `SKILL.md`：`name` 用短横线命名；`description` 要同时说清「做什么」和「何时触发」（触发全靠它）。
3. 需要确定性/重复性动作时，把逻辑放进 `scripts/`，让 Skill 调用而不是每次即兴生成。
4. 大段参数/模板放进 `references/`，按需加载，保持 `SKILL.md` 精简（建议 500 行内）。
5. 不要在 Skill 中写入密钥或任何敏感凭证。

## 安全

安装任何第三方 Skill 前务必先扫描、审阅其 `SKILL.md` 与脚本内容，确认没有可疑的网络外发、凭证收集或破坏性操作。来源不明的 Skill 不要直接安装。

