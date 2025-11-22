# Overview

# Troubleshooting

## Context window always full and compaction keeps triggering

- Remove unused MCP servers.
- Reduce `CLAUDE.md` files' size.

## API Error (429 Too many tokens, please wait before trying again.)

- The limit for number of tokens for your model is too low, request
  increase or using another model with higher token limit.

## API Error (503 Model is getting throttled. Try your request again.)

- The current model has a low TPS, so we need to wait or use another
  model.

# Installation

- https://w.amazon.com/bin/view/Cyxie/ClaudeCodeBestPractices
+ Install claude code:
    * Install NodeJS 18+
    * `npm install -g @anthropic-ai/claude-code`
    * Disable Harmony if necessary
        - `harmony npm --disable`

# Configure

- https://docs.anthropic.com/en/docs/claude-code/settings
- Bedrock claude models
    + 3.7 Sonnet: `us.anthropic.claude-3-7-sonnet-20250219-v1:0`
    + Sonnet 4: `us.anthropic.claude-sonnet-4-20250514-v1:0`
    + Opus 4: `us.anthropic.claude-opus-4-20250514-v1:0`

```
{
  "env": {
    "CLAUDE_CODE_USE_BEDROCK": "1",
    "AWS_PROFILE": "ClineBedrockAccess",
    "CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC": "1",
    "DISABLE_PROMPT_CACHING": "1",
    "ANTHROPIC_MODEL": "us.anthropic.claude-opus-4-20250514-v1:0",
    "ANTHROPIC_SMALL_FAST_MODEL": "us.anthropic.claude-sonnet-4-20250514-v1:0"
  },
  "includeCoAuthoredBy": false,
}
```

- Notifications
    + https://docs.anthropic.com/en/docs/claude-code/settings#global-configuration
    + `claude config set --global preferredNotifChannel iterm2_with_bell`

# Use Claude

## Common Use Cases

- `explain to me this project structure`
- `<describe what we want claude to do in details>. Think harder`
- `write a test for the change we just made to make sure the logic is
  correct and indeed <describe the expected behavior here>`
- `now let's build the app to make sure everything works`
- `commit the changes with clear description`

## Advanced Use Cases and Power User

- Compare with Q CLI
    + https://taskei.amazon.dev/tasks/7e58ba39-b19c-4ebc-922c-1457c841303e?activeTab=comments#4fe0f75e-af1b-462c-9d13-31b3d57eb435

## Prompt Engineering

- https://docs.claude.com/en/docs/build-with-claude/prompt-engineering/overview

## Context Engineering

- https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents

# Best Practices

- https://www.anthropic.com/engineering/claude-code-best-practices

## Customize your setup

### Use CLAUDE.md

- `CLAUDE.md` files are automatically pulled into context
    + Common bash commands
    + Core files and utility functions
    + Code style guidelines
    + Testing instructions
    + Repository etiquette (e.g., branch naming, merge vs. rebase, etc.)
    + Developer environment setup (eg., pyenv use, which compilers work)
    + Any unexpected behaviors or warning particular to the project
    + Other information that you want Claude to remember
- Locations
    + `~/.claude/CLAUDE.md`: all claude sessions
    + Any directory: workspace or repository
        * commit to version control to share with team
- Tuning the content occasionally
    + Using `IMPORTANT` or `YOU MUST` emphasis to improve adherence.
- In claude sessions, can use `#` to add content to relevant `CLAUDE.md`
  file.

```
# Bash commands
- npm run build: Build the project
- npm run typecheck: Run the typechecker

# Code style
- Use ES modules (import/export) syntax, not CommonJS (require)
- Destructure imports when possible (eg. import { foo } from 'bar')

# Workflow
- Be sure to typecheck when you’re done making a series of code changes
- Prefer running single tests, and not the whole test suite, for performance
```

### Curate Claude's list of allowed tools

- `/permissions` command in session
- manually edit: `~/.claude/settings.json` or `~/.claude.json`

## Add documents or directories to context

- Add docs:
    + `Add @<doc> to your context`
- Add dirs:
    + `/add-dir`
- `/context` to monitor and manage the context size

## Give Claude more tools

- Add your shell tools to `CLAUDE.md`
    + Tool name and usage examples.
    + Tell claude to run `--help` to see tool documentation.
- MCP
    + `claude --mcp-debug` to help identify configuration issues
    + Only include necessary tools to reduce context size
        * Using include or allow list tools to do this

### Use custom slash commands
    + For repeated workflows—debugging loops, log analysis, etc.—store
      prompt templates in Markdown files within the `.claude/commands`
      folder
    + Custom slash commands can include the special keyword $ARGUMENTS
      to pass parameters from command invocation.

