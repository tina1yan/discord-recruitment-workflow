# 最小运行记录

优先更新已有项目 STATUS、CHANNELS、LOG；只有没有现有台账才新建。运行日志和截图留在用户授权的私有工作区，不自动上传公开 GitHub。

每轮记一条摘要：开始/结束时间与时区、执行者、用户授权范围、候选数、核实外部发布数、已退出临时群数、成员数起止及来源、来源明确的新增/留存、未解决项、后台任务状态。会话墙钟和实际执行时间分别写，无法测量则写未知。

每个入口可用下列 CSV 表头，或映射到已有字段：

```csv
run_id,observed_at,timezone,server_name,server_id,channel_id,channel_url,membership_before,status,message_url,published_at,minimum_interval_minutes,next_eligible_at,leave_status,evidence_path,blocker,next_action
```

状态建议：

- `CANDIDATE`：只找到入口，尚未发布。
- `JOINED_NO_POST`：加入但未发布，继续处理普通步骤或退出。
- `SKIPPED`：该路径未发，写清事实原因，不用“bot检测”概括所有错误。
- `UNCERTAIN`：发送结果不明，先核对，禁止重发。
- `PUBLISHED_VERIFIED`：有已发消息及回执证据。
- `PUBLISHED_THEN_LEFT_VERIFIED`：消息核实后已离开临时群，退群后留存未知。
- `LEFT_NO_POST`：无法发布，已离开新加临时群。

`membership_before` 记录 `existing`、`new` 或 `unknown`，未知时不得擅自退出。`next_eligible_at` 带日期和时区，用最后成功时间加更严格的发布间隔计算；运行前仍读最新消息，避免别人已经操作。

交接只需要：本轮真实成果及链接、当前所在页面/草稿、仍占用的临时群、下一次允许操作时间、明确的阻塞，以及原项目记录位置。旧交接中的时间必须标成历史快照，不能直接执行。
