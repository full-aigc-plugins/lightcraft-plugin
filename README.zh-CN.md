# Lightcraft 插件

待发布开发预发行 `0.1.0-dev.3`，包含技能库六项技能的受摘要保护快照。`candidate-source.json` 锁定已公开来源 v0.1.0-dev.1 / 87fe7ce；`source-suite.json` 记录来源版本，原生版本独立为 `0.2.1`。插件运行不需要来源仓库。

已实现持久任务锁、原子状态、只读核对、停止请求、明确剩余步骤建议、有界修订、绑定目标/原片/候选/设置的审阅，以及独立重开交付门禁。`.codex-plugin/plugin.json` 是最小接入清单；不添加自动 hooks。来源升级默认只预检，拒绝快照漂移或用户修改。

```bash
python3 -I -B scripts/validate_package.py
python3 -I -B -m unittest discover -s tests -v
python3 -I -B scripts/controller.py --help
```

控制器通过 `init/run/status/inspect/reconcile/stop/remaining/review-request/review/revise/deliver` 显式调用。run 可能触发原生安装；只在已有授权内执行。inspect/reconcile 不启动原生程序，UNKNOWN 不重放。

输入 JSON、恢复与审阅交接见 [控制器操作契约](docs/controller.zh-CN.md)。

主 OpenSpec 任务 **26/26** 完成，主变更适用验收与公开开发预发行已完成。已通过宿主安装/发现、缓存控制器原生闭环与合成图视觉审阅；Codex 0.161.0 六技能隔离环境的五类宿主场景已通过，全量技能环境仍有上下文预算限制；Git main 已推送，Python 3.11/3.12/3.13 远端离线 CI 全部通过；插件开发预发行 v0.1.0-dev.2 已公开，锁定技能库 v0.1.0-dev.1。三个 P3 独立扩展变更保持 OPEN。

[任务与规格](openspec/README.md) · [当前证据及差距](docs/verification/implementation-evidence.md) · [分层报告](docs/verification/local-report.json) · [架构](docs/architecture.md) · [回执与来源同步](docs/task-receipts.zh-CN.md)

本轮候选状态与实际证据以 [六目标验收记录](docs/verification/windows-20261008/README.md) 为准，历史版本通过记录不能代替当前候选验收。
