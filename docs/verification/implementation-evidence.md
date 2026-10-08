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
| P-4.2 | LOCAL_DONE | .github/workflows/offline-contracts.yml, tests/, 配套技能库 tests/test_package.py；远端 CI 未运行 |
| P-4.3 | OPEN | .codex-plugin/plugin.json。宿主发现、加载、六技能路由和新缓存安装未授权/未运行。 |
| P-4.4 | OPEN | scripts/controller.py, scripts/task_core.py；仅 mock 回归。固定制品在宿主中的原生与独立视觉闭环未运行。 |
| P-4.5 | LOCAL_DONE | local-components.json；不添加 hooks，无自动安装或扫描 |
| P-5.1 | LOCAL_DONE | 配套技能库 scripts/generate_runtime.py/scripts/sync_local_snapshot.py/tests/test_snapshot_sync.py, tests/test_snapshot.py |
| P-5.2 | OPEN | scripts/provenance.py, scripts/release_preflight.py。未获 Git/远端/发布授权，无实际 tag/commit。 |
| P-5.3 | OPEN | scripts/release_upgrade.py, tests/test_release_upgrade.py。升级预检与模拟 Git 回归已完成；实际来源发行、升级应用及宿主更新识别未验证。 |
| P-5.4 | OPEN | docs/verification/local-report.json。本地适用检查已通过；原生/宿主/视觉/发行/远端 CI 缺失，不 sync/archive。 |
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

- Python 3.12/3.13 本地完整回归：PASS；Python 3.11 本地不可用，远端 CI 尚未运行。
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
