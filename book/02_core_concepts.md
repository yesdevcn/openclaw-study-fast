# 第2章：核心概念与命令

本章将帮助您理解 OpenClaw 的核心概念，以及学会一些重要的基础命令。

## 核心概念
OpenClaw 是一个模块化的自动化开发框架，以下是几个关键部分的概述：

### 1. Skill（技能模块）
- 每个技能是一个独立的功能模块，负责完成特定任务。
- 举例：天气查询、GitHub 操作。
- 技能的安装和调用可以通过命令行完成。

### 2. Session（会话）
- 会话是用户与 OpenClaw 的交互流程，包含任务状态、环境变量等信息。
- 支持多会话并行运行。

### 3. Workflow（工作流）
- 将多个任务或技能有机组合起来，形成完整的自动化策略。
- 示例：工作流“每天早上提醒天气和邮件通知”。

### 4. Plugin（插件）
- OpenClaw 支持扩展，通过自定义插件，可以轻松添加新功能。

---

## 常用命令
以下是一些常用的命令以及它们的作用：

### 1. 初始化工作环境
```bash
npx openclaw init
```
- 作用：初始化 OpenClaw 配置，并创建工作目录。
- 输出：生成 `.openclaw/` 隐藏配置文件夹。

### 2. 安装技能
```bash
npx openclaw install <skill-name>
```
- 作用：从技能市场或自定义源码中安装技能模块。
- 示例：
  ```bash
  npx openclaw install weather
  ```

### 3. 查看技能列表
```bash
npx openclaw list skills
```
- 作用：显示当前环境中的所有技能模块，以及对应的版本信息。

### 4. 创建自定义技能
```bash
npx openclaw create-skill <skill-name>
```
- 作用：生成一个技能的骨架代码。

### 5. 调试技能
```bash
npx openclaw debug <skill-name>
```
- 作用：启动调试模式，用于技能的调试和问题定位。

---

## 进阶命令
如果需要测试工作流或运行更复杂的任务，可以使用以下命令：

### 1. 启动工作流
```bash
npx openclaw start-workflow <workflow-name>
```
- 示例：
  ```bash
  npx openclaw start-workflow morning-routine
  ```

### 2. 日志查看
```bash
npx openclaw logs
```
- 用于查看最近任务的日志信息，辅助排查问题。

---

下一章，我们将通过一个案例详细演示如何创建和运行一个简单的自动化任务。