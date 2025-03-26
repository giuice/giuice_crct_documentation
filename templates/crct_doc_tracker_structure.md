# Documentation Dependency Tracker

[DEP_MATRIX_START]
# KEY DEFINITIONS
D1: memory-bank/prompts/crct_core_prompt.md
D2: memory-bank/prompts/setup_plugin.md
D3: memory-bank/prompts/strategy_plugin.md
D4: memory-bank/prompts/execution_plugin.md
D5: memory-bank/projectbrief.md
D6: memory-bank/productContext.md
D7: memory-bank/activeContext.md
D8: memory-bank/dependency_tracker.md
D9: docs/doc_tracker.md
D10: memory-bank/changelog.md
D11: memory-bank/progress.md
D12: memory-bank/tasks/task_template.md
D13: memory-bank/tasks/subtask_template.md
D14: memory-bank/tasks/module_template.md
D15: .memory-bank-rules

# MATRIX (Row depends on Column)
# Symbols: > (depends on), < (depended by), x (mutual), - (none), d (doc)
     | D1 | D2 | D3 | D4 | D5 | D6 | D7 | D8 | D9 | D10| D11| D12| D13| D14| D15|
D1   | -  | <  | <  | <  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | >  |
D2   | >  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | >  |
D3   | >  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | >  | >  | >  | >  |
D4   | >  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | >  | >  | >  | >  |
D5   | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  |
D6   | -  | -  | -  | -  | >  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  |
D7   | -  | -  | -  | -  | >  | >  | -  | >  | -  | >  | >  | -  | -  | -  | >  |
D8   | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  |
D9   | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  |
D10  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  |
D11  | -  | -  | -  | -  | >  | -  | >  | -  | -  | >  | -  | -  | -  | -  | >  |
D12  | >  | -  | >  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  |
D13  | >  | -  | >  | -  | -  | -  | -  | -  | -  | -  | -  | >  | -  | -  | -  |
D14  | >  | -  | >  | -  | -  | -  | -  | >  | -  | -  | -  | -  | -  | -  | -  |
D15  | >  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  | -  |
[DEP_MATRIX_END]

## Purpose
This tracker monitors dependencies between all documentation and configuration files in the CRCT system. It ensures proper updating of related files when changes are made.

## File Descriptions

### Core System Files
- D1: Core system prompt defining the CRCT framework
- D2: Setup/Maintenance phase plugin
- D3: Strategy phase plugin
- D4: Execution phase plugin
- D15: Phase management and configuration file

### Project Context Files
- D5: Project mission and objectives
- D6: Product context and user needs
- D7: Current state and decisions tracker
- D10: Changelog of significant modifications
- D11: Overall project progress tracker

### Dependency Management
- D8: Module-level dependency tracker
- D9: Documentation dependency tracker (this file)

### Task Templates
- D12: Main task template
- D13: Subtask template
- D14: Module-specific task template

## Dependency Key
- > : Row depends on column (changes to column affects row)
- < : Column depends on row (changes to row affects column)
- x : Mutual dependency (changes to either affects both)
- - : No dependency
- d : Direct code reference

## Update Procedure
When modifying any file, check its row to identify which other files might need updates.