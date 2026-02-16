# AI Skills: Task Manager

这是一个用于规划和优化任务的项目，包含以下功能：
- `task-composer`: 生成项目任务分解结构（WBS）
- `task-suggestor`: 根据现有数据提供优化建议

## 项目结构

```text
skills/
  task-composer/
    SKILL.md
  task-suggestor/
    SKILL.md
README.md
```

## Skills 说明

### 1) task-composer
- 功能：将项目分解为多层级任务列表，包括持续时间、优先级和依赖关系
- 输入要求
- 项目描述
- 初始项目计划
- 输出 WBS 结构
- 输出要求
- 输出为 JSON
- 文本内容为英文
- `priority` 字段值为 `high|medium|low`
- 每个任务都有唯一的 ID

建议字段：
- 必需：项目名称
- 可选：时间线、团队规模、技术栈、里程碑

### 2) task-suggestor
- 功能：分析现有任务并返回结构化、可操作的任务优化建议。
- 输入要求
- 缺失任务建议
- 优化任务顺序
- 添加任务父子关系
- 输出要求
- 输出为 JSON
- 文本内容为英文
- 建议使用固定类别
- `confidence` 范围为 `0.0` 到 `1.0`

建议字段：
- 必需：当前任务计划
- 可选：希望改进的优化建议（如任务顺序等）

## 如何使用这些 Skills

在对话系统中使用 skills 时，正确写法是调用相应的 skill 来完成指定任务

示例：

```text
Use task-composer to build a project task tree for:
"Build a SaaS task management app for 3 developers in 8 weeks."
```

```text
Use task-suggestor to improve this task plan:
{ ...existing task json... }
Focus on missing dependencies and unrealistic durations.
```

## 输出格式约定和要求

每个 skill 需要遵循
- 输出必须是合法 JSON
- 可以包含 Markdown 注释
- 不应有额外输出信息
- 用户可见文本使用英文

不包含额外信息，skill 输出后无其他注释或解释

## 验收检查清单

开发人员在实现前应考虑以下验证：
- JSON 可解析
- 所有必需字段完整
- ID 唯一性验证
- `priority` 取值合法
- `confidence` 在 `0` 到 `1` 之间（仅适用于 `task-suggestor`）

## 已知注意事项

- `task-composer` 专注于从头开始创建详细的项目计划
- `task-suggestor` 专注于优化现有计划，发现结构中存在的问题
- 每个 skill 应严格按定义的大小写格式使用相应字段。

## Author

`LunaNeko` (`GitHub: lunaticlegacy`)
