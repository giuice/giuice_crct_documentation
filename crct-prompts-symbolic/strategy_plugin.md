# **CRCT Strategy Plugin **

╔═══════════════════════════════════════════════════════════╗
║                       STRATEGY                             ║
║                                                           ║
║  Identify  -->  Create     -->  Prioritize  -->  Decompose ║
║  Tasks         Instructions     Tasks          Complex Tasks║
╚═══════════════════════════════════════════════════════════╝

## ENTERING/EXITING THIS PHASE

**Enter if**:
- `.memorybankrules` shows `current_phase: "Strategy"`
- Transitioning from Setup/Maintenance

**Exit when**:
- HDTA documents (Domain Modules, Implementation Plans, Task Instructions) are created
- Dependencies are clearly defined
- Tasks are prioritized and ready for execution

**Exit action**:
```
[LAST_ACTION_STATE]
last_action: "Completed Strategy Phase - Tasks Planned"
current_phase: "Strategy"
next_action: "Phase Complete - User Action Required"
next_phase: "Execution"
```

## CONTEXT LOADING

1. Read core files:
   - `.memorybankrules`
   - `memory-bank/system_manifest.md`
   - `memory-bank/activeContext.md`
   - `memory-bank/module_relationship_tracker.md`
   - `memory-bank/changelog.md`
   - `memory-bank/progress.md`
   - `docs/doc_tracker.md`
   
2. Review `system_manifest.md` for system overview
3. Check dependency trackers for module relationships
4. Review `activeContext.md` for current state and priorities

## HDTA DOCUMENT CREATION

**Pre-Creation Checklist**:
- [ ] Document tier determined (Domain Module, Implementation Plan, or Task Instruction)
- [ ] Document name follows convention (see below)
- [ ] Document location is appropriate `memory-bank/tasks/`
- [ ] Existing document checked to avoid unnecessary overwrites

**Document Naming Conventions**:
- Domain Module: `{module_name}_module.md`
- Implementation Plan: `implementation_plan_{filename}.md`  
- Task Instruction: `T{number}_{task_name}.md` or `T{parent_number}_{parent_name}_ST{subtask_number}_{subtask_name}.md`

**Population Procedure**:
1. Use appropriate template from `memory-bank/templates/`
2. Fill in all sections completely
3. **Manual Dependency Linking (CRITICAL)**:
   - Link new Domain Modules in the `system_manifest.md`
   - Link Implementation Plans to Domain Modules
   - Link Task Instructions to Implementation Plans

## TASK INSTRUCTION CREATION

Create files with this structure:
```
# T{number}_{task_name} Instructions

## Objective
[Clear statement of purpose]

## Context
[Background information]

## Dependencies
[List of required modules/files with keys]

## Steps
1. [First step]
2. [Second step]
...

## Expected Output
[Description of deliverables]

## Notes
[Additional considerations]
```

For module-level tasks, include mini dependency tracker:
```
## Mini Dependency Tracker
[DEP_MATRIX_START]
# KEY DEFINITIONS
K1: module_name/file1.py
K2: module_name/file2.py

# MATRIX
    | K1 | K2 |
K1  | -  | >  |
K2  | <  | -  |
[DEP_MATRIX_END]
```

## TASK PRIORITIZATION

1. Review existing Task Instructions
2. Assess dependencies using trackers to identify prerequisites
3. Align with project objectives from `system_manifest.md`
4. Consider recent priorities from `activeContext.md`
5. Document prioritization in `activeContext.md` and update `progress.md`:
   ```
   ## Task Priorities
   1. T1_DatabaseSetup (Highest) - Required for all other tasks
   2. T2_UserAuthentication (High) - Security requirement
   3. T3_UIComponents (Medium) - Can be started in parallel
   ```

## RECURSIVE TASK DECOMPOSITION

For complex tasks:
1. Analyze complexity and scope
2. If too large, identify logical subtasks
3. Create subtask instruction files following naming convention:
   `T{parent_number}_{parent_name}_ST{subtask_number}_{subtask_name}.md`
4. Define dependencies between subtasks
5. Update parent task to reference subtasks
6. Document decomposition in `activeContext.md`

## DEPENDENCY OPERATIONS

Use these operations to maintain dependency tracking:
- `ADD_DEP(source, target, type)`: Add dependency
- `REMOVE_DEP(source, target, type)`: Remove dependency
- `ADD_MODULE(id, path)`: Add new module/file
- `REMOVE_MODULE(id)`: Remove obsolete module/file

## STRATEGY MUP

After creating/updating documents:
1. Update HDTA documents with proper cross-linking
2. Update `system_manifest.md` if needed
3. Update `activeContext.md` with:
   - Summary of planned tasks
   - List of instruction locations
   - Task priorities and reasoning
4. Update `progress.md` with new tasks
5. Update `.memorybankrules`:
   ```
   [LAST_ACTION_STATE]
   last_action: "[description of completed action]"
   current_phase: "Strategy"
   next_action: "[next action to take]"
   next_phase: "Strategy"
   ```

## CHECKPOINTS BEFORE TRANSITION

[TRANSITION_CHECKLIST]
[ ] All identified tasks have instruction files
[ ] All instruction files have complete sections
[ ] Dependencies are clearly specified
[ ] Task priorities are documented
[ ] Complex tasks are decomposed if needed
[ ] `.memorybankrules` updated with next_phase: "Execution"
[/TRANSITION_CHECKLIST]

## MUP VERIFICATION FORMAT

After every action, include:

[MUP_VERIFICATION]
[X] 1. Updated activeContext.md with: [brief description]
[X] 2. Updated changelog.md: [Yes/No + reason]
[X] 3. Updated `.memorybankrules` with last_action: [action description]
[X] 4. Updated HDTA documents: [Yes/No + which ones]
[X] 5. Task instructions follow naming convention: [Yes/No + details]
[X] 6. Dependencies clearly specified: [Yes/No + details]
[X] 7. Task priorities documented: [Yes/No + details]
[/MUP_VERIFICATION]