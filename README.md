# refactoring2-skill

一个面向 Agent 的代码重构 skill，将 Martin Fowler《重构：改善既有代码的设计（第 2 版）》蒸馏为可执行工作流：识别代码异味、选择重构手法、用测试建立安全边界，并通过小步修改保持外部行为不变。

> “在不改变代码外在行为的前提下，对代码做出修改，以改进程序的内部结构。”
>
> —— Martin Fowler，《重构（第 2 版）》[中文版原文：什么是重构](https://github.com/NxeedGoto/Refactoring2-zh/blob/master/docs/README.md#%E4%BB%80%E4%B9%88%E6%98%AF%E9%87%8D%E6%9E%84)

## 包含内容

- `refactoring2/SKILL.md`：任务路由、安全边界、小步重构闭环与完成标准。
- `refactoring2/references/code-smells.md`：24 种代码异味到候选手法的决策表。
- `refactoring2/references/catalog.md`：按主题组织的 61 项重构手法速查表。
- `refactoring2/references/operating-guide.md`：遗留代码、数据库、共享 API、性能与并发场景的额外护栏。
- `refactoring2/references/source-map.md`：技能内容与原文章节的对应关系。

## 安装

将 `refactoring2` 目录复制到 Agent 运行环境所使用的 skills 目录。具体位置取决于运行环境；安装后应保持以下结构：

```text
skills/
└── refactoring2/
    ├── SKILL.md
    ├── agents/
    └── references/
```

## 使用示例

```text
Use $refactoring2 to review this module, identify the highest-value smell,
and refactor it in small behavior-preserving steps.
```

也可以用中文：

```text
使用 $refactoring2 检查这段代码，先说明最值得处理的代码异味，
再通过小步、可验证的修改完成重构，不改变外部行为。
```

## 原文与致谢

本项目是面向 Agent 的原创摘要与操作化改写，不包含原书示例代码，也不替代原书。原文请参阅上游仓库：[NxeedGoto/Refactoring2-zh](https://github.com/NxeedGoto/Refactoring2-zh)。

## License

本仓库中的原创 skill 指令与摘要采用 MIT License。书名、原书内容及相关权利归各自权利人所有。
