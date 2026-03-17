# 第6章：复杂任务的工作流组装

本章将深入讲解如何结合多个技能和任务，将其编排成高效的工作流。

## 什么是工作流？
工作流是 OpenClaw 的核心功能，它将多个操作按顺序或条件组织在一起，适用于复杂的自动化任务。

---

## 案例：日报生成器
任务目标：
1. 每天早晨生成一份项目日报，包括：
   - 最新 GitHub PR 列表。
   - 团队待办总结。
   - 外部天气信息。
2. 将日报发送到 Feishu 群组。

---

### 第一步：安装必要技能
您需要安装以下技能：

```bash
npx openclaw install github
npx openclaw install task-manager
npx openclaw install weather
npx openclaw install feishu
```

这些技能分别用于：
- 获取 GitHub PR 信息。
- 管理任务清单。
- 查询天气。
- 向 Feishu 推送消息。

---

### 第二步：定义工作流
编辑 `workflow.json`，配置如下任务：

```json
{
  "name": "daily-report",
  "steps": [
    {
      "skill": "github",
      "action": "list-prs",
      "input": {
        "owner": "example-owner",
        "repo": "example-repo"
      },
      "alias": "prs"
    },
    {
      "skill": "task-manager",
      "action": "list-tasks",
      "alias": "tasks"
    },
    {
      "skill": "weather",
      "action": "get-today",
      "input": {
        "location": "Beijing"
      },
      "alias": "weather"
    },
    {
      "skill": "feishu",
      "action": "send-message",
      "input": {
        "chat_id": "example-chat-id",
        "message": "Good morning! Here is today's report:\n- Weather: {{weather.summary}}, {{weather.temp}}°C\n- PRs:\n{{prs.map(pr => `#${pr.id} - ${pr.title}`).join('\n')}}\n- Tasks:\n{{tasks.map(task => `- ${task.name}`).join('\n')}}"
      }
    }
  ]
}
```

- **PR 列表**：列出指定仓库的 Pull Requests。
- **待办任务**：从任务管理工具提取待办项。
- **天气信息**：获取当天的天气动态。
- **消息推送**：将处理结果在 Feishu 群组中展示。

---

### 第三步：运行工作流
执行以下命令启动自动化流程：

```bash
npx openclaw start-workflow daily-report
```
OpenClaw 会依次执行步骤并输出流程结果。

---

### 日志分析
在完成执行后，可以查看运行日志以调试或优化工作流：

```bash
npx openclaw logs
```

---

### 扩展方向
- **条件逻辑**：根据天气类型修改每日提醒内容。
- **多渠道推送**：同时发送到 Feishu 和电子邮件。
- **数据存档**：将日报保存到云存储供后续分析。

通过以上内容，您已经能够构建适合自己的复杂工作流程！