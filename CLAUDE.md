# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

这是一个个人 Claude Code Skills 仓库，用于存放自定义的 skills 以扩展 Claude 的能力。

## 仓库结构

```
skillhub/
├── CLAUDE.md          # 本文件，项目说明
├── README.md          # 仓库介绍
└── skills/            # 所有 skill 存放目录
    └── <skill-name>/  # 每个 skill 独立目录
        ├── SKILL.md   # 必需，skill 定义文件
        ├── <skill-name>.skill  # 打包后的分发文件
        ├── scripts/   # 可选，可执行脚本
        ├── references/# 可选，参考文档
        └── assets/    # 可选，资源文件（模板、图片等）
```

重要规则：
- 所有 skill 相关文件必须放在 `skills/<skill-name>/` 目录下
- 打包生成的 `.skill` 文件也放在对应 skill 目录内，不要放在仓库根目录或 skills 根目录
- 新创建的 skill 完成后，必须更新 README.md 添加该 skill 的介绍

## 创建新 Skill

在对话中描述创建 skill 的需求（如 "帮我创建一个 skill"），Claude 会自动加载 skill-creator 引导创建流程。生成的目录放入 `skills/` 文件夹。

## Skill 文件格式

每个 SKILL.md 需包含：
1. YAML frontmatter（`name` 和 `description` 字段）
2. Markdown 格式的指令内容
