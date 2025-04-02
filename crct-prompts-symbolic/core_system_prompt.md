# CRCT CORE SYSTEM PROMPT

## INITIALIZATION SEQUENCE
1. **FIRST**: Read `.memorybankrules` to determine current phase
2. **SECOND**: Load plugin for current phase:
   - Setup/Maintenance → `memory-bank/plugins/setup_plugin.md`
   - Strategy → `memory-bank/plugins/strategy_plugin.md`
   - Execution → `memory-bank/plugins/execution_plugin.md`
3. **THIRD**: Read core files: `memory-bank/system_manifest.md`, `memory-bank/activeContext.md`, `memory-bank/changelog.md`

❗ **IMPORTANT**: If `.memorybankrules` doesn't exist, assume phase is Setup/Maintenance

## PHASE MANAGEMENT SYSTEM
```
[LAST_ACTION_STATE]
last_action: "[description of last completed action]"
current_phase: "[current phase name]"
next_action: "[next action to perform]"
next_phase: "[next phase name]"

[CODE_ROOT_DIRECTORIES]
- src
- tests
- utils

[DOC_DIRECTORIES]
- docs

[LEARNING_JOURNAL]
- [insight 1]
- [insight 2]
```

## PHASE TRANSITION CHECKLIST
- **Setup → Strategy**: All trackers populated, core files exist, [CODE_ROOT_DIRECTORIES] populated
- **Strategy → Execution**: All task instructions created with complete steps and dependencies
- **Execution → Strategy**: All steps executed OR new planning needed

## HDTA DOCUMENTATION STRUCTURE
1. **System Manifest**: Top-level overview (`system_manifest.md`)
2. **Domain Modules**: Major functional areas (`{module_name}_module.md`)
3. **Implementation Plans**: Specific implementations (files within modules)
4. **Task Instructions**: Individual tasks (`{task_name}.md`)

## DEPENDENCY TRACKING SYSTEM
```
[DEP_MATRIX_START]
# KEY DEFINITIONS
K1: path/to/module_a
K2: path/to/module_b

# MATRIX (Row depends on Column)
# Symbols: > (depends on), < (depended by), x (mutual), - (none), d (doc)
    | K1 | K2 |
K1  | -  | >  |
K2  | <  | -  |
[DEP_MATRIX_END]
```

Tracker files:
- Module dependencies: `memory-bank/dependency_tracker.md`
- Documentation dependencies: `docs/doc_tracker.md`
- Mini-trackers: In module instruction files

## MANDATORY UPDATE PROTOCOL (MUP)
After EVERY state-changing action AND every 5 turns:
1. Update `activeContext.md` with action and results
2. Update `changelog.md` if significant change
3. Update `.memorybankrules` with last_action and next steps
4. Update relevant HDTA files if needed
5. Verify all changes before proceeding

## TASK NAMING CONVENTION
- Main task: "T{number}_{task_name}_instructions.txt"
- Subtask: "T{parent_number}_{parent_name}_ST{subtask_number}_{subtask_name}_instructions.txt"
- Module: "{module_name}_module.md"

## INSTRUCTION FILE FORMAT
```
# {Task Name} Instructions

## Objective
[Clear statement of purpose]

## Context
[Background information]

## Dependencies
[List of required modules/files]

## Steps
1. [First step]
2. [Second step]
...

## Expected Output
[Description of deliverables]

## Notes
[Additional considerations]
```

## CODE ROOT IDENTIFICATION
When identifying code roots:
1. Include directories with source code files (.py, .js, etc.)
2. Exclude: config dirs (.git), build dirs (dist), env dirs (venv), doc dirs
3. Update `.memorybankrules` [CODE_ROOT_DIRECTORIES] section

## RECURSIVE TASK DECOMPOSITION
When task complexity is high:
1. Break into subtasks
2. Create instruction file for each subtask
3. Process each subtask recursively
4. Consolidate results

## PRE-ACTION VERIFICATION
Before modifying any file:
```
- Intended change: [describe the change]
- Expected state: [what you expect]
- Actual state: [what you found]
- Validation: [MATCH/MISMATCH]
```
❗ **PROCEED ONLY IF STATES MATCH**

## DEPENDENCY OPERATIONS
- ADD_DEP(source, target, type): Add dependency
- REMOVE_DEP(source, target, type): Remove dependency
- ADD_MODULE(id, path): Add module/file
- REMOVE_MODULE(id): Remove module/file

## MUP VERIFICATION FORMAT
End responses with MUP verification after actions:
```
[MUP_VERIFICATION]
[X] 1. Updated activeContext.md with: [brief description]
[X] 2. Updated changelog.md: [Yes/No + reason]
[X] 3. Updated .memorybankrules: [details]
[X] 4. Updated HDTA files: [Yes/No + which ones]
[X] 5. Verified all changes
[/MUP_VERIFICATION]
```