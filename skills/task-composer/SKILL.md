---
name: task-composer
description: Generate a hierarchical project task tree with duration, priority, dependencies, and strict JSON output in English only.
---

## When to use
Use this skill when the user asks to:
- decompose a project into tasks/WBS
- create a project plan tree
- estimate task duration a:contentReference[oaicite:12]{index=12}tialize project tasks from a project description

Do NOT u:contentReference[oaicite:13]{index=13}code generation unrelated to planning
- generic Q&A without project/task context

## Input contract
The user input should include:
- project description (required)
- optional constraints (timeline, team size, tech stack, milestones)

## Procedure
1. Parse and understand the project description.
2. Identify major project phases.
3. Break each phase into actionable subtasks.
4. Estimate task duration.
5. Assign priority levels (`high`, `medium`, `low`).
6. Define dependencies among tasks.
7. Build a task tree (parent-child hierarchy).
8. Ensure all user-facing text is English.

## Output requirements
- Output MUST be valid JSON only.
- No Markdown, no code fences, no commentary.
- Keep schema keys exactly as defined.
- Ensure dependencies refer to existing task IDs.
- Ensure root-level tasks use `parentId: null`.
- If information is missing, infer reasonable defaults and proceed.

## JSON schema (target shape)
{
  "projectName": "string",
  "description": "string",
  "tasks": [
    {
      "id": "string",
      "name": "string",
      "description": "string",
      "parentId": "string|null",
      "duration": "string",
      "priority": "high|medium|low",
      "dependencies": ["string"],
      "status": "string"
    }
  ]
}
    
## Quality checks before returning
- JSON parseable
- all required keys present
- priority values are valid
- dependency IDs exist in tasks
- hierarchy has no orphan nodes
