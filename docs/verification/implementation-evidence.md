# 本地实施证据与未完成门禁

2026-10-08。插件主变更完成 **21/26** 项任务；本地实现/契约验证不代表原生、宿主或整体发行验收。原生安装授权问题已发出，尚未收到回复。

实际测试与身份见 [分层报告](local-report.json)。

## 任务映射

| ID | 状态 | 实现与证据或剩余差距 |
|---|---|---|
| P-1.1 | LOCAL_DONE | tests/test_provenance_identity.py |
| P-1.2 | LOCAL_DONE | scripts/provenance.py, source-suite.json, candidate-source.json |
| P-1.3 | LOCAL_DONE | tests/test_provenance_identity.py, tests/test_release_upgrade.py, 配套技能库 tests/test_snapshot_sync.py |
| P-1.4 | LOCAL_DONE | LICENSE, licenses/Apache-2.0.txt, scripts/validate_package.py, 配套技能库 scripts/sync_local_snapshot.py |
| P-2.1 | LOCAL_DONE | scripts/task_core.py, tests/test_review_contract.py |
| P-2.2 | LOCAL_DONE | tests/test_task_core.py, tests/test_controller_integration.py |
| P-2.3 | LOCAL_DONE | scripts/task_core.py, tests/test_task_core.py |
| P-2.4 | LOCAL_DONE | tests/test_controller_integration.py, 配套技能库 tests/test_wrapper_integration.py/test_execution_protocol.py/test_photo_contract.py |
| P-2.5 | LOCAL_DONE | tests/test_controller_integration.py, 配套技能库 tests/test_native_process.py |
| P-3.1 | LOCAL_DONE | tests/test_review_contract.py, 配套技能库 tests/test_photo_contract.py |
| P-3.2 | LOCAL_DONE | schemas/, scripts/task_core.py, tests/test_review_contract.py |
| P-3.3 | LOCAL_DONE | tests/test_review_contract.py |
| P-3.4 | LOCAL_DONE | tests/test_review_contract.py |
| P-3.5 | LOCAL_DONE | tests/test_review_contract.py |
| P-4.1 | LOCAL_DONE | .codex-plugin/plugin.json, scripts/validate_package.py |
| P-4.2 | LOCAL_DONE | .github/workflows/offline-contracts.yml, tests/, 配套技能库 tests/test_package.py；远端三个 Python 版本 CI 均通过，见 remote-ci.json |
| P-4.3 | DONE | host-0161-20261008/index.json；真实 Codex 0.161.0、中文空格缓存、五类场景；全量技能预算限制单列。 |
| P-4.4 | DONE | native-20261008/index.json、实际原生回执与宿主缓存控制器交付证据；仅该固定制品与合成样本范围。 |
| P-4.5 | LOCAL_DONE | local-components.json；不添加 hooks，无自动安装或扫描 |
| P-5.1 | LOCAL_DONE | 配套技能库 scripts/generate_runtime.py/scripts/sync_local_snapshot.py/tests/test_snapshot_sync.py, tests/test_snapshot.py |
| P-5.2 | DONE | source-release.json、candidate-source.json、source-migrations/；实际已公开来源 tag/commit/摘要。 |
| P-5.3 | OPEN | scripts/release_upgrade.py, tests/test_release_upgrade.py。升级预检与模拟 Git 回归已完成；实际来源发行、升级应用及宿主更新识别未验证。 |
| P-5.4 | OPEN | docs/verification/local-report.json。本地适用检查已通过；原生/宿主/视觉/发行缺失；远端离线 CI 已通过，不 sync/archive。 |
| P-6.1 | LOCAL_DONE | openspec/changes/extend-lightcraft-connect-mcp-plugin/ |
| P-6.2 | LOCAL_DONE | openspec/changes/extend-lightcraft-expanded-photo-capabilities-plugin/ |
| P-6.3 | LOCAL_DONE | openspec/changes/extend-lightcraft-portable-artcraft-delivery-plugin/ |

## 要求映射

| 要求 | 关联任务 | 验收范围 |
|---|---|---|
| AR-1 产物事实与交付目标 | P-3.1, P-3.2, P-4.4 | 本地证据见对应任务；整体验收 OPEN |
| AR-2 视觉审阅绑定当前内容 | P-3.3 | 本地证据见对应任务；整体验收 OPEN |
| AR-3 有界修订与最终回执 | P-3.4, P-3.5 | 本地证据见对应任务；整体验收 OPEN |
| HD-1 目标宿主接入与非侵入检查 | P-4.1, P-4.3, P-4.5 | 本地证据见对应任务；整体验收 OPEN |
| HD-2 自然语言路由与验收分层 | P-4.2, P-4.4, P-5.4 | 本地证据见对应任务；整体验收 OPEN |
| HD-3 发行与升级门禁 | P-5.2, P-5.3 | 本地证据见对应任务；整体验收 OPEN |
| PVD-1 候选来源一致性 | P-1.1, P-1.2 | 本地证据见对应任务；整体验收 OPEN |
| PVD-2 正式发行锁与受管归属 | P-1.3, P-5.1 | 本地证据见对应任务；整体验收 OPEN |
| PVD-3 快照更新保护与材料完整性 | P-1.4 | 本地证据见对应任务；整体验收 OPEN |
| TR-1 持久任务身份与单一执行契约 | P-2.1, P-2.2 | 本地证据见对应任务；整体验收 OPEN |
| TR-2 未知结果只读核对 | P-2.3, P-2.4 | 本地证据见对应任务；整体验收 OPEN |
| TR-3 停止与后续计划边界 | P-2.5 | 本地证据见对应任务；整体验收 OPEN |

