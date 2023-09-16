[TOC]

# Overview

- YAML tutorials
    + https://www.w3schools.io/file/yaml-arrays/
- Cheat sheets
    + https://quickref.me/yaml
    + https://docs.ansible.com/ansible/latest/reference_appendices/YAMLSyntax.html
- Can use ` #` (space followed by the pound sign) to add inline comment.
- A colon followed by a space `: ` is an indicator for a mapping.
- Indicators for the start `---` and end `...` of a YAML document.
    + https://stackoverflow.com/q/50788277
- All members of a list are lines beginning at the same indentation
  level starting with a "- " (a dash and a space).
- A dictionary is represented in a simple key: value form (the colon
  must be followed by a space).

# Tips and Tricks

## Working with YAML

- Python
    + ruamel.yaml: keep most formatting as the original, but can't
      control spaces between brackets.
- CLI: `yq`
    + does not keep the original formatting.
- NOTE:
    + If you want to keep the original formatting, it's better to use
      replacement with regex in your editor or VIM macros + VIM search
      and replace with Regex (this is RECOMMENDED)

## Single vs Double Quotes

- Rules of thumb
    + https://stackoverflow.com/a/67536258/1683888
    + Single quotes work for all cases
    + You only need to handle the single quote itself as escape
      character in the single quotes approach.

