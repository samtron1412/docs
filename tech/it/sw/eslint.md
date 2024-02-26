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

# Configure Rules

## Disabling Rules

- https://eslint.org/docs/latest/use/configure/rules#disabling-rules

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

# Troubleshooting

## Symlinks issue: Parsing error: "parserOptions.project" has been set for @typescript-eslint/parser

- https://github.com/typescript-eslint/typescript-eslint/issues/2987
- Need to open the project without the symlinks.

## SyntaxError: Unexpected token

- This is because of incorrect NodeJS version (old version).
- Make sure the NodeJS version in your build system (IntelliJ, etc.) is
  set correctly to the latest version.
