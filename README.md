# AGENTSmd

给 AI 编程助手用的中文协作规范。复制进项目就能用，不绑定语言、框架或平台。

它要解决三件事：

- 工作稳定：先查证再动手，改动范围可控，结果如实汇报。
- 持续迭代：每次任务的经验都能写回文档，文档随项目一起长，规则不重复、不过期。
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
| [docs/agents/](docs/agents/) | 按主题拆分的专题，任务涉及时读取；项目可以继续新增 |
| [templates/PROJECT_CONTEXT.md](templates/PROJECT_CONTEXT.md) | 项目事实模板：术语、目录、命令、约定、关键约束、改动路由、经验 |
| [prompts/ADOPT.md](prompts/ADOPT.md) | 让 AI 把本规范接入项目的提示词，接入时用一次 |

## 文档怎样跟着项目成长

刚接入时，文档里只有通用规则。之后每次任务，AI 都会把查明的原因、确认的约束和你纠正过的做法写回文档，按这条路径逐级升级：

1. 第一次遇到的坑，记进 `PROJECT_CONTEXT.md` 的「已知问题与经验」。
2. 同类问题再次出现，升级为「关键约束」，写成「做法加后果」。
3. 需要展开说明，或同一主题积累了好几条约束，写成专题：已有专题写在末尾的「本项目补充」，新主题在 `docs/agents/` 下新建文件，并登记到路由。
4. 原因不再成立的约束直接删掉，文档只写现状。

几个月后，`PROJECT_CONTEXT.md` 会变成项目的术语表、结构地图和关键约束清单，`docs/agents/` 里会多出项目自己的专题（比如支付流程、同步协议、设计系统）。完整规则见 [文档维护与演进](docs/agents/documentation.md)。

需要时，可以直接对 AI 说：

```text
把这次对话里值得留下的经验、约束和我纠正过的做法，按文档维护的规则写进文档。
```

```text
按文档维护的「定期体检」整理一遍文档：对照代码核实，删掉过期的，合并重复的，过长的拆成专题。
```

```text
通用规范有新版本，在 <新版本路径>。按文档维护的「升级通用规范」合并进来，保留项目自己的内容。
```

## 维护本仓库

本仓库只有 Markdown，没有构建和测试。修改后检查：

- 链接有效，路由表与 `docs/agents/` 中的文件一一对应；
- 规则之间不矛盾，同一条规则只写在一处；
- 不出现具体项目的名称、路径、常量或业务规则。

新增规则前，先按 [文档维护与演进](docs/agents/documentation.md) 里的筛选条件过一遍。各项目里验证过、去掉项目细节后仍然成立的规则，欢迎合并回来。
