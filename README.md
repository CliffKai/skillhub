# SKILLHUB

个人 Claude Code Skills 仓库，存放自定义的 skills 以扩展 Claude 的能力。

## Skills 列表

| Skill | 描述 |
|-------|------|
| [innovation-validator](skills/innovation-validator/) | 学术创新点探索与验证工具，使用 Claude + Codex + Gemini 三工具协同检索文献、分析创新点、评估 AI 顶会发表潜力 |

## 仓库结构

```
skillhub/
├── README.md                      # 仓库介绍
├── CLAUDE_CODE_SKILLS_GUIDE.md    # Skills 使用指南
└── skills/                        # 所有自定义 skills
    └── <skill-name>/              # 单个 skill 目录
        ├── SKILL.md               # Skill 定义文件（必需）
        ├── scripts/               # 可执行脚本
        ├── references/            # 参考文档
        └── assets/                # 资源文件
```

## 快速开始

1. 使用 `/skill-creator` 创建新 skill
2. 将生成的 skill 目录放入 `skills/` 文件夹
3. 更新本 README 的 Skills 列表