```
Please analyze and fix the GitHub issue: $ARGUMENTS.

Follow these steps:

1. Use `gh issue view` to get the issue details
2. Understand the problem described in the issue
3. Search the codebase for relevant files
4. Implement the necessary changes to fix the issue
5. Write and run tests to verify the fix
6. Ensure code passes linting and type checking
7. Create a descriptive commit message
8. Push and create a PR

Remember to use the GitHub CLI (`gh`) for all GitHub-related tasks.
```

- Putting the above content into .claude/commands/fix-github-issue.md
  makes it available as the /project:fix-github-issue command in Claude
  Code. You could then for example use /project:fix-github-issue 1234 to
  have Claude fix issue #1234. Similarly, you can add your own personal
  commands to the ~/.claude/commands folder for commands you want
  available in all of your sessions.

## Try common workflows

- https://docs.anthropic.com/en/docs/claude-code/common-workflows

### Codebase Q&A

- How does logging work?
- How do I make a new API endpoint?

### Explore, plan, code, commit

- https://www.reddit.com/r/ClaudeAI/comments/1lw5oie/how_phasebased_development_made_claude_code_10x/
- Explore
    + Ask Claude to read relevant files, images, or URLs
- Plan
    + Ask Claude to think with keywords:
    + These specific phrases are mapped directly to increasing levels of thinking budget in the system:
        * "think" -> "think hard" -> "think harder" -> "ultrathink."
- Code: Ask Claude to implement the solution in code
- Commit

### Write tests, commit; code, iterate, commit

- Ask Claude to write tests based on expected input/output pairs. Be explicit about the fact that you’re doing test-driven development so that it avoids creating mock implementations, even for functionality that doesn’t exist yet in the codebase.
- Tell Claude to run the tests and confirm they fail. Explicitly telling it not to write any implementation code at this stage is often helpful.
- Ask Claude to commit the tests when you’re satisfied with them.
- Ask Claude to write code that passes the tests, instructing it not to modify the tests. Tell Claude to keep going until all tests pass. It will usually take a few iterations for Claude to write code, run the tests, adjust the code, and run the tests again.
- At this stage, it can help to ask it to verify with independent subagents that the implementation isn’t overfitting to the tests
- Ask Claude to commit the code once you’re satisfied with the changes.

### Write code, screenshot result, iterate

- Give Claude a way to take browser screenshots (e.g., with the Puppeteer MCP server, an iOS simulator MCP server, or manually copy / paste screenshots into Claude).
- Give Claude a visual mock by copying / pasting or drag-dropping an image, or giving Claude the image file path.
- Ask Claude to implement the design in code, take screenshots of the result, and iterate until its result matches the mock.
- Ask Claude to commit when you're satisfied.

### Safe YOLO mode

Instead of supervising Claude, you can use claude
--dangerously-skip-permissions to bypass all permission checks and let
Claude work uninterrupted until completion. This works well for
workflows like fixing lint errors or generating boilerplate code.

### Git interaction

- Searching git history to answer questions like "What changes made it
  into v1.2.3?", "Who owns this particular feature?", or "Why was this
  API designed this way?" It helps to explicitly prompt Claude to look
  through git history to answer queries like these.
- Writing commit messages. Claude will look at your changes and recent
  history automatically to compose a message taking all the relevant
  context into account
- Handling complex git operations like reverting files, resolving rebase
  conflicts, and comparing and grafting patches

## Optimize your workflow

### Be specific in your instructions

Poor	Good
add tests for foo.py	write a new test case for foo.py, covering the edge case where the user is logged out. avoid mocks
why does ExecutionFactory have such a weird api?	look through ExecutionFactory's git history and summarize how its api came to be
add a calendar widget	look at how existing widgets are implemented on the home page to understand the patterns and specifically how code and interfaces are separated out. HotDogWidget.php is a good example to start with. then, follow the pattern to implement a new calendar widget that lets the user select a month and paginate forwards/backwards to pick a year. Build from scratch without libraries other than the ones already used in the rest of the codebase.

### Give Claude images

Claude excels with images and diagrams through several methods:
- Paste screenshots (pro tip: hit cmd+ctrl+shift+4 in macOS to screenshot to clipboard and ctrl+v to paste. Note that this is not cmd+v like you would usually use to paste on mac and does not work remotely.)
- Drag and drop images directly into the prompt input
- Provide file paths for images

This is particularly useful when working with design mocks as reference
points for UI development, and visual charts for analysis and
debugging. If you are not adding visuals to context, it can still be
helpful to be clear with Claude about how important it is for the result
to be visually appealing.

### Mention files you want Claude to look at or work on

### Give Claude URLs

### Course correct early and often

While auto-accept mode (shift+tab to toggle) lets Claude work
autonomously, you'll typically get better results by being an active
collaborator and guiding Claude's approach.

