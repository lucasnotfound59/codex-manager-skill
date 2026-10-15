# manager

让主 agent 专注管理，让子 agent 完成项目工作。

manager 是一个中文 Codex / Agent Skill。启用后，主 agent 负责澄清目标、判断难度与风险、选择实际可用的模型和思考 effort、委派与协调、持续汇报、按证据验收。规划、代码、配置、测试、调试、集成和技术审查由执行者完成。

## 核心原则

- **纯经理职责**：主 agent 不亲自写项目代码、实施计划或其他项目交付物，小任务也交给执行者。
- **按任务路由**：分别选择模型和 effort，尊重用户要求与宿主限制，不固定使用最强模型或最高思考深度。
- **人数按需**：一个执行者足够就只用一个；不为凑人数、占满并发或制造团队感而拆分任务。
- **持续负责**：主动报告重要结果、阻塞和变化，依据实际检查与最终集成证据验收。
- **权限不扩张**：不绕过授权、环境限制或并发上限；没有可用执行者时明确报告阻塞。

完整规则见 [manager/SKILL.md](manager/SKILL.md)。

## 安装

### 让 Codex 安装

将本仓库的 GitHub 地址发给 Codex，并告诉它：

> 使用 $skill-installer，从这个仓库的 manager 目录安装 manager skill。

官方支持使用 `$skill-installer` 从其他仓库安装 skill。具体安装位置以当前安装器为准。[官方安装说明](https://learn.chatgpt.com/docs/build-skills#install-curated-skills-for-local-use)

### 手动安装到本地

下载或克隆本仓库，进入仓库根目录。以下命令适用于 macOS / Linux，已有同名目录时会停止，避免覆盖现有版本：

```sh
mkdir -p "$HOME/.agents/skills"
if [ -e "$HOME/.agents/skills/manager" ] || [ -L "$HOME/.agents/skills/manager" ]; then
  printf '%s\n' 'manager 已存在，请先检查并备份现有版本。'
else
  cp -R manager "$HOME/.agents/skills/manager"
fi
```

只供单个项目使用时，也可将 `manager` 文件夹放到项目的 `.agents/skills/manager/`。保持 `SKILL.md`、`agents/` 和 `assets/` 的相对位置。Codex 会自动检测变更；若未显示，重启 Codex。[官方本地目录说明](https://learn.chatgpt.com/docs/build-skills#where-codex-loads-local-skills)

## 使用

在 Codex CLI / IDE 中用 `/skills` 查找，或在提示中使用 `$manager`；ChatGPT 中可用 `@` 选择已安装的 skill。[官方调用说明](https://learn.chatgpt.com/docs/build-skills#how-chatgpt-and-codex-use-skills)

例如：

> 使用 $manager 完成这项任务。先评估复杂度和风险，按当前可用能力选择执行者的模型与思考 effort，再委派规划、实现、测试和审查。你负责协调、进度汇报与验收，不亲自写代码或项目计划。

适用于用户明确要求经理式协作的项目；普通问答和一般编程请求不会仅因安装本 skill 就自动改成经理模式。

## 运行条件与边界

- 宿主需提供真实可用的子 agent / 协作能力及执行环境。
- 模型、effort 档位和并发数取决于宿主实际开放的能力；skill 无法增加这些能力。
- 这是行为指导，不是强制隔离机制。实际执行仍受模型表现、工具能力及更高优先级规则约束。

## 文件

- `manager/SKILL.md`：经理式协作规则
- `manager/agents/openai.yaml`：显示信息与调用策略
- `manager/assets/icon.svg`：界面图标
