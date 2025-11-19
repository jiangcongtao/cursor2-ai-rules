# Test Cursor Rules

这是一个用于测试 Cursor AI 规则系统的项目。

## 项目简介

本项目旨在测试和验证 Cursor 编辑器的规则配置功能，包括工作区级别的规则和核心规则设置。

## 项目结构

```
test-cursor-rules/
├── .cursorrules              # 工作区级别的规则配置
└── .cursor/
    └── rules/
        └── core.mdc          # 核心规则配置（始终应用）
```

## 规则说明

### `.cursorrules`

工作区级别的规则文件，包含以下规则：
- 在所有回复的末尾添加签名 "--- By Cursor AI"

### `.cursor/rules/core.mdc`

核心规则文件（`alwaysApply: true`），定义了 AI 助手的行为模式：
- 作为耐心且知识渊博的教学助手
- 系统性地解释概念，从基础原理到实际应用
- 使用清晰的示例和分步指导
- 帮助初学者通过实践学习

## 使用方法

1. 在 Cursor 编辑器中打开此项目
2. AI 助手将自动应用这些规则
3. 观察 AI 助手的行为是否符合规则定义

## 注意事项

- 规则文件遵循 Cursor 的规则配置格式
- `.cursorrules` 文件适用于整个工作区
- `.cursor/rules/core.mdc` 中的规则会始终应用（`alwaysApply: true`）

## 许可证

本项目仅用于测试目的。

