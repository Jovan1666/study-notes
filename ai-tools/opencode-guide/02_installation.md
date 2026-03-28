# 二、战前准备：环境搭建与部署形态

## 2.1 安装路径

建议优先使用命令行版（CLI），它具备最强的工程执行力，能够直接改代码、跑命令、执行自动化脚本。企业环境对权限控制极其敏感，在部署时应严格遵循 OpenCode 的安装目录优先级：系统首先检索 `$OPENCODE_INSTALL_DIR`，其次为 `$XDG_BIN_DIR`。

```bash
# 一键安装（YOLO 脚本）
curl -fsSL https://opencode.ai/install | bash

# 通用安装（npm）
npm install -g opencode
```

## 2.2 多形态部署方式

| 部署形态 | 核心亮点 | 适用场景 |
|------|------|------|
| CLI (命令行) | 工程执行力最强，支持并行任务处理（Session），深度集成 TUI 交互 | 核心工程落地、全项目重构、自动化脚本运行 |
| IDE 插件 (VS Code) | 极佳的即时上下文关联，支持 Alt+K 将选定代码同步至 AI 会话 | 编码过程中的即时补全、单文件小步快跑 |
| 桌面版 (App) | 图形化界面友好，可视化管理多会话，文档整理体验更佳 | 架构复盘、非技术性分析、跨项目文档管理 |
| 云端自动化 (GitHub) | 集成 GitHub Actions，支持 Issue 驱动的自动修复与 PR 生成 | 远程仓库维护、全自动 Bug 修补、流水线集成 |

## 2.3 配置文件总控中心

所有配置最终都存储在本地的 JSON 文件中。如果发现某些插件无法加载，这里是你的第一检查站：

- **Windows**：`C:\Users\用户名\.config\opencode\opencode.json`
- **macOS / Linux**：`~/.config/opencode/opencode.json`

**配置文件加载优先级（从高到低）：**

1. 远程配置 (`.well-known/opencode`)
2. 全局配置 (`~/.config/opencode/opencode.json`)
3. 自定义配置 (`OPENCODE_CONFIG` 环境变量)
4. 项目配置 (项目根目录 `opencode.json`)
5. `.opencode` 目录 (`agents`, `commands`, `plugins`)
6. 内联配置 (`OPENCODE_CONFIG_CONTENT` 环境变量)