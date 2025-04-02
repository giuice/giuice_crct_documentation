# **CRCT Setup/Maintenance Plugin **

╔═══════════════════════════════════════════════╗
║              SETUP/MAINTENANCE                ║
║                                               ║
║  Initialize  -->  Identify  -->  Populate     ║
║  Core Files      Code Roots    Trackers       ║
╚═══════════════════════════════════════════════╝

## ENTERING/EXITING THIS PHASE

**Enter if**:
- `.memorybankrules` shows `current_phase: "Setup/Maintenance"`
- `.memorybankrules` is missing (initial setup)

**Exit when**:
- All core files exist and are initialized
- Code root directories are identified 
- Dependency trackers are populated with no placeholders
- `system_manifest.md` is created
- Mini-trackers are created/populated as needed

**Exit action**:
```
[LAST_ACTION_STATE]
last_action: "Completed Setup/Maintenance Phase"
current_phase: "Setup/Maintenance"
next_action: "Phase Complete - User Action Required"
next_phase: "Strategy"
```

## CORE FILE INITIALIZATION

**Required files**:
- `.memorybankrules`: Phase management
- `memory-bank/system_manifest.md`: Project overview
- `memory-bank/activeContext.md`: Current state
- `memory-bank/module_relationship_tracker.md`: Module dependencies
- `memory-bank/changelog.md`: Change log
- `memory-bank/progress.md`: Progress tracking
- `docs/doc_tracker.md`: Documentation dependencies

**Creation procedure**:
1. Check if each file exists
2. For missing files, create with basic templates:
   - For `.memorybankrules`:
     ```
     [LAST_ACTION_STATE]
     last_action: "System Initialized"
     current_phase: "Setup/Maintenance"
     next_action: "Initialize Core Files"
     next_phase: "Setup/Maintenance"
     
     [CODE_ROOT_DIRECTORIES]
     - [list to be populated]
     
     [DOC_DIRECTORIES]
     - docs
     
     [LEARNING_JOURNAL]
     - Initial setup on [current date]
     ```
   - For `system_manifest.md`: Use template from `memory-bank/templates/`
   - For other files: Create with appropriate headers

## CODE ROOT IDENTIFICATION

1. Scan project root directory
2. **Include directories** with:
   - Source code files (.py, .js, etc.)
   - Project-specific logic
   
3. **Exclude directories** like:
   - `.git`, `.vscode` (configuration)
   - `venv`, `node_modules` (dependencies)
   - `build`, `dist` (outputs)
   - `docs` (documentation)

4. Update `.memorybankrules`:
   ```
   [CODE_ROOT_DIRECTORIES]
   - src
   - utils
   - [other identified directories]
   ```

## DEPENDENCY TRACKER CREATION

1. Create tracker structure:
   ```
   [DEP_MATRIX_START]
   # KEY DEFINITIONS
   K1: src/module_a
   K2: src/module_b
   
   # MATRIX (Row depends on Column)
   # Symbols: > (depends on), < (depended by), x (mutual), - (none), d (doc)
       | K1 | K2 |
   K1  | -  | >  |
   K2  | <  | -  |
   [DEP_MATRIX_END]
   ```

2. For each dependency:
   - Use `ADD_DEP(source, target, type)` to add new dependencies
   - Use `REMOVE_DEP(source, target, type)` to remove incorrect dependencies
   - Use `ADD_MODULE(id, path)` to add newly discovered modules
   - Use `REMOVE_MODULE(id)` to remove obsolete modules

3. Ensure the following:
   - All module-to-module dependencies are recorded
   - Documentation dependencies are recorded in `doc_tracker.md`
   - Mini-trackers for module-specific dependencies are created

## SETUP/MAINTENANCE MUP

After each significant action:
1. Update `activeContext.md` with action and results
2. Update `changelog.md` if files were created or modified
3. Update `.memorybankrules`:
   ```
   [LAST_ACTION_STATE]
   last_action: "[description of completed action]"
   current_phase: "Setup/Maintenance"
   next_action: "[next action to take]"
   next_phase: "Setup/Maintenance"
   ```
4. Update `system_manifest.md` if project structure changes
5. Check if phase transition criteria are met

## CHECKPOINTS BEFORE TRANSITION

[TRANSITION_CHECKLIST]
[ ] All required files exist
[ ] Code roots identified and added to `.memorybankrules`
[ ] `module_relationship_tracker.md` populated with dependencies
[ ] `doc_tracker.md` created and populated
[ ] `system_manifest.md` created using template
[ ] `.memorybankrules` updated with next_phase: "Strategy"
[/TRANSITION_CHECKLIST]

## MUP VERIFICATION FORMAT

After every action, include:

[MUP_VERIFICATION]
[X] 1. Updated activeContext.md with: [brief description]
[X] 2. Updated changelog.md: [Yes/No + reason]
[X] 3. Updated `.memorybankrules` with last_action: [action description]
[X] 4. Updated relevant HDTA files: [Yes/No + which ones]
[X] 5. Verified all changes
[X] 6. Code root directories identified: [Yes/No/NA + details]
[X] 7. Dependency trackers populated: [Yes/No/NA + details]
[/MUP_VERIFICATION]