# LightCraft Use

## 插件市场导航

本插件所属分类：**AIGC 内容创作**。

| 分类 | 插件市场入口 | 用途 |
| --- | --- | --- |
| 全栈开发 | [Full Stack Plugins](https://github.com/partme-ai/full-stack-plugins) | 架构与 UI 设计、代码理解、质量检查、代码审查、流程治理与服务器运维 |
| AIGC 内容创作 | [Full AIGC Plugins](https://github.com/partme-ai/full-aigc-plugins) | 图像、视频、音频、音乐、3D 与多模态内容创作 |

![LightCraft Use——照片管理与无损显影](assets/official-logo.png)

> 在智能体宿主里筛选、显影并导出照片，原片保持不变，每一步显影都留成可回退的设置。

[![版本](https://img.shields.io/badge/release-0.1.0--dev.20261018.3-1A73E8)](https://github.com/full-aigc-plugins/lightcraft-plugin/releases)
[![技能](https://img.shields.io/badge/skills-17-00A67E)](#技能)
[![MCP 工具](https://img.shields.io/badge/MCP%20tools-14-00A67E)](#mcp-工具)
[![许可证](https://img.shields.io/badge/license-Apache--2.0-green)](LICENSE)

[English](README.md) | [简体中文](README.zh-CN.md) · [安装](#安装) · [快速开始](#快速开始) · [技能](#技能) · [故障排查](#故障排查)

## 项目定位

`lightcraft` 让智能体宿主驱动真实的 LightCraft CLI 与其浏览器面板，因此照片任务的结果是可解码的输出文件、带版本的显影历史和交付回执，而不是「已经调过滑杆」的口头承诺。插件负责照片技能、显式任务控制器和同会话面板桥接；它不替代 LightCraft，也不重新实现 RAW 解码。

| 属性 | 取值 |
| :--- | :--- |
| 插件 ID | `lightcraft` |
| 版本 | `0.1.0-dev.20261018.3` |
| 状态 | 开发预览；生产发布被阻塞，创作验收尚未关闭 |
| 固定原生 CLI | LightCraft CLI `0.2.1` |
| 已核验平台 | macOS arm64，Python 3.11 或更新版本 |
| 面板运行时 | Node.js 24，由 `ui/bootstrap.mjs` 启动 |
| 许可证 | Apache-2.0 |

## 安装

### 前置条件

- `PATH` 上有 Node.js 24，供 stdio MCP server 与面板使用。
- Python 3.11 或更新版本；技能与 `scripts/controller.py` 都是 Python 入口。
- 固定 CLI 需要 macOS arm64。其他平台按独立变更跟踪，当前不作宣称。
- 首次打开面板需要网络：插件会下载并校验锁定编辑器制品，完整发行 ZIP 已内置该制品。
- 原生 CLI 不随包分发。安装器会下载锁定的官方发行，并把许可文件保留在制品内。

### 从插件市场安装

```bash
codex plugin marketplace add partme-ai/full-aigc-plugins
codex plugin add lightcraft@full-aigc-plugins
```

重启宿主，新建任务，在动任何照片之前先让 LightCraft 检查照片库。

### 其他宿主清单

| 宿主 | 清单 | 路径基准 |
| --- | --- | --- |
| 标准 Agent Plugins 1.0.0 | `plugin.json`、`mcp.json` | `${PLUGIN_ROOT}` |
| Codex | `.codex-plugin/plugin.json`、`.codex-plugin/mcp.json` | 相对 `cwd` 的插件根目录 |
| Claude Code | `.claude-plugin/plugin.json`、`.mcp.json` | `${CLAUDE_PLUGIN_ROOT}` |

此外还提供 Kimi（`kimi.plugin.json`）、DeepSeek Harness（`dsh/`）和 WorkBuddy 示例（`hosts/workbuddy/mcp.json`）。在开发仓中必须先构建编辑器资源，只克隆源码不等于已安装运行包。

## 快速开始

```mermaid
flowchart LR
    A[安装插件] --> B[在工作区打开面板]
    B --> C[command_list / list_files]
    C --> D[导入并检查照片]
    D --> E[按真实照片 ID 显影]
    E --> F[导出并解码实际文件]
    F --> G[独立重开复核]
```

1. 打开面板时显式传入 `workspace` 参数。
2. 先查环境：`python3 -I -B "$SKILL_DIR/scripts/bootstrap.py" --no-install` 只报告锁定 CLI，不执行安装。
3. 用 `command_list` 读真实命令，改动前先用 `inspect` 读照片。
4. 用 `command_run` 显影，始终绑定真实照片 ID；不要凭记忆编造设置对象。
5. 导出后解码实际输出文件，并在独立会话中重开照片库，才能判定任务完成。

长任务使用显式控制器记录状态，而不是依赖对话记忆：

```bash
python3 -I -B scripts/controller.py init /absolute/new-task --payload /absolute/init.json
python3 -I -B scripts/controller.py run /absolute/new-task --runtime-home /absolute/runtime
python3 -I -B scripts/controller.py status /absolute/new-task
python3 -I -B scripts/controller.py deliver /absolute/new-task
```

`init`、`run`、`status`、`inspect`、`reconcile`、`stop`、`remaining`、`review-request`、`review`、`revise` 与 `deliver` 是各自独立的调用。`UNKNOWN` 不重放，`reconcile` 只读。

## 可完成的工作

| 工作流 | 内置路径 | 可验证输出 |
| :--- | :--- | :--- |
| RAW 基础显影 | `lightcraft-raw-develop` | 白平衡、曝光、高光与阴影设置，加可解码输出 |
| 同组照片批量调色 | `lightcraft-batch-photo-style` | 只作用于清单内照片的统一风格 |
| 风光显影 | `lightcraft-landscape-develop` | 天空、地面与层次分离恢复 |
| 人像自然显影 | `lightcraft-portrait-develop` | 肤色、曝光与背景平衡 |
| 筛选与评级 | `lightcraft-photo-culling` | 评级、分组与精选集 |
| 成片交付 | `lightcraft-photo-export` | 尺寸、色彩与命名合规的文件，附回执 |
| 独立虚拟副本审稿 | `lightcraft-virtual-copy-review` | 不影响原片的可审阅副本 |
| 命名版本恢复 | `lightcraft-named-version-restore` | 设置与像素都回到该命名版本 |
| 曲线迁移 | `lightcraft-tone-curve-transfer` | 只移动曲线，曝光、色彩与裁切保持 |

## 技能

| 技能 | 作用 |
| :--- | :--- |
| `lightcraft-use` | 主入口：路由照片任务并衔接各阶段 |
| `lightcraft-editor` | 在宿主内打开编辑器，让 Agent 修改显示在同一页面 |
| `lightcraft-cli` | 命令目录、控件清单、JSON 计划检查与回执契约 |
| `lightcraft-cli-setup` | 检查或安装锁定 CLI、核对版本、诊断失败 |
| `lightcraft-cli-library` | 导入、选择与组织照片，排查重复导入 |
| `lightcraft-cli-develop` | 曝光、白平衡、局部调整与按范围同步显影 |
| `lightcraft-cli-export` | 导出照片，检查格式、尺寸与色彩，核对实际文件 |
| `lightcraft-raw-develop` | RAW 基础：白平衡、曝光、高光与阴影 |
| `lightcraft-batch-photo-style` | 统一同组照片的风格 |
| `lightcraft-landscape-develop` | 风光片的天空、地面与色调层次 |
| `lightcraft-portrait-develop` | 肤色、曝光与背景平衡 |
| `lightcraft-photo-culling` | 导入、评级、分组与精选 |
| `lightcraft-photo-export` | 精选照片的尺寸、色彩与命名 |
| `lightcraft-virtual-copy-review` | 在独立虚拟副本中审稿，不触碰原片 |
| `lightcraft-named-version-restore` | 试调命名版本并精确恢复 |
| `lightcraft-tone-curve-transfer` | 只迁移曲线，保留逐片曝光与裁切 |
| `lightcraft-scenario-playbooks` | 亮部整理、黑白版本、正方形构图、灰卡白平衡、水印审稿、双格式导出、联系表与分区回退 |

技能由独立的 `lightcraft-skills` 运行时生成，此处消费的是受摘要保护的快照；`candidate-source.json` 固定已公开来源，`source-suite.json` 记录独立的原生版本。

## MCP 工具

只内置一个 server：`lightcraft-editor`，使用 **stdio**。本地 HTTP 只承载面板与同会话桥接。目录共 14 个工具，其中 11 个可供 Agent 调用，3 个 `_panel_*` 是面板内部使用的桥接工具。

| 类别 | 工具 | 用途 |
| :--- | :--- | :--- |
| 会话 | `open_editor`、`open_browser_editor`、`editor_status` | 打开面板并确认已接入 |
| 命令网关 | `command_list`、`command_run` | 查询真实命令，用 JSON 参数执行单条 |
| 检查 | `inspect` | 读取可见编辑器或 LightCraft 图库的状态 |
| 图库 | `list_files`、`open_file` | 列出浏览器编辑器持有的文件；把工作区文件导入其中 |
| 交付 | `save_file`、`save_project`、`screenshot` | 把浏览器文件或工程另存到新的工作区路径；截取画布 |

`save_project` 不适用于浏览器图库：图库位于页面浏览器存储，应通过 `file.backupLibrary` 命令导出备份。

## 配置

| 配置 | 位置 | 作用 |
| :--- | :--- | :--- |
| `workspace` 参数 | `open_editor` / `open_browser_editor` | 绑定任务目录；越界路径会被拒绝 |
| `--runtime-home` | Harness CLI 与控制器 | 隔离锁定运行时缓存 |
| `CRAFT_EDITOR_UPDATE=off` | stdio MCP 的 `env` | 只用内置面板，不再尝试下载 |
| `CRAFT_EDITOR_CACHE_DIR` | 环境变量 | 已校验编辑器归档的绝对缓存目录 |
| `LIGHTCRAFT_SOURCE_GIT` | CI 与发行预检 | 用于核验技能来源锁的 Git 检出 |

已校验归档缓存在 `~/.cache/full-aigc/editors`。活动会话在关闭前保持自己的版本，缓存损坏时回退内置版本。

## 架构与安全

Agent 与插件之间只走 stdio MCP；浏览器桥接只监听 `127.0.0.1`，使用随机令牌并校验 Host/Origin。工作区之外的路径被拒绝，下载内容按 SHA-256 校验，内置面板始终保留为回退。

原片被当作只读输入：编辑是叠加在带版本历史上的设置，交付需要匹配的重开回执。控制器持有持久任务锁与原子状态，拒绝重放 `UNKNOWN`，并对修订次数设上限。插件不保存凭据，也没有流量到达作者。详见[架构](docs/architecture.zh-CN.md)、[控制器操作契约](docs/controller.zh-CN.md)、[任务回执](docs/task-receipts.zh-CN.md)、[实施证据](docs/verification/implementation-evidence.md)。

## 故障排查

| 现象 | 处理 |
| :--- | :--- |
| 看不到面板工具 | 确认插件已启用，重启宿主，新建任务 |
| 宿主内不渲染面板 | 改用 `open_browser_editor` 返回的地址；终端本身不提供浏览器面板 |
| CLI 缺失或版本不对 | 运行 setup 技能的 `bootstrap.py --no-install` 检查；安装器不会静默升级 |
| 导出后 RAW 颜色异常 | 在独立会话中复核实际解码文件；Nikon RAW 色彩准确性仍是未关闭门禁 |
| 照片库不见了 | 图库在浏览器存储中；用 `file.backupLibrary` 的导出版本恢复 |
| 运行以 `UNKNOWN` 结束 | 先只读核对再决定；不要重放该步骤 |

## 升级

```bash
codex plugin marketplace upgrade full-aigc-plugins
codex plugin add lightcraft@full-aigc-plugins
```

CLI、编辑器归档与技能快照分别锁定；升级插件不会静默升级原生 CLI。

## 贡献与支持

问题请提交到 <https://github.com/full-aigc-plugins/lightcraft-plugin/issues>。行为变更先在 `openspec/changes/` 立规格，任务只有在真实验收后才勾选。宣称能力前先读 `AGENTS.md` 与 `docs/verification/implementation-evidence.md`，并保持中英文一致。

## 许可证

本仓原创内容采用 [Apache-2.0](LICENSE)。图标为 MIT OR Apache-2.0 许可的上游 LightCraft 素材，来源记录在 `assets/official-icon-source.json`。原生 CLI 不再分发，其许可文件随锁定制品提供。上游 LightCraft 是独立项目 <https://github.com/storytold/lightcraft>。
