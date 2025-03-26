# Module Dependency Tracker

[DEP_MATRIX_START]
# KEY DEFINITIONS
M1: src/core
M2: src/utils
M3: src/api
M4: src/database
M5: src/ui
M6: src/auth
M7: tests/core
M8: tests/api

# MATRIX (Row depends on Column)
# Symbols: > (depends on), < (depended by), x (mutual), - (none), d (doc)
    | M1 | M2 | M3 | M4 | M5 | M6 | M7 | M8 |
M1  | -  | >  | -  | -  | -  | -  | <  | -  |
M2  | -  | -  | -  | -  | -  | -  | -  | -  |
M3  | >  | >  | -  | >  | -  | >  | -  | <  |
M4  | -  | >  | -  | -  | -  | -  | -  | -  |
M5  | >  | >  | >  | -  | -  | >  | -  | -  |
M6  | >  | >  | -  | >  | -  | -  | -  | -  |
M7  | >  | -  | -  | -  | -  | -  | -  | -  |
M8  | -  | -  | >  | -  | -  | -  | -  | -  |
[DEP_MATRIX_END]

## Purpose
This tracker monitors code dependencies between modules in the source code. It helps identify which modules will be affected when changes are made to a specific module.

## Module Descriptions

### Source Code Modules
- M1: Core system functionality and shared components
- M2: Utility functions used across the application
- M3: API endpoints and handlers
- M4: Database access layer and models
- M5: User interface components and controllers
- M6: Authentication and authorization system

### Test Modules
- M7: Core functionality test suite
- M8: API endpoints test suite

## Dependency Key
- > : Row depends on column (module in row imports/uses module in column)
- < : Column depends on row (module in column imports/uses module in row)
- x : Mutual dependency (both modules depend on each other)
- - : No dependency (used on diagonal or when truly independent)
- d : Documentation reference only

## Module Structure
Each module represents a top-level directory in the source code. Files within these directories inherit the dependencies of their parent module.

## Update Procedure
When modifying a module, check its column to identify which other modules might be affected by the change.