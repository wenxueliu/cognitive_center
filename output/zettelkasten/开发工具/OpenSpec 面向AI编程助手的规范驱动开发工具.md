---
title: OpenSpec 面向AI编程助手的规范驱动开发工具
type: entity
permalink: output/zettelkasten/开发工具/open-spec-面向-ai-编程助手的规范驱动开发工具
tags:
- 开发工具
- AI辅助
- 规范驱动
- 项目管理
---

# OpenSpec 面向AI编程助手的规范驱动开发工具

## 概述

OpenSpec 是一种规范驱动开发（Spec-Driven Development）方法，专为 AI 编程助手设计。它让你和 AI 在编写任何代码之前就对"要构建什么"达成一致，无需 API 密钥。

## 核心价值

- **提前对齐规范**：人类与 AI 利益相关者在开发开始前就规范达成一致
- **结构化变更管理**：结构化的变更文件夹（提案、任务、规范更新）使范围明确且可审计
- **共享可见性**：清晰了解哪些变更处于"提案"、"活跃"或"已归档"状态
- **兼容性**：兼容你已在使用的 AI 工具：支持原生斜杠命令的工具可直接使用；其他工具则通过上下文规则集成

## 架构特点

### 双文件夹模型
- `openspec/specs/`：当前的事实源（已批准的规范）
- `openspec/changes/`：提议的更新（待评审的变更）

### 变更驱动设计
- **面向存量项目**：不仅适用于从零到一（0→1）的新功能，更擅长处理对已有行为的修改（1→n）
- **变更追踪**：提案、任务和规范增量（delta）集中存放
- **归档操作**：已批准的更新合并回规范源

## 工作流程

1. **起草变更提案**：描述你希望更新的规范内容
2. **评审与对齐**：反复迭代，直到人类与 AI 对规范达成一致
3. **执行任务**：基于已批准的规范，由 AI 实现具体任务
4. **归档变更**：将已批准的更新合并回 openspec/specs/，成为新的事实源

## 支持的AI工具

### 原生斜杠命令支持
- Claude Code
- Cursor
- Factory Droid
- OpenCode
- Kilo Code
- Windsurf
- Codex
- GitHub Copilot
- Amazon Q Developer
- Auggie (Augment CLI)

### AGENTS.md 兼容
- Amp • Jules • Gemini CLI • 其他工具

## 安装与初始化

### 前提条件
Node.js >= 20.19.0

### 安装步骤
```bash
# 全局安装 CLI
npm install -g @fission-ai/openspec@latest

# 项目初始化
openspec init
```

## 核心命令

```bash
openspec list                    # 查看活跃的变更文件夹
openspec view                    # 交互式仪表盘，展示规范与变更
openspec show <change>           # 显示变更详情（提案、任务、规范更新）
openspec validate <change>       # 检查规范格式与结构
openspec archive <change>        # 将已完成的变更移入归档
```

## 文件格式

### 增量（Delta）格式
- `## ADDED Requirements`：新增功能
- `## MODIFIED Requirements`：行为变更（需包含完整更新后的文本）
- `## REMOVED Requirements`：已弃用的功能

### 格式要求
- 使用 `### Requirement: <名称>` 作为标题
- 每个需求必须至少包含一个 `#### Scenario:` 块
- 需求文本中使用 SHALL 或 MUST

## 与其他方案对比

### vs. spec-kit
- OpenSpec 的双文件夹模型将状态与差异分离
- 在修改现有功能或跨多个规范更新时更具扩展性
- spec-kit 在全新项目（0→1）中表现优秀

### vs. Kiro.dev
- OpenSpec 将每个功能的所有变更集中在一个文件夹中
- Kiro 将更新分散在多个规范文件夹中，可能导致功能追踪困难

### vs. 无规范开发
- 没有规范时，AI 编程助手仅凭模糊提示生成代码
- OpenSpec 通过在编码前对行为达成一致，带来可预测性

## 团队采用建议

1. **初始化 OpenSpec**：在仓库中运行 `openspec init`
2. **从新功能开始**：要求 AI 将新工作以变更提案形式捕获
3. **渐进式演进**：每次变更归档后，都会更新为"活文档"
4. **保持灵活性**：不同成员可使用不同的 AI 工具，同时共享同一套规范

## 使用示例

### 创建变更示例
当你要求 AI 助手"添加双因素认证（2FA）"时，它会自动生成以下结构：

```
openspec/
├── specs/
│   └── auth/
│       └── spec.md          # 当前认证规范
└── changes/
    └── add-2fa/             # AI 自动生成整个结构
        ├── proposal.md       # 变更原因与内容
        ├── tasks.md          # 实现清单
        ├── design.md         # 技术决策（可选）
        └── specs/
            └── auth/
                └── spec.md   # 规范增量（delta）
```

## 技术特点

- **轻量级**：流程简单、无需 API 密钥、设置极少
- **开源**：MIT License，GitHub 官方开源项目
- **标准化**：遵循 Conventional Commits 规范
- **可扩展**：支持自定义工作流和集成


## 参考
https://artisan.blog.csdn.net/article/details/153654303