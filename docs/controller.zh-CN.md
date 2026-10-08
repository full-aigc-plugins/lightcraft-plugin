# 显式任务控制器

本资料说明当前接口，不是宿主加载或原生验收记录。控制器通过插件根目录的 `scripts/controller.py` 调用；任务目录与照片库由调用者明确指定，不能猜测宿主缓存路径。运行可能安装原生依赖，只能在已有相应授权时使用；纯诊断使用技能自己的 doctor。

## 建立与执行任务

`init` 的 `--payload` JSON 对应以下字段；本例仅展示只读照片库查询计划，不是可交付照片编辑闭环。

```json
{
  "goal": {"request": "检查指定照片库"},
  "plan": {"domain": "lightcraft", "steps": [{"command": "library.info", "params": {}}]},
  "inputs": ["/absolute/originals"],
  "library": "/absolute/library",
  "output_root": "/absolute/exports",
  "max_revisions": 3
}
```

inputs 必须已存在且指向要保全的原片；library 是可修改持久库，output_root 是导出目标根；任务目录必须是新目录。已有任务不能再次 init。实际编辑计划须根据当前目录选择照片，包含 photo.inspect、develop.get 与导出步骤，不能把示例中的库查询当作完成编辑。

```bash
python3 -I -B scripts/controller.py init /absolute/new-task --payload /absolute/init.json
python3 -I -B scripts/controller.py run /absolute/new-task --runtime-home /absolute/runtime
python3 -I -B scripts/controller.py status /absolute/new-task
python3 -I -B scripts/controller.py reconcile /absolute/new-task
```

run 只接受 PLANNED 状态并持有任务锁；开始状态先落盘。status/inspect/reconcile 不启动 Lightcraft、不推进状态。UNKNOWN 不可重新 run；先核对回执与进程事实，不把目录中的导出文件当作执行成功。

## 停止与剩余步骤

stop 发布停止请求，即使运行控制器持锁也能请求；只有原始监督器能终止它启动的进程组，不能用 PID 文件向别的进程发送信号。请求成功不等于原生已取消。

remaining 仅在可信 FAILED_OR_PARTIAL 回执中提取明确 NOT_EXECUTED 的步骤。它还核对 run、计划、资源和输入身份，只输出建议片段；新会话须恢复库与照片选择，并重新确认执行范围。该接口不修改原任务或自动执行。

## 审阅与修订

review-request 的 payload 字段：

| 字段 | 内容 |
|---|---|
| candidates | 每个对象包含真实 path，可用 expected 声明 format/width/height/bitDepth/colorSpace/iccSha256 |
| settings | 执行回执中成功 develop.get 返回的完整设置对象，不能手填期望值或只提供局部补丁 |
| rubric_version | 非空审阅规则版本 |
| reopen_evidence | 可选 `{ "receiptPath": "/absolute/independent-run/receipt.json" }`；最终 deliver 时必需 |

候选必须可解码且符合目标，并且执行回执中有成功 photo.inspect 提供照片 ID 与源身份。请求绑定目标、原片、候选、设置、规则和修订次数。review 的 payload 遵循 `schemas/review-receipt.schema.json`：schemaVersion、requestId、bindingSha256、source（human/host-model）、reviewer、verdict（PASS/FAIL）和非空 observations 数组。它必须来自实际审阅；包校验不得自行生成视觉 PASS。候选变化或重复回执均拒绝。

失败审阅后用 revise 提交 `{plan, issue, scope}`，明确问题与允许调整范围。次数和历史保留在任务中；达到 max_revisions 后拒绝，不因重启重置。修改计划须指定新导出路径，不能覆盖既有候选。

## 最终交付

deliver 要求当前视觉 PASS、候选与原片未变，以及同一库在不同 runId 的独立会话重开回执。设置与照片源身份必须一致，library.info 明确 persistent=true、unsavedOps=0，库摘要不能在重开后变化。只满足其中一层时不能完成。

成功后保留 state.json、delivery.json、执行日志、审阅请求/回执和修订历史；交付回执分列执行、持久化、文件、重开、视觉及未验证项。真实宿主/原生/视觉验收与发行状态见 [实施证据](verification/implementation-evidence.md)。
