# Claude Code Skills 使用指南

## 如何使用 skill-creator

skill-creator 是一个帮助你创建 Claude Code skills 的工具。

### 调用方式

skill-creator 是自动触发的 skill，不是 slash 命令。在对话中描述创建 skill 的需求，Claude 会自动加载该 skill：

- "帮我创建一个用于代码审查的 skill"
- "我想创建一个自动生成 API 文档的 skill"
- "Create a new skill for..."

### 创建流程

1. **理解** - 收集 skill 的具体用例
2. **规划** - 确定需要的脚本、参考文档和资源
3. **初始化** - 运行 `scripts/init_skill.py <skill-name> --path <output-directory>`
4. **编辑** - 编写 SKILL.md 和相关资源
5. **打包** - 运行 `scripts/package_skill.py <path/to/skill-folder>`
6. **迭代** - 根据实际使用改进

### Skill 结构

```
skill-name/
├── SKILL.md          # 必需，包含 YAML frontmatter 和 markdown 指令
├── scripts/          # 可执行脚本
├── references/       # 参考文档
└── assets/           # 输出用的资源文件
```

## 如何查看已安装的 Skills

### 查看已安装的 plugins（包含 skills）

```bash
claude plugin list
```

### 查看已配置的 marketplaces

```bash
claude plugin marketplace list
```

### 安装新的 plugin

```bash
claude plugin install <plugin-name>@<marketplace-name>
```

例如：
```bash
claude plugin install example-skills@anthropic-agent-skills
claude plugin install document-skills@anthropic-agent-skills
```

### 常用 plugin 命令

| 命令 | 说明 |
|------|------|
| `claude plugin list` | 列出已安装的 plugins |
| `claude plugin marketplace list` | 列出已配置的 marketplaces |
| `claude plugin install <plugin>` | 安装 plugin |
| `claude plugin uninstall <plugin>` | 卸载 plugin |
| `claude plugin enable <plugin>` | 启用 plugin |
| `claude plugin disable <plugin>` | 禁用 plugin |
| `claude plugin update <plugin>` | 更新 plugin |
