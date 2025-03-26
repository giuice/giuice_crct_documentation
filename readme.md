# CRCT Simplified Framework

A lightweight, AI-friendly implementation of the Cline Recursive Chain-of-Thought (CRCT) system optimized for GitHub Copilot and other AI assistants.

## Overview

CRCT Simplified Framework provides a structured approach to manage complex projects through AI-assisted development. It organizes work into distinct phases with clear transitions, tracks dependencies through an intuitive matrix format, and ensures consistent state management through mandatory update protocols. All the credits go to [lloydchang](https://github.com/lloydchang/RPG-fan-Cline-Recursive-Chain-of-Thought-System-CRCT-) , I'm just trying compressed and symbolic versions to play with less capable IA's.

### Key Features

- **Phase-Based Workflow**: Distinct Setup/Maintenance, Strategy, and Execution phases
- **Simplified Dependency Tracking**: Visual matrix-based dependency tracking
- **Universal MUP (Mandatory Update Protocol)**: Ensures consistent state management
- **Recursive Task Decomposition**: Breaks complex tasks into manageable subtasks
- **AI-Optimized Formatting**: Works effectively across different AI capabilities

## Getting Started

### Prerequisites

- GitHub Copilot or similar AI assistant
- A version control system (e.g., Git)
- A text editor

### Basic Setup

1. **Create the initial directory structure**:

```
your-project/
├── memory-bank/
│   ├── plugins/
│   ├── activeContext.md
│   ├── changelog.md
│   ├── dependency_tracker.md
│   ├── productContext.md
│   └── projectbrief.md
├── docs/
│   └── doc_tracker.md
└── .memory-bank-rules
```

2. **Initialize core files**:
Using the [templates](templates) folder: 
- Copy the `.memory-bank-rules` template from the [Core System Prompt](crct-prompts-symbolic/core_system_prompt.md)
- Create basic `projectbrief.md` with your project's mission and objectives
- Copy empty `activeContext.md`, `changelog.md`, `progress.md`and other core files 

1. **Set up plugin files**:
- Set you system prompt with [Core System Prompt](crct-prompts-symbolic/core_system_prompt.md)
  - In github copilot create `.github`folder and save core system prompt instructions with the name copilot-instructions.md
- Copy [Setup/Maintenance Plugin](crct-prompts-symbolic/setup-plugin.md) to `memory-bank/plugins/setup_plugin.md`
- Copy [Strategy Plugin](crct-prompts-symbolic/strategy_plugin.md) to `memory-bank/plugins/strategy_plugin.md`
- Copy [Execution Plugin](crct-prompts-symbolic/execution-plugin.md) to `memory-bank/plugins/execution_plugin.md`

## Using with GitHub Copilot

### Initial Prompt

Start by instructing GitHub Copilot about the system. Provide this initial prompt:

```
I'm using the CRCT Simplified Framework to manage this project. Please help me follow the protocols defined in the core system prompt. First, read the .memory-bank-rules file to determine the current phase, then load the corresponding plugin from memory-bank/plugins/.
```

### Phase-Specific Instructions

For each phase, provide clear instructions based on the current phase:

#### Setup/Maintenance

```
We're in the Setup/Maintenance phase of CRCT. Please help me initialize the core files and identify code root directories according to the setup_plugin.md guidelines.
```

#### Strategy

```
We're in the Strategy phase of CRCT. Help me create instruction files for the next tasks following the naming convention and format in strategy_plugin.md.
```

#### Execution

```
We're in the Execution phase of CRCT. Let's execute the steps in [task_file] with proper pre-action verification and documentation as defined in execution_plugin.md.
```

### Reminding About MUP

If Copilot forgets to complete the MUP:

```
Please complete the Mandatory Update Protocol (MUP) before continuing, following the checklist format.
```

## Core Components

### 1. Phase Management

Phases are managed in `.memory-bank-rules` with a clear marker structure:

```
[PHASE_MARKER]
CURRENT: Strategy
NEXT: Execution
LAST_ACTION: Created task breakdown
REQUIRED_BEFORE_TRANSITION: Complete all task instruction files
[/PHASE_MARKER]
```

### 2. Dependency Tracker

Dependencies use an intuitive matrix format:

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

### 3. Mandatory Update Protocol (MUP)

The MUP ensures consistent state management:

```
[MUP_VERIFICATION]
[X] 1. Updated activeContext.md with: Added new task structure
[X] 2. Updated changelog.md: Yes - Added entry for database schema change
[X] 3. Updated phase marker with last_action: Completed database schema
[X] 4. Verified next action is correct: Implement data access layer
[X] 5. Checked if phase transition is needed: No - more tasks remaining
[/MUP_VERIFICATION]
```

### 4. Task Naming Convention

```
- Main task: "T{number}_{task_name}_instructions.txt"
- Subtask: "T{parent_number}_{parent_name}_ST{subtask_number}_{subtask_name}_instructions.txt"
- Module: "{module_name}_main_instructions.txt"
```

## Best Practices

1. **Consistency**: Always use the same format for files and updates
2. **Verification**: Complete all verification steps before making changes
3. **MUP Discipline**: Always complete the MUP verification after changes
4. **Small Steps**: Break work into small, manageable steps
5. **Clear Communication**: Use consistent terms from the framework

## Troubleshooting

### Common Issues with AI Assistants

1. **MUP Forgetting**: Remind the AI about the MUP checklist if it's skipped
2. **Format Drift**: Copy/paste the correct format template as needed
3. **Phase Confusion**: Explicitly state the current phase before instructions
4. **Task Naming**: Provide examples of correct task naming when needed

## Example Workflow

1. **Start in Setup Phase**:
   - Initialize core files
   - Identify code root directories
   - Create initial dependency trackers

2. **Transition to Strategy Phase**:
   - Create task instruction files
   - Prioritize tasks
   - Decompose complex tasks

3. **Move to Execution Phase**:
   - Execute steps with verification
   - Document results
   - Update dependency trackers

4. **Return to Strategy Phase**:
   - Plan next cycle of tasks
   - Reprioritize based on progress

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- Based on the Cline Recursive Chain-of-Thought System (CRCT)
- Optimized for improved AI compatibility and token efficiency