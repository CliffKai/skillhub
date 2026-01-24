---
name: autoflow-setup
description: 深度学习/机器学习项目自动化配置工具。分析项目结构，与用户交互确认环境、路径、命令等配置，生成 .autoflow/ 配置目录供 autoflow-run 使用。触发场景：(1) 用户说"帮我构建自动化运行配置"或"配置自动化流程"；(2) 需要为 ML/DL 项目创建可复现的运行环境；(3) 准备项目的自动化训练/推理/评估流程。
---

# Autoflow Setup

为深度学习/机器学习项目创建自动化运行配置，生成 `.autoflow/` 目录，供 `autoflow-run` skill 使用。

## 工作流程

### Phase 1: 项目分析

1. 扫描项目结构，识别：
   - 框架类型（PyTorch/TensorFlow/JAX 等）
   - 入口文件（train.py, main.py 等）
   - 配置文件（config.yaml, *.json 等）
   - 依赖文件（requirements.txt, environment.yaml）

2. 检查现有环境：
   - 查找 conda 环境或 venv
   - 验证 Python 版本兼容性

### Phase 2: 用户确认

逐项与用户确认以下内容（使用 AskUserQuestion 工具）：

**必须确认：**
- 项目类型（训练/推理/数据处理/混合）
- 数据集位置
- 模型位置（预训练模型/checkpoint）
- 主要运行命令

**按需确认：**
- 环境配置（如果检测到多个或没有可用环境）
- GPU 要求
- 输出目录
- 其他项目特定配置

### Phase 3: 环境准备

根据分析结果：
- 如果存在可用环境 → 记录环境信息
- 如果不存在 → 协助创建并记录

### Phase 4: 生成配置

在项目根目录创建 `.autoflow/` 目录：

```
.autoflow/
├── project.yaml      # 项目基本信息
├── env.yaml          # 环境配置
├── paths.yaml        # 路径配置
├── commands.yaml     # 运行命令
├── hardware.yaml     # 硬件要求
└── misc.yaml         # 其他配置
```

## 配置文件说明

| 文件 | 内容 |
|------|------|
| project.yaml | 项目名称、描述、类型、框架、结构 |
| env.yaml | Python 版本、环境类型/名称、依赖、激活命令 |
| paths.yaml | 数据集、模型、输出、日志等路径 |
| commands.yaml | 预处理、训练、评估、推理命令 |
| hardware.yaml | GPU/CPU/内存要求、分布式配置 |
| misc.yaml | 随机种子、外部服务、注意事项 |

## 执行步骤

1. **读取项目结构**
   ```
   使用 Glob 和 Read 工具扫描项目
   ```

2. **分析并生成问题列表**
   - 根据扫描结果确定需要用户确认的内容
   - 对于能自动检测的信息，提供默认值让用户确认

3. **与用户交互**
   - 使用 AskUserQuestion 逐步确认
   - 每次最多问 3-4 个相关问题
   - 提供检测到的默认选项

4. **处理环境**
   - 验证或创建运行环境
   - 测试关键依赖是否可用

5. **生成配置文件**
   - 从 `assets/templates/` 复制模板
   - 填充用户确认的信息
   - 写入 `.autoflow/` 目录

6. **验证配置**
   - 检查路径是否存在
   - 验证命令格式
   - 输出配置摘要供用户确认

## 模板文件

配置模板位于 `assets/templates/`：
- `project.yaml` - 项目信息模板
- `env.yaml` - 环境配置模板
- `paths.yaml` - 路径配置模板
- `commands.yaml` - 命令配置模板
- `hardware.yaml` - 硬件配置模板
- `misc.yaml` - 其他配置模板

## 注意事项

- 所有路径使用绝对路径或相对于项目根目录的路径
- 敏感信息（API keys 等）不要写入配置文件，使用环境变量引用
- 配置完成后提醒用户将 `.autoflow/` 加入 `.gitignore`（如果包含本地路径）
