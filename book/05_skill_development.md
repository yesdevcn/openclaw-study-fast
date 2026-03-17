# 第5章：自定义技能开发

在本章中，我们将从零开始创建一个 OpenClaw 技能，学习技能开发的完整过程。

## 什么是技能？
技能是 OpenClaw 的基本功能单元，负责完成特定的任务。自定义技能可以帮助用户实现高度个性化的需求。

---

## 案例：定时提醒技能
任务目标：开发一个技能，每天早晨自动发送天气提醒和任务清单。

---

### 第一步：创建技能骨架
执行以下命令生成技能模板：

```bash
npx openclaw create-skill daily-reminder
```
该命令会在当前目录中创建一个名为 `daily-reminder` 的文件夹，包含基础结构：

```
.daily-reminder/
├── index.js     # 技能主逻辑
├── skill.json   # 技能配置信息
└── package.json # npm 配置
```

---

### 第二步：定义技能配置
编辑 `skill.json` 文件，补充技能的元信息：

```json
{
  "name": "daily-reminder",
  "description": "每天早晨发送天气提醒和任务清单。",
  "version": "1.0.0",
  "author": "Your Name"
}
```

---

### 第三步：编写技能逻辑
修改 `index.js` 文件，添加天气提醒和任务清单的逻辑：

```javascript
const fetchWeather = require('weather-api');
const fetchTasks = require('task-api');

module.exports = async function(context) {
  const weather = await fetchWeather('Los Angeles');
  const tasks = await fetchTasks('user123');

  const message = `早安！今天的天气是：${weather.summary}，温度：${weather.temp}°C\n` +
                  `你的任务清单：\n${tasks.join('\n')}`;

  context.send(message);
};
```
> 说明：
> - `fetchWeather` 是一个模拟的天气 API 请求。
> - `fetchTasks` 模拟从任务管理工具获取任务清单。

---

### 第四步：技能调试
在技能开发完成后，使用以下命令进行测试：

```bash
npx openclaw debug daily-reminder
```
查看终端输出，验证技能逻辑是否正确。

---

### 第五步：运行技能
注册技能后，您可以直接在 OpenClaw 环境中调用该技能：

```bash
npx openclaw run-skill daily-reminder
```

---

### 扩展功能
- **增强消息格式**：支持 HTML 或 Markdown 格式化通知内容。
- **支持多种数据源**：如整合 Gmail 邮件摘要。

通过学习本章内容，您已掌握创建自定义技能的基础流程。下一章将探讨复杂任务的工作流编排！