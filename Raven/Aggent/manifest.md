# MANIFEST

## FILES

| File               | Role                                     | Required                                |
| :----------------- | :--------------------------------------- | :-------------------------------------- |
| Instructions.md    | Base layer for all conversations         | Always                                  |
| Core-Principles.md | Anti-slop and balance principles         | For design, engineering, workflow, VNPC |
| Design-Core.md     | UI/UX, folder structure, algorithm rules | For design tasks, VNPC evaluate         |
| Output-Format.md   | Response shape rules                     | For design, workflow, VNPC              |
| Workflow-Core.md   | Phases, modes, artifacts, changelog      | For workflow tasks                      |
| VNPC-Agent.md      | VNPC format, tree, verification point    | For VNPC tasks                          |

## COMBINATIONS

| Task             | Files to load, in order                                                                                     |
| :--------------- | :---------------------------------------------------------------------------------------------------------- |
| Any conversation | Instructions.md                                                                                             |
| Design task      | Instructions.md → Core-Principles.md → Design-Core.md → Output-Format.md                                    |
| Workflow task    | Instructions.md → Core-Principles.md → Workflow-Core.md → Output-Format.md                                  |
| VNPC describe    | Instructions.md → Core-Principles.md → VNPC-Agent.md → Output-Format.md                                     |
| VNPC evaluate    | Instructions.md → Core-Principles.md → Design-Core.md → VNPC-Agent.md → Output-Format.md                    |
| Full project     | Instructions.md → Core-Principles.md → Design-Core.md → Output-Format.md → Workflow-Core.md → VNPC-Agent.md |

## RULES

1. Load files in the order listed for the selected combination.

2. If any required file is missing, reply: "Missing file: [name]." and stop.

3. If the task spans more than one combination, use the Full project combination.

4. Do not load files outside the selected combination unless the user requests it.
