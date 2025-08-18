# Overview

- How to conserve tokens?
    + Recursive context
- https://www.reddit.com/r/ChatGPTCoding/comments/1inyt2s/my_experience_with_cursor_vs_cline_after_3_months/
- https://github.com/eyaltoledano/claude-task-master
- https://github.com/RPG-fan/Cline-Recursive-Chain-of-Thought-System-CRCT-
- Comparison of AI coding tools
    + https://www.shakudo.io/blog/best-ai-coding-assistants

# Getting Started

- Cline is AI-powered coding companion.

## Task Management

- Task history
    + Quickly search by content using fuzzy search
    + Task actions: open, favorite, delete, export (to markdown)
- Task favorites
    + Protected from individual and bulk deletion operations.
- Best practices
    + Favorite important tasks
    + Regular cleanup: remove old and unused tasks to improve
      performance
    + Export valuable tasks: export important tasks to markdown for
      external reference

## Context Management

- Quick reference
    + Context = the information Cline knows about your project
    + Context window = how much information Cline can hold at once
        * Claude 3.5 Sonnet: 200,000 tokens (1 token ~ 3/4 of an English
          word)
    + Use context files to maintain project knowledge
    + Reset when the context window gets full
- How Context is built?
    + Automatic context gathering
    + User-guided context
    + https://cline.bot/blog/understanding-the-new-context-window-progress-bar-in-cline
- Context files help maintain understanding across sessions.
- Approaches to context files
    + Evergreen project context (i.e. memory bank)
        * living documentation that evolves with your project
        * updated as architecture and patterns emerge
        * example: the memory bank pattern maintains files like:
          `techContext.md` and `systemPatterns.md`
        * useful for long-running projects and teams
    + Task-specific context (i.e. structured approach)
        * Created for specific implementation tasks
        * Document requirements, constraints, and decisions
        * example:

    ```
    # auth-system-implementation.md

    ## Requirements

    -   OAuth2 implementation
    -   Support for Google and GitHub
    -   Rate limiting on auth endpoints

    ## Technical Decisions

    -   Using Passport.js for provider integration
    -   JWT for session management
    -   Redis for rate limiting
    ```

    + Knowledge Transfer docs
        * Switch to plan mode and ask Cline to document everything
          you've accomplished so far, along with the remaining steps,
          in a markdown file
        * copy the contents of the markdown file
        * start a new task using that content as context
- Best Practices
    + Consider starting a fresh session when usage reaches 70-80% of the
      context window size for that model to maintain optimal performance.

# Prompting Skills

## Prompt Engineering Guide

- https://docs.cline.bot/prompting/prompt-engineering-guide
    + Read this and practice to build habit!
- How to write effective prompts and custom instructions?
- Add `clineignore` file to tells Cline which files and directories to
  ignore when analyzing your codebase.

# Cline Rules (.clinerules)

- https://docs.cline.bot/features/cline-rules

# Cline Memory Bank

- https://docs.cline.bot/prompting/cline-memory-bank
- Create a `.clinerules` file to add rules for a workspace.
    + Create a global rule for all workspaces to use the same memory
      bank structure.
- We can use folder system `.clinerules/`
    + With numeric prefixes for markdown files: `01-coding.md`,
      `02-documentation.md`, etc. Or non-numeric: `client-a.md`,
      `react.md`, `api-service.md`

## Rule Bank: For projects with multiple contexts or teams

- We can have inactive rule bank: `clinerules-bank/`
    + Sub-folders: `clients/`, `frameworks/`, `project-types/`, etc.
    + These rules can be copied to the `.clinerules/` folder to be
      active.

```
# Switch to Client B project
rm .clinerules/client-a.md
cp clinerules-bank/clients/client-b.md .clinerules/

# Frontend React project
cp clinerules-bank/frameworks/react.md .clinerules/
```

### Implementation Tip

Keep individual rule files focused on specific concerns
Use descriptive filenames that clearly indicate the rule’s purpose
Consider git-ignoring the active .clinerules/ folder while tracking the clinerules-bank/
Create team scripts to quickly activate common rule combinations
