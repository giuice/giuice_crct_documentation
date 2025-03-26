# Simplified CRCT System: Quick Start Guide

This guide will walk you through setting up and using the simplified JSON-based CRCT system with VS Code and an AI assistant.

## 1. Initial Setup

### Create Core Files

First, create the essential files for the system:

1. Create `.memory_bankrules.json` in your project root:
   ```json
   {
     "lastActionState": {
       "lastAction": "System Initialized",
       "currentPhase": "Set-up/Maintenance",
       "nextAction": "Initialize Core Files",
       "nextPhase": "Set-up/Maintenance"
     },
     "codeRootDirectories": [],
     "learningJournal": [
       "memory_bank Project initialized on [current date]."
     ]
   }
   ```

2. Create a `memory_bank_docs` directory and add these files:
   - `projectbrief.md`: Define your project mission and goals
   - `productContext.md`: Explain the product purpose and user needs
   - `activeContext.md`: Track your project's current state
   - `changelog.md`: Log changes to your codebase
   - `dependencies.json`: Track dependencies between files
     ```json
     {
       "moduleRelationships": {},
       "fileRelationships": {},
       "documentationRelationships": {}
     }
     ```

3. Create a `memory_bank_docs/prompts` directory and add the three plugin files:
   - `setup_maintenance_plugin.md`
   - `strategy_plugin.md`
   - `execution_plugin.md`

## 2. Workflow Example

Let's walk through a simple example project - creating a basic weather API.

### Phase 1: Setup/Maintenance

1. **Start by reading `.memory_bankrules.json`** to confirm you're in Setup/Maintenance phase.

2. **Identify code root directories**:
   - Scan project folders to identify where code should live
   - Add to `codeRootDirectories` in `.memory_bankrules.json`:
     ```json
     "codeRootDirectories": ["src", "tests"]
     ```

3. **Create basic directory structure**:
   ```
   src/
   ├── api/
   ├── models/
   ├── services/
   └── utils/
   tests/
   ```

4. **Initialize dependency tracking**:
   - Add the directories to `dependencies.json`:
     ```json
     {
       "moduleRelationships": {
         "src": {
           "depends_on": [],
           "depended_by": ["tests"],
           "description": "Source code directory"
         },
         "tests": {
           "depends_on": ["src"],
           "depended_by": [],
           "description": "Test directory"
         }
       },
       "fileRelationships": {},
       "documentationRelationships": {}
     }
     ```

5. **Update `.memory_bankrules.json` to move to Strategy phase**:
   ```json
   {
     "lastActionState": {
       "lastAction": "Completed Setup/Maintenance Phase",
       "currentPhase": "Set-up/Maintenance",
       "nextAction": "Phase Complete - User Action Required",
       "nextPhase": "Strategy"
     },
     "codeRootDirectories": ["src", "tests"],
     "learningJournal": [
       "memory_bank Project initialized on [date].",
       "Completed initial setup with src and tests as code roots."
     ]
   }
   ```

### Phase 2: Strategy

1. **Read `.memory_bankrules.json`** to confirm you're in Strategy phase.

2. **Create a strategy_tasks directory** to store instruction files.

3. **Create a task instruction file** for the weather service:
   ```
   # WeatherService Instructions

   ## Objective
   Create a service for fetching and processing weather data from an external API.

   ## Context
   We need a reliable way to fetch weather data for our application.

   ## Dependencies
   - src/utils/http.js (HTTP request utility)
   - src/models/weather.js (Weather data model)

   ## Steps
   1. Create src/services/weatherService.js with getForecast method
   2. Implement error handling for API failures
   3. Add data transformation to convert API response to our model
   4. Create unit tests

   ## Expected Output
   - src/services/weatherService.js
   - tests/services/weatherService.test.js

   ## Notes
   - Use environment variables for API keys
   - Consider caching to reduce API calls
   ```

4. **Add files to dependencies.json**:
   ```json
   "fileRelationships": {
     "src/utils/http.js": {
       "depends_on": [],
       "depended_by": ["src/services/weatherService.js"],
       "description": "HTTP request utility"
     },
     "src/models/weather.js": {
       "depends_on": [],
       "depended_by": ["src/services/weatherService.js"],
       "description": "Weather data model"
     },
     "src/services/weatherService.js": {
       "depends_on": ["src/utils/http.js", "src/models/weather.js"],
       "depended_by": ["tests/services/weatherService.test.js"],
       "description": "Weather service for API integration"
     },
     "tests/services/weatherService.test.js": {
       "depends_on": ["src/services/weatherService.js"],
       "depended_by": [],
       "description": "Tests for weather service"
     }
   }
   ```

5. **Create other task instruction files** as needed.

6. **Prioritize tasks** and update `activeContext.md` with the priority list.

7. **Update `.memory_bankrules.json` to move to Execution phase**:
   ```json
   {
     "lastActionState": {
       "lastAction": "Completed Strategy Phase - Tasks Planned",
       "currentPhase": "Strategy",
       "nextAction": "Phase Complete - User Action Required",
       "nextPhase": "Execution"
     }
   }
   ```

### Phase 3: Execution

1. **Read `.memory_bankrules.json`** to confirm you're in Execution phase.

2. **Read the task instruction file** to understand what needs to be done.

