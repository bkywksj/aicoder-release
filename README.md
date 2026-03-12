# 智码 AICoder

> 基于 Tauri 2.x 构建的 Claude Code 桌面管理工具

## 简介

智码 AICoder 是一款轻量级桌面应用，专为 Claude Code CLI 用户打造。它提供了可视化的会话管理、终端集成和开发效率工具，让你在桌面端高效使用 Claude Code 进行 AI 辅助编程。

## 核心功能

- **终端管理** — 内置 PTY 终端，直接运行 Claude Code，支持多标签页并行会话
- **会话管理** — 创建、切换、收藏会话，按项目组织工作区
- **Claude 会话浏览** — 查看 Claude Code 历史对话记录，支持搜索和导出（Markdown/HTML）
- **代码片段** — 保存常用 Prompt 和代码模板，一键插入终端
- **Token 统计** — 实时追踪 API 用量，可视化消耗统计
- **API 配置管理** — 多 API Profile 切换，支持不同密钥和端点配置
- **MCP Server 管理** — 可视化管理 Model Context Protocol 服务器配置
- **CLAUDE.md 编辑器** — 项目级和全局 CLAUDE.md 在线编辑
- **深色/浅色主题** — 跟随系统或手动切换，护眼舒适
- **系统托盘** — 最小化到托盘，常驻后台
- **自动更新** — 内置 OTA 更新，新版本自动推送

## 技术栈

| 组件 | 技术 |
|------|------|
| 框架 | Tauri 2.x（Rust + WebView） |
| 前端 | React 19 + TypeScript 5.8 |
| UI | Ant Design 6 + TailwindCSS 4 |
| 状态管理 | Zustand 5 |
| 终端 | xterm.js 6 + tauri-plugin-pty |
| 数据库 | SQLite（rusqlite） |

## 系统要求

