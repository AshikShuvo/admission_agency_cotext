# Detailed Requirement Structure Guide
## Module Folder, EPIC File, Story File, and Task Plan Rules

This guide defines the expanded requirement structure used for implementation-agent routing.

## Folder Shape

Each module now has an independent folder under `requirements/modules/`:

```text
requirements/modules/{MODULE_ID}_{module_slug}/
├── index.md                  # module overview and complete file map
├── epics/                    # one file per EPIC
├── stories/                  # one file per user story
└── tasks/                    # one detailed implementation plan per FE/BE task
```

## Required Reading Order For Agents

1. `requirements/index.md`
2. `requirements/agent_map.md`
3. `requirements/module_index.md`
4. `requirements/modules/{MODULE_ID}_{module_slug}/index.md`
5. Target EPIC file
6. Target story file
7. Target task file

## File Responsibility

| File Type | Responsibility |
|---|---|
| Module `index.md` | Business goal, actors, source docs, business rules, dependency map, and links to all EPIC/story/task files. |
| EPIC file | Capability-level scope, business rules, story list, dependencies, EPIC acceptance criteria. |
| Story file | Detailed story expectation, actors, acceptance criteria, FE/BE task links, QA checklist. |
| Task file | Exact implementation plan, data/API/UI expectations, test plan, definition of done, handoff template. |

## Status Tracking

The expanded files keep local checkboxes, but `requirements/progress_tracker.md` remains the central rollup. A task is complete only after the task file, story file, module folder index, and progress tracker all reflect completion.

