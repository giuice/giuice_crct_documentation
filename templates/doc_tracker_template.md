# Documentation Dependency Tracker

[DEP_MATRIX_START]
# KEY DEFINITIONS
D1: docs/overview.md
D2: docs/installation.md
D3: docs/api/auth.md

# MATRIX (Row depends on Column)
# Symbols: > (depends on), < (depended by), x (mutual), - (none), d (doc)
    | D1 | D2 | D3 |
D1  | -  | -  | -  |
D2  | <  | -  | -  |
D3  | <  | -  | -  |
[DEP_MATRIX_END]

## Purpose
This tracker monitors dependencies between documentation files. When one document references or requires another document, we track it here.

## Key
- > : Row references/requires column (e.g., api doc references installation doc)
- < : Column references/requires row (e.g., overview is referenced by installation)
- x : Cross-references (both documents reference each other)
- - : No dependency (used on diagonal)
- d : References code module (used when docs directly reference code)

## Additional Notes
- All files in docs/ directory should be included here
- Maintain this tracker to ensure documentation completeness