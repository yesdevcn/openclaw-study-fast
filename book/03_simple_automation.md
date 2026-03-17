# 第3章：简单自动化任务

本章通过一个简明的案例，展示 OpenClaw 的基本能力，并指导您创建和运行第一个自动化任务。

## 创建任务：文件整理器
任务目标：实现一个自动化脚本，将指定目录下的日志文件按日期分类存储。

---

### 第一步：初始化项目
```bash
npx openclaw init
```
运行上述命令后，OpenClaw 会创建默认的项目结构，包括所有必要配置文件。

---

### 第二步：安装依赖技能 - 文件操作
在本案例中，我们需要安装一个技能，用于处理文件操作：

```bash
npx openclaw install file-manager
```
该技能支持文件移动、复制、读取等功能，特别适合我们的需求。

---

### 第三步：创建工作流
编辑 `workflow.json` 文件，定义如下流程：

```json
{
  "name": "organize-logs",
  "steps": [
    {
      "skill": "file-manager",
      "action": "move",
      "input": {
        "source": "./logs/",
        "destination": "./archive/{YEAR}/{MONTH}/",
        "filters": ["*.log"]
      }
    }
  ]
}
```
- **`source`**: 要分类整理的日志文件目录。
- **`destination`**: 文件保存路径，自动按年/月分类。
- **`filters`**: 查询条件，仅针对扩展名为 `.log` 的文件移动。

---

### 第四步：运行工作流
使用以下命令启动工作流：

```bash
npx openclaw start-workflow organize-logs
```
运行后，OpenClaw 会处理定义的每个步骤，并在终端显示任务状态。

---

### 日志验证
查看控制台或直接检查日志输出目录：

```bash
tree ./archive/
```
示例输出：

```
./archive/
├── 2026/
│   └── 03/
│       ├── access.log
│       └── error.log
```

确认整理后的日志文件已按预期分类存储。

---

### 扩展案例
您可以将该任务扩展应用到更多文件类型：
- **图片整理**：按尺寸分类存放。
- **文档聚合**：自动归档不同项目的报告文档。

下一章我们将探讨如何调用现有技能库，快速实现复杂自动化任务。