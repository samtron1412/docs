# Overview

Agentic AI

# Agents

- Agent Introduction and how to use them effectively
    + https://atoz.amazon.work/feed/content/1bdf30d0-0a1d-486f-a089-6e9e2834af84
- Agent anatomy
    + https://www.mihaileric.com/The-Emperor-Has-No-Clothes/

```
Agent components, revisited

Before we get into how to use agents, it helps to have a clear understanding of what agents are. Unsurprisingly, there's a bit of variety in how agents are defined. For the purposes of this article, we'll use the following definition:



An agent is a combination of a large language model, tools, prompts, context, and a reasoning loop, working together to handle complex tasks.



Four of these components might already be familiar to you:



Large Language Model (LLM): An LLM is a stateless, nondeterministic predictive algorithm that serves as the foundation of agentic systems. It's stateless because it doesn't store computation beyond training weights, starting fresh with each interaction unless history is explicitly provided. It's nondeterministic because identical inputs can produce different outputs based on probability distributions, and it's predictive because it examines text patterns to predict what should come next based on its training data.
Tools: Tools are functions the LLM can invoke during its agentic loop to extend its capabilities beyond text generation. They include read-only tools that retrieve information without changing anything, and write tools that create side effects by modifying state. One common way to connect an LLM to these tools is through the Model Context Protocol (MCP), a standardized protocol that enables systems to connect with external tools and extend the agentic system's access to documentation, databases, and domain-specific operations.
Prompts: Prompts are instructions provided to a generative AI model to guide it in producing a specific response. Well-written prompts establish clear expectations about agent behavior, error handling, and interaction patterns. They also make AI agents easier to debug. When prompts are step-by-step in structure, you can more easily identify what happened when an agent goes off-track. Again, a common challenge when working with AI is its non-determinism. Structured prompts don’t eliminate this issue entirely, but they do make troubleshooting a whole lot easier. (We cover one way to create effective prompts later in this article.)
Context: Context is all the input that the agentic system feeds to the LLM, combining direct input with additional information that shapes how the LLM interprets and responds to requests. It comes from multiple sources including explicit files and attachments, conversation history, prompts, and tools. Context is measured in tokens and limited by the context window—the amount of text a model can view at once. The document categorizes context into four types: rules (boundaries and constraints), knowledge (domain-specific facts), workflows (processes and methodologies), and tools (extensions of capabilities).


The Reasoning Loop

Now, let’s examine what makes these four components—the LLM, tools, prompts, and context—work together as an agent rather than just a collection of parts. The key difference lies in the reasoning loop—the iterative decision-making process that enables agents to autonomously complete complex tasks.



8l6QXtAAAABklEQVQDABL0Vi+5j+j9AAAAAElFTkSuQmCC



Unlike a simple LLM call that generates a single response and stops, an agent uses a reasoning loop that breaks down complex requests into steps, makes decisions about what information is needed, and iteratively works toward a solution. When you ask an agent to "optimize this Python script for performance," it doesn't just generate suggestions. Instead, it first reads the file to understand the implementation, then analyzes the code structure to identify expensive operations, and finally proposes specific changes with explanations—each step building on the previous one.



The loop operates through continuous assessment and adaptation, having the agent:



Examine your request
Determine what actions to take
Invoke tools to gather information or perform actions
Incorporate results into its reasoning

The agent continues this cycle until it determines it has enough information to provide a useful response. Just as a pit crew monitors telemetry and adjusts strategy based on what they learn, or a dispatch center reroutes buses based on traffic conditions, the reasoning loop adapts its approach based on intermediate results.



This iterative nature has an important consequence: Because the reasoning loop's decisions are dictated by the underlying LLM, the same request might follow slightly different paths on different runs. The agent might focus on memory optimization in one instance and computational efficiency in another, yet both approaches remain valid responses to the original query. While this tendency to produce non-deterministic results is technically a feature, the reality is that having different outputs can prove frustrating when consistency is important.



Effective agent inputs

Because agents are built on nondeterministic predictive algorithms, what you get out is dependent on what you put in. This input management is commonly referred to as context engineering. Understanding how to do context engineering well is critical to having agents produce useful and reliable results. One effective approach is to focus on four key properties that define what makes input effective when working with agents: accuracy, preciseness, cohesiveness, and conciseness.



Accuracy

Input accuracy refers to how true and factually correct the information you provide is. If you feed the agent incorrect premises or false information, it will build upon those flaws and produce unreliable outputs. Understanding this idea is important, because agents don’t fact-check your inputs—they trust them.



Giving an agent inaccurate or incomplete information can cause all sorts of challenges. For example, when you tell an agent "the configuration file is at /etc/app/config.yaml" but it's actually at /opt/app/config.yaml, the agent will attempt to read the wrong path, then navigate the directory structure trying to guess which file you meant. It might load an incorrect file if similarly named YAML files exist elsewhere in your system, wasting time and tokens while building its entire response on the wrong configuration data.



Inaccurate information cascades through the reasoning loop, leading to solutions that solve the wrong problem or make incorrect assumptions about your environment.



That’s why, before you engage an agent on complex tasks:



Verify that the information you're providing is current and correct
Double-check file paths, API endpoints, configuration values, and system states
Ensure that any documents or specifications are up to date


Preciseness

Input preciseness describes how well your input defines the expected outcome. Vague requests produce vague results, while the more precise your requests are, the more deterministic the output becomes.



For example, asking an agent to "make this code better" might yield superficial generic improvements like adding comments or renaming variables that may not address your actual needs. In contrast, "add input validation that checks for null values and raises ValueError with descriptive messages" is more likely to produce the changes you want.



Preciseness is important because the agent's reasoning loop operates on probability distributions. When your request is vague, the agent must guess which of many possible interpretations you intended. Precise specifications narrow the probability space, making it far more likely that the agent's output aligns with your actual needs.



To improve the preciseness of an agent’s outputs, define clear success criteria before making requests. Instead of "optimize this function," specify "reduce memory allocation in this function by reusing buffers instead of creating new ones." Instead of "write tests," specify "write pytest unit tests that cover edge cases for null inputs, empty lists, and boundary conditions."



Cohesiveness

Input cohesiveness measures how closely related the various elements of your input are to each other and to the task at hand. Scattered, tangential information dilutes the signal and reduces output quality, while tightly integrated inputs help the agent stay on task.



When asking an agent to refactor a specific function, pasting just that function produces focused results. Including unrelated functions from across your codebase introduces noise that causes the agent to suggest changes that optimize for the wrong context or miss the specific improvement opportunity you were targeting.



Agents aren't great at knowing what information is more important than another. That means that every piece of information in the context window competes for the agent's attention. Unrelated information doesn't just waste tokens—it actively degrades performance by introducing patterns and relationships that aren't relevant to your task, causing the agent to make connections that lead away from your goal.



As you work with agents, make sure to curate your context deliberately. Include only the files, documentation, and conversation history directly relevant to the current task. If you're debugging a specific error, provide the error message and the relevant code section, not your entire application log. If you're implementing a feature, include the specification and affected modules, not your entire codebase.



Conciseness

Input conciseness requires providing the right amount of information—not too little, which leaves the agent guessing, and not too much, which overwhelms it with noise and irrelevant details.



Prompting an agent to "debug this error" without showing the error message forces it to speculate about common issues rather than diagnosing your specific problem. Conversely, pasting your entire application log when only the stack trace matters buries the relevant information, leading the agent to focus on irrelevant warnings or info messages instead of the actual failure.



Just as with cohesiveness, conciseness matters because context windows are finite. When they become too full, the signal-to-noise ratio degrades, leading to hallucinations as the agent struggles to identify what information is most relevant. When they're too empty of relevant context, the agent relies too heavily on its training data, which may not align with your specific needs.



It’s up to you, as you work with agents, to find the balance between too little and too much. Provide enough context for the agent to understand the problem fully, but trim away anything that doesn't directly contribute to solving it. If you're working through a long troubleshooting session and notice the agent forgetting earlier context or contradicting itself, start a fresh conversation with a concise summary of what you've learned so far.



Agent strategies

Understanding input properties helps you work with agents effectively, but applying these concepts to real problems requires strategy. Over the past year, four strategies have emerged that address the most common challenge builders face: managing context effectively when agents handle complex, long-running tasks:



Divide and conquer: breaks complex problems into manageable pieces
Delegation: isolates context and applies specialization for each task
Progressive disclosure: makes information available as needed
Deterministic substitution: replaces probabilistic reasoning with factual computations


The specific implementation of these techniques varies across different agentic systems, but the underlying concepts remain constant regardless of the tools we use. Most real-world solutions implement these concepts either separately or in combination to address specific context management challenges.



Divide and Conquer

Divide and conquer tackles the problem of input conciseness and accuracy by splitting complex problems into several better-defined, smaller pieces. This strategy is the same as how you tackle any complex problem: by breaking the problem into smaller, more manageable chunks.



Using the divide and conquer strategy gives you the opportunity to separate thinking from doing. For example, when implementing a new API endpoint, planning first means defining the request/response schema, identifying error cases, and determining success criteria before writing code. This upfront work prevents discovering requirements mid-implementation when your context window is already full of partially completed code.



This plan/act pattern is why Kiro’s spec-driven development workflow is so powerful. It helps you separate the cognitive work of understanding what to accomplish from the tactical work of implementation. Along the way, you have greater control over the inputs you give Kiro, which helps make sure it creates the solution you’re looking for.



Delegation

Delegation builds on the divide and conquer strategy by taking each subtask assigning an independent agent to perform the work. Even though the divide and conquer strategy is useful, on its own it can still overwhelm a single agent’s context window if the problem is sufficiently complex. For example, if a single agent is asked to handle 10 subtasks, by the time it reaches the fifth one, the accumulated context might degrade performance, a trend that will continue until the agent has gone completely off the rails.



Delegation addresses this challenge by opening new context sessions per task and assigning an agent to each one to ensure they have the best chance of succeeding. Each delegated task operates in its own context boundary with only the information relevant to that specific task. This methodology helps prevent context pollution from unrelated work while enabling specialization that improves output quality.



One approach to delegation is to pair it with another common practice: creating specific agent specializations or personas. Specializations refers to creating focused agentic systems that bundle domain expertise, behavioral constraints, and tool permissions into a single configuration. Personas take this further by adopting professional identities like "Principal Engineer at Commerce Platform," embedding role-specific knowledge and decision-making patterns directly into agent behavior. Rather than relying on do-anything agents that struggle with context management, these patterns let you develop multiple specialists optimized for specific domains.



Progressive disclosure

Progressive disclosure (sometimes referred to as dynamic context loading) presents the agent with specific options and lets the agent decide what option to use and when. Rather than front-loading all potentially relevant context, this technique makes context available on demand.



This idea of progressive disclosure is what prompted the recent developments in agent skills and Kiro’s Powers. This strategy can help the agent detect when to delegate a given task to another agent, determine when to use a particular tool, or load specific context files containing knowledge, rules, or workflows as the need emerges during reasoning. The initial context window remains lean while also ensuring that any relevant information stays accessible when the reasoning process identifies gaps.



Deterministic Substitution

Determinist substitution refers to replacing inference-heavy steps with predictable operations.

Rather than asking the agent to infer patterns or analyze complex data directly, you can use tools to execute deterministic operations that provide factual summaries first.



For instance, consider a situation where you need to analyze several CSV files containing raw business data for KPI extraction and trend analysis. If you prompt the agent to read the entire dataset into context and infer patterns, you’ll likely encounter context window limits that produce inaccurate results. With deterministic substitution, you prompt the agent to generate a data processing script first, then run that script, and finally analyze the resulting summary.



This approach reduces the probability space the agent must navigate by providing concrete, processed facts rather than requiring inference from massive raw datasets. When you substitute deterministic operations for inferential reasoning, you’re constraining the agent's task to interpretation and recommendation rather than speculation, leading to more reliable outputs while consuming fewer tokens in the reasoning process.
```

# Protocols

- https://modelcontextprotocol.io
- https://a2a-protocol.org/latest/

# Frameworks to build Agents

- Amazon Strands Agent SDK
- OpenAPI
- LangChain
- LangGraph
- etc.
