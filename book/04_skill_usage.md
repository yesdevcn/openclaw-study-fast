# 第4章：使用技能库

在本章中，我们将探索 OpenClaw 丰富的技能库，并通过一个案例学习如何安装、调用和组合技能。

## 什么是技能？
技能是 OpenClaw 的核心组件，封装了特定功能，使复杂任务可以被简单调用。

---

## 案例：GitHub 自动化操作
任务目标：
1. 自动检查指定仓库的 Pull Request (PR) 列表。
2. 对符合条件的 PR 添加评论。

---

### 第一步：安装 GitHub 技能
使用以下命令安装 GitHub 技能模块：

```bash
npx openclaw install github
```

GitHub 技能提供了对仓库、Issues、Pull Requests 等操作的封装。

---

### 第二步：配置技能凭据
编辑 `.env` 文件，添加 GitHub API 的访问令牌：

```bash
GITHUB_TOKEN=your_personal_access_token
```
- 如何生成 `GITHUB_TOKEN`：
  1. 登录 GitHub，进入[开发者页面](https://github.com/settings/tokens)。
  2. 创建一个具有 `repo` 权限的令牌。
  3. 将其存储到 OpenClaw 配置中。

---

### 第三步：创建自动化工作流
编辑 `workflow.json` 文件，定义以下内容：

```json
{
  "name": "github-comment-bot",
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
      "skill": "github",
      "action": "comment-pr",
      "input": {
        "owner": "example-owner",
        "repo": "example-repo",
        "pr_id": "{{prs[0].id}}",
        "comment": "自动评论：感谢您的贡献，我们会尽快审核这个 PR！"
      }
    }
  ]
}
```
- **第一步**：调用 `list-prs` 列出所有 PR，并将结果存储在变量 `prs` 中。
- **第二步**：调用 `comment-pr`，对第一个 PR 添加评论。

---

### 第四步：运行工作流
启动工作流：

```bash
npx openclaw start-workflow github-comment-bot
```
终端将实时显示流程以及执行结果。

---

### 日志验证
查看 OpenClaw 的运行日志：

```bash
npx openclaw logs
```
确保工作流操作的调用数据正确。

---

## 技能组合的强大
借助 OpenClaw 可以组合多个技能，例如：
- **每日定时提醒**：天气技能 + 日历技能。
- **代码自动分析**：GitHub 技能 + Linter 技能。

通过技能组合，您可以灵活完成高度定制化的工作流。下一章我们将深入介绍自定义技能的开发过程。