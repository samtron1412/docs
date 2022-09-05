# Overview

- Specifying globals
    + https://eslint.org/docs/user-guide/configuring/language-options#specifying-globals
    + Tell the linter that the global variables are defined in a
      different location.
    + Using configuration comments:
        * `/* global var1, var2 */`
        * `/* globals var1, var2 */`
- Two categories of rules
    + Formatting rules: we can use Prettier to replace these rules
    + Code quality rules: we still need linter to take care of these
      rules.

# plugin:import/recommended

- List of recommended rules for plugin import
    + https://github.com/import-js/eslint-plugin-import/blob/main/config/recommended.js

# plugin:@typescript-eslint/recommended

- List of recommended rules and compatibility rules
    + https://github.com/typescript-eslint/typescript-eslint/blob/main/packages/eslint-plugin/src/configs/eslint-recommended.ts
- Type checking
    + https://github.com/typescript-eslint/typescript-eslint/blob/main/packages/eslint-plugin/src/configs/recommended-requiring-type-checking.ts

# plugin:react/recommended

- https://github.com/jsx-eslint/eslint-plugin-react