- **操作系统**: Windows 10/11 (x64)、macOS (Apple Silicon / Intel)
- **运行时**: 无需额外安装（Windows WebView2 已内置于 Windows 10+）
- **磁盘**: ~10 MB 安装空间
- **前置**: 需已安装 [Claude Code CLI](https://docs.anthropic.com/en/docs/claude-code)

## 下载安装

### 最新版本: v1.1.4

| 平台 | 下载链接 |
|------|---------|
| Windows x64 | [AICoder_1.1.4_x64-setup.exe](releases/v1.1.4/AICoder_1.1.4_x64-setup.exe) |
| macOS Apple Silicon | [AICoder_1.1.4_aarch64.dmg](releases/v1.1.4/AICoder_1.1.4_aarch64.dmg) |
| macOS Intel | [AICoder_1.1.4_x64.dmg](releases/v1.1.4/AICoder_1.1.4_x64.dmg) |

### 安装步骤

1. 下载上方安装包
2. 双击运行安装程序
3. 选择安装语言（中文/英文）
4. 按提示完成安装
5. 启动应用，开始使用

## 更新机制

应用内置自动更新功能：

- 启动后自动检查更新（首次延迟 5 秒，之后每 30 分钟检查一次）
- 发现新版本后，右上角浮动通知显示「有可用更新」
- 点击「立即更新」按钮，自动下载并安装
- 安装完成后自动重启应用

更新清单文件: [update.json](update.json)

## 版本历史

### v1.1.4 (2026-03-12)

- 修复 macOS CLI 检测失败（重写 PATH 获取策略，支持 nvm/fnm/volta/mise/asdf 等）
- 修复 macOS 终端光标不可见
- 修复 About 页面浅色主题显示异常
- 修复新建会话标题被旧会话覆盖
- 修复多实例 MCP 配置不同步
- 修复 hasCompletedOnboarding 写入位置错误
- 新增 API 配置切换时环境变量冲突检测
- 优化设置弹窗堆叠（订阅/激活不再关闭设置）

### v1.1.3 (2026-03-12)

- 功能更新
- 新增双 GitHub CI 仓库支持（额度切换）

### v1.1.2 (2026-03-11)

- 启动时确保 hasCompletedOnboarding=true（跳过 Claude Code onboarding 交互）
- 打包产物文件名去掉中文前缀（统一为 AICoder_ 格式）

### v1.1.1 (2026-03-11)

- Rust 侧授权守门（过期状态下禁止创建会话/片段，前端无法绕过）
- HMAC-SHA256 缓存完整性校验（防篡改本地授权缓存文件）
- StatusLine 统计插件多实例隔离（支持 CLAUDE_CONFIG_DIR 环境变量）
- 可执行文件名从 tauri.exe 更名为 aicoder.exe

### v1.1.0 (2026-03-11)

- 多开实例配置隔离（每个实例独立 Claude/Codex 配置目录，支持多账号并行）
- 双击标题栏最大化/还原窗口
- 多开实例首次启动自动复制默认配置文件（解决 onboarding 问题）
- 支持自定义 shell 配置并添加 Windows PowerShell→CMD 回退机制
- 过滤非正式版本的 Codex 安装列表
- 为开发环境创建独立数据目录
- 添加窗口置顶功能

### v1.0.1 (2026-03-11)

- 修复 macOS GUI 应用找不到 npm/node 命令（PATH 环境变量补充）

### v1.0.0 (2026-03-11)

- 多提供商支持与命令优化

### v0.2.0 (2026-03-10)

- Bug 修复 + 性能优化

### v0.1.9 (2026-03-10)

- 修复右上角更新弹窗按钮无响应（改用 Modal.confirm 静态方法）
- CI 增加 macOS `.dmg` 和 Linux `.deb` 安装包下载

### v0.1.8 (2026-03-10)

- 修复 CI macOS updater 产物缺失（`--bundles dmg` → `--bundles app,dmg`）
- 优化 CI 推送顺序：Gitee 优先推送，GitHub 备份（`continue-on-error`）

### v0.1.7 (2026-03-10)

- 修复 CI 草稿 Release 权限问题（contents: read → write）

### v0.1.6 (2026-03-10)

- 修复 CI 草稿 Release 查询 404（改用 /releases 列表 API）
- 修复 Linux 编译 unused import 警告

### v0.1.5 (2026-03-10)

- CI update.json 支持全平台自动更新（Windows/macOS/Linux）
- 修复 Linux CI 签名失败（硬编码空密码）

### v0.1.4 (2026-03-10)

- 切换自动更新端点到 Gitee（解决中国大陆无法访问 GitHub raw URL）
- CI 构建后自动同步产物到 GitHub + Gitee 双仓库
- 修复更新弹窗无响应问题（z-index + 错误提示）

### v0.1.3 (2026-03-10)

- 活动热力图功能
- GitHub Actions CI 跨平台构建

### v0.1.2 (2026-03-09)

- 侧边栏重设计：按项目目录分组（替代原时间分组）
- 相对时间显示（刚刚/X分钟前/X小时前/X天前）
- 项目组折叠/展开，超过 3 条自动收起
- 收藏会话置顶独立分组
- 更新提示改为标题栏内嵌徽章

### v0.1.1 (2026-03-09)

- 优化更新提示 UI：从顶部横条改为右上角浮动通知
- 显示「有可用更新」文字，点击可直接升级
- 支持关闭通知稍后提醒
- 下载时显示进度条

### v0.1.0 (2026-03-09)

首个公开版本，包含以下功能：

- Claude Code 终端集成（PTY）
- 多会话标签页管理
- Claude 历史会话浏览和搜索
- 代码片段管理
- Token 消耗统计
- API Profile 多配置管理
- MCP Server 可视化管理
- CLAUDE.md 编辑器
- 深色/浅色主题
- 系统托盘
- 自动更新

## 项目结构

```
aicoder-release/
├── README.md           # 本文件
├── update.json         # 自动更新清单（Tauri Updater 读取）
├── .gitignore          # Git 忽略规则
└── releases/           # 版本发布目录
    ├── v0.1.0/         # v0.1.0 版本
    │   ├── 智码 AICoder_0.1.0_x64-setup.exe      # 安装包
    │   └── 智码 AICoder_0.1.0_x64-setup.exe.sig   # 签名文件
    ├── v0.1.1/         # v0.1.1 版本
    │   ├── 智码 AICoder_0.1.1_x64-setup.exe      # 安装包
    │   └── 智码 AICoder_0.1.1_x64-setup.exe.sig   # 签名文件
    ├── v0.1.2/         # v0.1.2 版本
    │   ├── 智码 AICoder_0.1.2_x64-setup.exe      # 安装包
    │   └── 智码 AICoder_0.1.2_x64-setup.exe.sig   # 签名文件
    ├── v0.1.3/         # v0.1.3 版本
    │   ├── 智码 AICoder_0.1.3_x64-setup.exe      # 安装包
    │   └── 智码 AICoder_0.1.3_x64-setup.exe.sig   # 签名文件
    ├── v0.1.4/         # v0.1.4 版本
    │   ├── 智码 AICoder_0.1.4_x64-setup.exe      # 安装包
    │   └── 智码 AICoder_0.1.4_x64-setup.exe.sig   # 签名文件
    ├── v0.1.5/         # v0.1.5 版本
    │   ├── 智码 AICoder_0.1.5_x64-setup.exe      # 安装包
    │   └── 智码 AICoder_0.1.5_x64-setup.exe.sig   # 签名文件
    ├── v0.1.6/         # v0.1.6 版本
    │   ├── 智码 AICoder_0.1.6_x64-setup.exe      # 安装包
    │   └── 智码 AICoder_0.1.6_x64-setup.exe.sig   # 签名文件
    ├── v0.1.7/         # v0.1.7 版本
    │   ├── 智码 AICoder_0.1.7_x64-setup.exe      # 安装包
    │   └── 智码 AICoder_0.1.7_x64-setup.exe.sig   # 签名文件
    ├── v0.1.8/         # v0.1.8 版本
    │   ├── 智码 AICoder_0.1.8_x64-setup.exe      # 安装包
    │   └── 智码 AICoder_0.1.8_x64-setup.exe.sig   # 签名文件
    ├── v0.1.9/         # v0.1.9 版本
    │   ├── AICoder_0.1.9_x64-setup.exe           # Windows 安装包
    │   ├── AICoder_0.1.9_aarch64.dmg             # macOS Apple Silicon
    │   ├── AICoder_0.1.9_x64.dmg                 # macOS Intel
    │   └── ...                                    # updater 签名文件
    ├── v0.2.0/         # v0.2.0 版本
    │   ├── AICoder_0.2.0_x64-setup.exe           # Windows 安装包
    │   ├── AICoder_0.2.0_x64-setup.exe.sig       # Windows updater 签名
    │   ├── AICoder_0.2.0_aarch64.dmg             # macOS Apple Silicon
    │   ├── AICoder_aarch64.app.tar.gz            # macOS ARM updater 产物
    │   ├── AICoder_aarch64.app.tar.gz.sig        # macOS ARM updater 签名
    │   ├── AICoder_0.2.0_x64.dmg                 # macOS Intel
    │   ├── AICoder_x64.app.tar.gz               # macOS Intel updater 产物
    │   └── AICoder_x64.app.tar.gz.sig           # macOS Intel updater 签名
    ├── v1.0.0/         # v1.0.0 版本
    │   ├── AICoder_1.0.0_x64-setup.exe           # Windows 安装包
    │   ├── AICoder_1.0.0_x64-setup.exe.sig       # Windows updater 签名
    │   ├── AICoder_1.0.0_aarch64.dmg             # macOS Apple Silicon
    │   ├── AICoder_aarch64.app.tar.gz            # macOS ARM updater 产物
    │   ├── AICoder_aarch64.app.tar.gz.sig        # macOS ARM updater 签名
    │   ├── AICoder_1.0.0_x64.dmg                 # macOS Intel
    │   ├── AICoder_x64.app.tar.gz               # macOS Intel updater 产物
    │   └── AICoder_x64.app.tar.gz.sig           # macOS Intel updater 签名
    ├── v1.0.1/         # v1.0.1 版本
    │   ├── AICoder_1.0.1_x64-setup.exe           # Windows 安装包
    │   ├── AICoder_1.0.1_x64-setup.exe.sig       # Windows updater 签名
    │   ├── AICoder_1.0.1_aarch64.dmg             # macOS Apple Silicon
    │   ├── AICoder_aarch64.app.tar.gz            # macOS ARM updater 产物
    │   ├── AICoder_aarch64.app.tar.gz.sig        # macOS ARM updater 签名
    │   ├── AICoder_1.0.1_x64.dmg                 # macOS Intel
    │   ├── AICoder_x64.app.tar.gz               # macOS Intel updater 产物
    │   └── AICoder_x64.app.tar.gz.sig           # macOS Intel updater 签名
    ├── v1.1.0/         # v1.1.0 版本（仅 Windows）
    │   ├── AICoder_1.1.0_x64-setup.exe           # Windows 安装包
    │   └── AICoder_1.1.0_x64-setup.exe.sig       # Windows updater 签名
    ├── v1.1.1/         # v1.1.1 版本（仅 Windows）
    │   ├── AICoder_1.1.1_x64-setup.exe           # Windows 安装包
    │   └── AICoder_1.1.1_x64-setup.exe.sig       # Windows updater 签名
    ├── v1.1.2/         # v1.1.2 版本（仅 Windows）
    │   ├── 智码 AICoder_1.1.2_x64-setup.exe      # Windows 安装包
    │   └── 智码 AICoder_1.1.2_x64-setup.exe.sig  # Windows updater 签名
    ├── v1.1.3/         # v1.1.3 版本
    │   ├── AICoder_1.1.3_x64-setup.exe           # Windows 安装包
    │   ├── AICoder_1.1.3_x64-setup.exe.sig       # Windows updater 签名
    │   ├── AICoder_1.1.3_aarch64.dmg             # macOS Apple Silicon
    │   ├── AICoder_aarch64.app.tar.gz            # macOS ARM updater 产物
    │   ├── AICoder_aarch64.app.tar.gz.sig        # macOS ARM updater 签名
    │   ├── AICoder_1.1.3_x64.dmg                 # macOS Intel
    │   ├── AICoder_x64.app.tar.gz               # macOS Intel updater 产物
    │   └── AICoder_x64.app.tar.gz.sig           # macOS Intel updater 签名
    └── v1.1.4/         # v1.1.4 版本
        ├── AICoder_1.1.4_x64-setup.exe           # Windows 安装包
        ├── AICoder_1.1.4_x64-setup.exe.sig       # Windows updater 签名
        ├── AICoder_1.1.4_aarch64.dmg             # macOS Apple Silicon
        ├── AICoder_aarch64.app.tar.gz            # macOS ARM updater 产物
        ├── AICoder_aarch64.app.tar.gz.sig        # macOS ARM updater 签名
        ├── AICoder_1.1.4_x64.dmg                 # macOS Intel
        ├── AICoder_x64.app.tar.gz               # macOS Intel updater 产物
        └── AICoder_x64.app.tar.gz.sig           # macOS Intel updater 签名
```

## 发布新版本流程

1. 在主项目中更新版本号（`tauri.conf.json` / `Cargo.toml` / `package.json`）
2. 打 Git Tag（`v*.*.*` 格式）并推送到 GitHub，CI 自动构建 Windows + macOS 安装包
3. 从 GitHub Release 下载产物，本地推送到本仓库并生成 `update.json`

## 许可证

Copyright (c) 2026 AgileFR. All rights reserved.
