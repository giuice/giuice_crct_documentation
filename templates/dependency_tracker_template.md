# Module Dependency Tracker

[DEP_MATRIX_START]
# KEY DEFINITIONS
M1: src/auth
M2: src/database
M3: src/utils

# MATRIX (Row depends on Column)
# Symbols: > (depends on), < (depended by), x (mutual), - (none), d (doc)
    | M1 | M2 | M3 |
M1  | -  | >  | >  |
M2  | -  | -  | >  |
M3  | -  | -  | -  |
[DEP_MATRIX_END]

## Purpose
This tracker monitors code dependencies between modules. When module M1 requires code from module M2, we mark it with ">" (depends on).

## Key
- > : Row depends on column (e.g., auth depends on database)
- < : Column depends on row (e.g., database is depended on by auth)
- x : Mutual dependency (both modules rely on each other)
- - : No dependency (used on diagonal)
- d : Documentation dependency (used mainly in doc_tracker)