## 验证边界

- Python 3.12/3.13 本地完整回归：PASS；Python 3.11 本地不可用；远端 Python 3.11/3.12/3.13 离线矩阵全部 PASS，运行身份见 [远端 CI 证据](remote-ci.json)。
- 六技能隔离、中文空格路径、来源快照和实际合成图像解码：本地检查；不构成固定原生制品的能力证明。
- skill-creator 的 quick_validate.py 依赖 PyYAML，当前解释器不可用；使用标准库包校验覆盖 frontmatter、结构与引用，没有安装依赖。
- TRACE 分数仅为静态内容基线，详见配套技能库 docs/verification/trace/，不是路由/模型/原生完成证明。
- 两个真实 RAW 样本只完成来源/摘要准备，不宣称解码通过。
- GitHub 只读查询未能解析两个目标仓库；这不证明其不存在。本轮没有 Git 提交、远端或发行证据。
- P3 三组扩展已登记独立变更：实际功能与各自 4 项任务保持 OPEN；它们不因“建立规格”任务完成而视为实现。
- 不执行 sync/archive，当前正式规格仍为增量 change。

## 本轮协议复核补充

- 导入映射改为读取重复项 existing 与 photo.inspect.source，缺失身份不再计为完整交接。
- RAW 驱动按 previewOnly 的字符串/null 协议区分预览回退；不把布尔值或缺字段当作完整 RAW。核对回执、计划、资源、原片与独立重开持久化；回退单列 PASS_WITH_PREVIEW_FALLBACK，完整 RAW 保持 NOT_PROVEN。
- 合成驱动逐一处理 PNG/JPEG 两个输入，记录前后预览和独立重开。以上驱动只完成模拟协议回归，真实原生任务仍 OPEN。
- --require-installed 的缺失目录拒绝回归及已有安装替身包装链均无下载/安装；真实 CLI 仍未执行。

## 2026-10-08 获授权后的真实验收

证据见 [原生与宿主验收索引](native-20261008/index.json)。固定制品安装、PNG/JPEG 显影导出及独立重开通过；重复/损坏/缺失导入逐项报告，占用锁未强制解除，显式批量修改只影响指定 ID。缓存插件的控制器完成真实闭环、实际图像审阅和 delivery.json。Nikon D2H 完整 RAW 解码由运行时报告通过；Blackmagic DNG 为明确不支持，Canon EOS 7D sRAW 仅预览回退通过，Canon D30 CRW 不支持。自然语言路由未通过：Codex CLI 0.147.0 配置模型要求更新宿主，且现有技能列表超出上下文预算。加载六技能不代表路由通过；未升级 Codex，也未公开发行。

### 发行检查入口回归

新增 test_release_validation_cli.py：以临时本地 Git 仓库验证 `--source-git`、CI 环境变量与发行门禁参数转交。三项先因缺失入口失败，再通过；不是公开来源发行或宿主升级识别证据。P-5.3 仍 OPEN，须待真实来源发行和宿主更新验收。

## 2026-10-08 Codex 0.161.0 宿主验收

已获隔离安装授权，CLI 0.161.0 安装于临时独立前缀；全局 CLI 仍为 0.147.0。插件在含中文和空格的新缓存目录加载六项技能。实际模型分别通过自然语言入口、显式导出入口、UNKNOWN 恢复边界、缺失依赖无安装诊断与无关请求。逐项命令、退出码与模型结果见 [宿主证据](host-0161-20261008/index.json)。验收进程只启用六项 Lightcraft 技能，不修改全局配置；全量 771 技能环境仍超上下文预算，仅通过文件搜索读取入口，不声称完整环境默认发现通过。历史章节描述当时状态，以本节和 local-report.json 为当前结论。

### 实际来源发行

技能库开发预发行 v0.1.0-dev.1 已公开：远端 tag、GitHub release 目标均为 `87fe7cebab2bc687ef7b819eb355e4e28132e6e9`，ZIP 与 SHA256SUMS 已上传；见 [公开来源身份](source-release.json)。该提交 Python 3.11/3.12/3.13 远端 CI 均通过。插件通过真实 `release_upgrade.py --apply` 锁定该来源，108 项技能文件摘要保持一致；迁移日志保留原始 APPLIED_HOST_NOT_VERIFIED 状态，宿主升级另列证据。