3. **Execute each step sequentially**:

   **Step 1: Create weatherService.js**
   
   - Pre-Action Verification: Check if file exists (it shouldn't yet)
   - Create the file with initial content:
     ```javascript
     // src/services/weatherService.js
     const httpClient = require('../utils/http');
     const WeatherModel = require('../models/weather');
     
     class WeatherService {
       constructor(apiKey) {
         this.apiKey = apiKey;
         this.baseUrl = 'https://api.weatherapi.com/v1';
       }
       
       async getForecast(location, days = 3) {
         try {
           const response = await httpClient.get(
             `${this.baseUrl}/forecast.json`,
             { key: this.apiKey, q: location, days }
           );
           
           return this._transformForecast(response);
         } catch (error) {
           console.error('Weather API error:', error);
           throw new Error('Failed to fetch weather forecast');
         }
       }
       
       _transformForecast(apiResponse) {
         // Transform API response to our model format
         return new WeatherModel({
           location: apiResponse.location.name,
           current: {
             temp: apiResponse.current.temp_c,
             condition: apiResponse.current.condition.text,
             humidity: apiResponse.current.humidity
           },
           forecast: apiResponse.forecast.forecastday.map(day => ({
             date: day.date,
             maxTemp: day.day.maxtemp_c,
             minTemp: day.day.mintemp_c,
             condition: day.day.condition.text
           }))
         });
       }
     }
     
     module.exports = WeatherService;
     ```
   
   - Document Results: "Created weatherService.js with basic functionality"
   - Update Dependencies: Confirm dependencies in dependencies.json
   - MUP: Update .memory_bankrules.json, activeContext.md, changelog.md

   **Repeat for steps 2-4**

4. **Validate the completed task**:
   - Check that all files were created
   - Verify the code meets the requirements
   - Add a summary to activeContext.md

5. **Update `.memory_bankrules.json` to complete the phase**:
   ```json
   {
     "lastActionState": {
       "lastAction": "Completed Execution Phase - Weather Service Implemented",
       "currentPhase": "Execution",
       "nextAction": "Phase Complete - User Action Required",
       "nextPhase": "Strategy"
     }
   }
   ```

## 3. The Recursive Process

The power of CRCT lies in its recursive approach to complex tasks:

1. **Identifying the Need for Recursion**:
   - During execution, you might realize a step is too complex
   - This triggers the creation of a subtask
   - The parent task is temporarily paused

2. **Creating a Subtask**:
   - Create a subtask instruction file with explicit reference to the parent task
   - Document the subtask relationship in `dependencies.json`
   - Add note in parent task about the recursive step

3. **Recursive Execution**:
   - Apply the full chain-of-thought loop to the subtask:
     - Load context specific to the subtask
     - Check dependencies for the subtask
     - Plan the subtask steps in detail
     - Execute the subtask steps
     - Update dependencies and state tracking
     - Apply MUP for the subtask

4. **Returning to the Parent Task**:
   - Once subtask is complete, return to the parent task
   - Continue execution from where you left off
   - Update parent task with subtask results

**Example**: Weather API Transformation Subtask

1. **Parent task step that triggers recursion**:
   ```
   Step 3: Implement data transformation to convert API response to our model
   Note: This step requires creating a subtask (recursive processing)
   ```

2. **Create subtask instruction file**:
   ```
   # WeatherTransformation Instructions

   ## Objective
   Create utility functions to transform external API data to our internal model.

   ## Context
   This is a subtask of WeatherService Instructions, created during execution of Step 3.
   Parent task is temporarily paused while this subtask is processed.

   ## Dependencies
   - src/models/weather.js
   - src/utils/dateUtils.js

   ## Steps
   1. Create src/utils/weatherTransformer.js with basic structure
   2. Implement transformation for current weather data
   3. Implement transformation for forecast data
   4. Add error handling for malformed API responses

   ## Expected Output
   - src/utils/weatherTransformer.js
   - tests/utils/weatherTransformer.test.js
   ```

3. **Document in `dependencies.json`**:
   ```json
   "taskRelationships": {
     "WeatherService": {
       "files": ["src/services/weatherService.js"],
       "subtasks": ["WeatherTransformation"],
       "depends_on": [],
       "depended_by": []
     },
     "WeatherTransformation": {
       "parent_task": "WeatherService",
       "files": ["src/utils/weatherTransformer.js"],
       "depends_on": [],
       "depended_by": []
     }
   }
   ```

4. **Update `activeContext.md`**:
   ```markdown
   # Active Context

   ## Current State
   Executing WeatherService task - temporarily paused at Step 3
   Currently executing WeatherTransformation subtask (recursive processing)
   ```

5. **Process subtask using the full chain-of-thought loop**:
   - Load context for the subtask
   - Check dependencies
   - Develop detailed reasoning about the transformations
   - Create and implement the transformer code
   - Document results
   - Apply MUP

6. **Update parent task after subtask completion**:
   ```
   # WeatherService Instructions

   ## Steps
   ...
   3. ✅ Implement data transformation to convert API response to our model
      Note: Completed via WeatherTransformation subtask
      Result: Created src/utils/weatherTransformer.js with transformation functions
   4. Create unit tests
   ...
   ```

7. **Continue with parent task execution**

## 4. Best Practices

1. **Keep files organized**:
   - Store instruction files in strategy_tasks/
   - Use a consistent naming convention

2. **Update dependencies frequently**:
   - Add new files to dependencies.json as they're created
   - Keep dependencies accurate to aid in future planning

3. **Detailed documentation**:
   - Record decisions and reasoning in activeContext.md
   - Use the learningJournal in .memory_bankrules.json for project insights

4. **Verify before acting**:
   - Always check file state before modifying
   - Use Pre-Action Verification to avoid errors

5. **Follow the MUP after every step**:
   - Update activeContext.md
   - Update changelog.md
   - Update .memory_bankrules.json
   - Update dependencies.json