# Lightcraft 插件

待发布开发预发行 `0.1.0-dev.3`，包含技能库六项技能的受摘要保护快照。`candidate-source.json` 锁定已公开来源 v0.1.0-dev.1 / 87fe7ce；`source-suite.json` 记录来源版本，原生版本独立为 `0.2.1`。插件运行不需要来源仓库。

已实现持久任务锁、原子状态、只读核对、停止请求、明确剩余步骤建议、有界修订、绑定目标/原片/候选/设置的审阅，以及独立重开交付门禁。`.codex-plugin/plugin.json` 是最小接入清单；不添加自动 hooks。来源升级默认只预检，拒绝快照漂移或用户修改。

```bash
python3 -I -B scripts/validate_package.py --source-git /path/to/lightcraft-skills
python3 -I -B -m unittest discover -s tests -v
python3 -I -B scripts/controller.py --help
```

控制器通过 `init/run/status/inspect/reconcile/stop/remaining/review-request/review/revise/deliver` 显式调用。run 可能触发原生安装；只在已有授权内执行。inspect/reconcile 不启动原生程序，UNKNOWN 不重放。

输入 JSON、恢复与审阅交接见 [控制器操作契约](docs/controller.zh-CN.md)。

主 OpenSpec 任务 **26/26** 完成，主变更适用验收与公开开发预发行已完成。已通过宿主安装/发现、缓存控制器原生闭环与合成图视觉审阅；Codex 0.161.0 六技能隔离环境的五类宿主场景已通过，全量技能环境仍有上下文预算限制；Git main 已推送，Python 3.11/3.12/3.13 远端离线 CI 全部通过；插件开发预发行 v0.1.0-dev.2 已公开，锁定技能库 v0.1.0-dev.1。三个 P3 独立扩展变更保持 OPEN。

[任务与规格](openspec/README.md) · [当前证据及差距](docs/verification/implementation-evidence.md) · [公开预发行历史报告](docs/verification/local-report.json) · [架构](docs/architecture.md) · [回执与来源同步](docs/task-receipts.zh-CN.md)

Connect/MCP 增量正在验收，见 [当前增量证据](docs/verification/connect-mcp-20261008/README.md)。上述公开预发行与宿主通过记录绑定历史源码，不能证明本次增量已完成宿主或桌面验收。三个独立扩展继续保持 OPEN。

批量范围与选择性修订增量已完成实际三照片验收，见 [批量证据](docs/verification/batch-20261008/README.md)。扩展变更尚未整体完成，当前发布草稿的旧目标提交不会自动包含此增量。

逐样本 RAW 身份与结果分层已完成当前原生验收，见 [RAW 证据](docs/verification/raw-20261008/README.md)。完整解码、预览回退和不支持分别记录，仅适用于所测摘要与相机变体。

SAM 当前只读评估与未完成门禁见 [验收记录](docs/verification/sam-20261008/README.md)。

三领域协议消费与失效规则已验证，宿主自动调度仍未验收，见 [实际证据](docs/verification/exchange-20261008/README.md)。
