# Code Quality Skill

一个面向 AI 编程 Agent 的轻量级代码质量 skill，用于约束代码编写、重构、代码审查、测试和完成前验证。

它的目标不是增加复杂流程，而是让 Agent 在写代码时保持基本工程纪律：先读代码、控制范围、小步修改、行为测试、审查 diff，并在声称完成前给出真实验证结果。

## 功能

`code-quality` 会引导 AI 编程 Agent：

- 修改前先阅读现有代码和项目约定
- 控制实现范围，避免顺手重构一大片
- 遵循仓库已有命名、结构、工具和测试风格
- 在保持行为不变的前提下重构代码
- 编写关注外部行为的测试，而不是绑定内部实现
- 审查 diff 中的正确性、可维护性和测试缺口
- 在声称完成前运行测试、构建、lint 或其他验证命令

这个 skill 刻意保持简洁。它的价值主要来自工作流约束，而不是依赖脚本、框架或复杂模板。

## 安装

使用 open agent skills CLI 安装：

```bash
npx skills add twinklexin/code-quality-skill --skill code-quality
```

如果只想安装到指定 Agent：

```bash
npx skills add twinklexin/code-quality-skill --skill code-quality -a codex
npx skills add twinklexin/code-quality-skill --skill code-quality -a claude-code
```

## 使用示例

在任务中显式要求 Agent 使用这个 skill：

```text
Use $code-quality to refactor this module while preserving behavior and adding focused tests.
```

```text
Use $code-quality to review this branch for correctness, maintainability, and missing tests.
```

```text
Use $code-quality to implement this bug fix, then run the relevant verification command before claiming it is complete.
```

中文也可以：

```text
请使用 $code-quality 重构这个模块，保持行为不变，并补充必要的行为测试。
```

```text
请使用 $code-quality 审查当前分支，重点检查正确性、可维护性和测试缺口。
```

## 适用场景

适合在这些任务中使用：

- 实现新功能
- 修复 bug
- 重构已有代码
- 清理难读、丑陋或重复的代码
- 审查 PR、分支或本地 diff
- 补充测试
- 要求 Agent 在完成前验证结果

不适合把它当作语言、框架或业务领域的专用规范。它提供的是通用工程质量约束；具体技术栈规范仍应以项目自己的文档、测试和工具为准。

## 仓库结构

```text
skills/
  code-quality/
    SKILL.md
    agents/
      openai.yaml
```

## 设计原则

- **先理解，再修改**：没有读过上下文就不要动代码。
- **小步前进**：每一步都应该尽量可理解、可回滚、可验证。
- **行为优先**：测试外部行为，不测试私有实现细节。
- **避免过度设计**：只有在真实降低复杂度时才添加抽象。
- **证据先于结论**：没有 fresh verification output，就不要说完成。

## 致谢

这个 skill 受到常见软件工程实践的启发，包括小步实现、重构纪律、代码审查、行为级测试和完成前验证机制，也受到 open agent skills 生态的启发。

本项目没有逐字复制上游 skill 文本。

## 许可证

本项目使用 MIT License。详见 [LICENSE](./LICENSE)。