These four tools help with course correction:

- Ask Claude to make a plan before coding. Explicitly tell it not to code until you’ve confirmed its plan looks good.
- Press Escape to interrupt Claude during any phase (thinking, tool calls, file edits), preserving context so you can redirect or expand instructions.
- Double-tap Escape to jump back in history, edit a previous prompt, and explore a different direction. You can edit the prompt and repeat until you get the result you're looking for.
- Ask Claude to undo changes, often in conjunction with option #2 to take a different approach.

### Use `/clear` to clear context between tasks

### Use checklists and scratchpads for complex workflows

For large tasks with multiple steps or requiring exhaustive
solutions—like code migrations, fixing numerous lint errors, or running
complex build scripts—improve performance by having Claude use a
Markdown file (or even a GitHub issue!) as a checklist and working
scratchpad:

For example, to fix a large number of lint issues, you can do the following:
- Tell Claude to run the lint command and write all resulting errors (with filenames and line numbers) to a Markdown checklist
- Instruct Claude to address each issue one by one, fixing and verifying before checking it off and moving to the next


### Ignore build output to reduce context size

- Can use sub-agent to handle build process to keep the main context
  clean, focus and small.

## Use headless mode to automate your infra

Claude Code includes headless mode for non-interactive contexts like CI,
pre-commit hooks, build scripts, and automation. Use the -p flag with a
prompt to enable headless mode, and --output-format stream-json for
streaming JSON output.

## Multi Claude

### Open other claude sessions in the same folder to check the work of each other

- Use Claude to write code
- Run /clear or start a second Claude in another terminal
- Have the second Claude review the first Claude's work
- Start another Claude (or /clear again) to read both the code and review feedback
- Have this Claude edit the code based on the feedback

You can do something similar with tests: have one Claude write tests,
then have another Claude write code to make the tests pass. You can even
have your Claude instances communicate with each other by giving them
separate working scratchpads and telling them which one to write to and
which one to read from.

### Check out code into multiple folders or git subtrees to work on different tasks.

Rather than waiting for Claude to complete each step, something many engineers at Anthropic do is:

- Create 3-4 git checkouts in separate folders
- Open each folder in separate terminal tabs
- Start Claude in each folder with different tasks
- Cycle through to check progress and approve/deny permission requests

### Use headless mode with a custom harness

1. Fanning out handles large migrations or analyses (e.g., analyzing
  sentiment in hundreds of logs or analyzing thousands of CSVs):

- Have Claude write a script to generate a task list. For example, generate a list of 2k files that need to be migrated from framework A to framework B.
- Loop through tasks, calling Claude programmatically for each and giving it a task and a set of tools it can use. For example: claude -p “migrate foo.py from React to Vue. When you are done, you MUST return the string OK if you succeeded, or FAIL if the task failed.” --allowedTools Edit Bash(git commit:*)
- Run the script several times and refine your prompt to get the desired outcome.

2. Pipelining integrates Claude into existing data/processing pipelines:

- Call `claude -p <your prompt> --json | your_command`, where your_command is the next step of your processing pipeline



# AI Orchestration Platform for Claude Code

- https://github.com/ruvnet/claude-flow

# Tips and Tricks

## Resume or Continue Previous Sessions

- Continue the most recent session: `claude -c`
- Resuming a specific session: `claude --resume`
    + `claude --resume <id>`
- Starting with a specific session ID (named session)
    + `claude --session-id <id>`

## MCP Server

- https://code.claude.com/docs/en/mcp
- https://www.anthropic.com/engineering/writing-tools-for-agents

## Agent Skills

- https://code.claude.com/docs/en/skills
    + Examples: https://github.com/anthropics/skills
- https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills
- Skills are folders that include instructions, scripts, and resources
  that Claude can load when needed.
- Claude can use Skills to improve how it performs specific tasks.
- Claude will only access a skill when it's relevant to the task at
  hand. When used, skills make Claude better at specialized tasks like
  working with Excel or following your organization's brand guidelines.

## Sub-agents

- https://code.claude.com/docs/en/sub-agents
- They're great tools for keeping sub-contexts focused.
- Subagents help to get the lengthy context about how to use brazil out
  of the main chat (which keeps it smaller and increases adherence to
  the instructions when the subagent does run a build), and lets the
  subagent totally contain the lengthy output of a build, distill it
  down to a main takeaway, and forward only that back to the main chat.
- Another good example could be a linter subagent that does lint checks,
  modifies files, does the lint checks again, etc. - a very iterative
  process that by default can really bloat a conversation with
  intermediate actions and attempts that are not useful to retain after
  they are complete.

## Hooks

- https://code.claude.com/docs/en/hooks-guide
