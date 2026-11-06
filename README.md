# AGENTSmd

给 AI 编程助手用的中文协作规范。复制进项目就能用，不绑定语言、框架或平台。

它要解决三件事：

- 工作稳定：先查证再动手，改动范围可控，结果如实汇报。
- 持续迭代：项目事实、决策和踩过的坑有固定位置记录，规则不重复、不过期。
- 没有 AI 味：生成的界面、文案和回复不带模板腔。

## 快速开始

### 新项目

在本仓库目录下执行，把 `TARGET` 换成你的项目路径：

```bash
TARGET=~/code/my-project
cp AGENTS.md CLAUDE.md "$TARGET/"
mkdir -p "$TARGET/docs" && cp -R docs/agents "$TARGET/docs/"
cp templates/PROJECT_CONTEXT.md "$TARGET/"
```

复制完就可以开始用。如果想让 AI 根据代码填好 `PROJECT_CONTEXT.md`、删掉用不上的专题，把 [接入提示词](prompts/ADOPT.md) 发给它。

### 已有项目

项目里已经有 `AGENTS.md` 或 `CLAUDE.md` 时不要直接覆盖。把本仓库的路径告诉 AI，再发送 [接入提示词](prompts/ADOPT.md)，由它合并，原有内容会保留。

### 工具支持

- 原生读取 `AGENTS.md` 的工具（如 Codex）：不需要额外配置。
- Claude Code：读取 `CLAUDE.md`，其中的 `@AGENTS.md` 会引入正文。
- 其他工具：在它的规则入口文件里引用 `AGENTS.md`。不要复制正文，多份副本迟早会不一致。

## 文件说明

| 文件 | 作用 |
|---|---|
| [AGENTS.md](AGENTS.md) | 核心规则和专题路由，每次任务都会读 |
| [CLAUDE.md](CLAUDE.md) | Claude Code 的入口，只引用 `AGENTS.md` |
| [docs/agents/](docs/agents/) | 按主题拆分的细则，只在任务涉及时读取 |
| [templates/PROJECT_CONTEXT.md](templates/PROJECT_CONTEXT.md) | 项目事实模板：术语、目录、命令、约定、关键约束、改动路由、经验 |
| [prompts/ADOPT.md](prompts/ADOPT.md) | 让 AI 把本规范接入项目的提示词，接入时用一次 |

## 定制

- 删专题：没有界面就删 `ui-and-interaction.md`，其他同理。路由表会跳过不存在的文件，也可以顺手删掉对应的行。
- 加项目规则：写进 `PROJECT_CONTEXT.md` 或子目录的 `AGENTS.md`。通用文件尽量不改，以后更新本规范时直接替换就行。
- 大仓库：在主要模块目录放一份局部 `AGENTS.md`，只写该模块的入口、约定和注意事项。

## 维护本仓库

本仓库只有 Markdown，没有构建和测试。修改后检查：

- 链接有效，路由表与 `docs/agents/` 中的文件一一对应；
- 规则之间不矛盾，同一条规则只写在一处；
- 不出现具体项目的名称、路径、常量或业务规则。

新增规则前，先按 [文档维护](docs/agents/documentation.md) 里的筛选条件过一遍。
