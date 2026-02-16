---
name: task-suggestor
description: Analyze existing project tasks and return structured, actionable task recommendations in strict JSON and English only.
---

## When to use
Use this skill when the user asks to:
- improve/adjust an existing task plan
- suggest missing tasks
- optimize dependencies or sequence
- refine durations or parent-child structure

Do NOT use this skill for:
- creating a full task tree from scratch (use task-composer)
- unrelated coding/debugging tasks

## Input contract
User/context should provide:
- current project/task data
- user query about planning improvements

## Procedure
1. Parse the user query intent.
2. Analyze current task structure and relationships.
3. Produce targeted suggestions across:
   - createTask
   - parentTaskSuggestion
   - dependencySuggestion
   - sequenceSuggestion
   - durationSuggestion
4. For each suggestion, provide rationale and confidence.
5. Include `taskSchema` only when proposing a concrete new task object.
6. Keep all user-facing text in English.

## Output requirements
- Output MUST be valid JSON only.
- No Markdown, no code fences, no extra commentary.
- Keep categories and keys exactly as specified.
- Confidence should be a normalized numeric score (0.0 to 1.0).

## JSON schema (target shape)
{
  "query": "string",
  "suggestions": {
    "createTask": [
      {
        "type": "createTask",
        "title": "string",
        "description": "string",
        "rationale": "string",
        "confidence": 0.0,
        "taskSchema": {
          "name": "string",
          "description": "string",
          "parentId": "string|null",
          "duration": "string",
          "priority": "high|medium|low",
          "dependencies": ["string"]
        }
      }
    ],
    "parentTaskSuggestion": [
      {
        "type": "parentTaskSuggestion",
        "title": "string",
        "description": "string",
        "rationale": "string",
        "confidence": 0.0
      }
    ],
    "dependencySuggestion": [
      {
        "type": "dependencySuggestion",
        "title": "string",
        "description": "string",
        "rationale": "string",
        "confidence": 0.0
      }
    ],
    "sequenceSuggestion": [
      {
        "type": "sequenceSuggestion",
        "title": "string",
        "description": "string",
        "rationale": "string",
        "confidence": 0.0
      }
    ],
    "durationSuggestion": [
      {
        "type": "durationSuggestion",
        "title": "string",
        "description": "string",
        "rationale": "string",
        "confidence": 0.0
      }
    ]
  }
}

## Quality checks before returning
- JSON parseable
- category names are exact
- suggestion `type` matches category
- confidence in [0,1]
- no empty rationale
