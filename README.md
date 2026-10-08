# Lightcraft 插件

开发候选 `0.1.0-dev.1`，包含技能库六项技能的受摘要保护快照。`candidate-source.json` 记录未发布来源；`source-suite.json` 记录来源版本，原生版本独立为 `0.2.1`。插件运行不需要来源仓库。

已实现持久任务锁、原子状态、只读核对、停止请求、明确剩余步骤建议、有界修订、绑定目标/原片/候选/设置的审阅，以及独立重开交付门禁。`.codex-plugin/plugin.json` 是最小接入清单；不添加自动 hooks。来源升级默认只预检，拒绝快照漂移或用户修改。

```bash
python3 -I -B scripts/validate_package.py
python3 -I -B -m unittest discover -s tests -v
python3 -I -B scripts/controller.py --help
```

控制器通过 `init/run/status/inspect/reconcile/stop/remaining/review-request/review/revise/deliver` 显式调用。run 可能触发原生安装；只在已有授权内执行。inspect/reconcile 不启动原生程序，UNKNOWN 不重放。

输入 JSON、恢复与审阅交接见 [控制器操作契约](docs/controller.zh-CN.md)。

主 OpenSpec 任务 **21/26** 完成，剩余宿主安装/发现、真实原生视觉闭环、发行身份、升级识别和最终跨项目验收保持 OPEN。没有宿主、原生、视觉或远端 CI 通过证据；Git 已初始化，正在交付开发候选；尚无公开发行。三个 P3 独立扩展变更保持 OPEN。

[任务与规格](openspec/README.md) · [当前证据及差距](docs/verification/implementation-evidence.md) · [分层报告](docs/verification/local-report.json) · [架构](docs/architecture.md) · [回执与来源同步](docs/task-receipts.zh-CN.md)
