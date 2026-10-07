# AgenticAI
MAI - Week 1
18 sources
·
May 28, 2026
The provided sources explore the mechanics and optimization of large language models, covering architectural designs like attention variants and hybrid attention stacks, alongside practical API integrations for audio modalities and prompt engineering development strategies. They also examine the foundational processes of model pre-training, including internet data curation, web filtering, and tokenization. Furthermore, the material highlights the balance between inference efficiency and memory reduction through techniques such as Grouped-Query Attention and Multi-head Latent Attention. Finally, the documentation and tutorials provide comprehensive guidance on deploying multimodal capabilities, structuring speech tasks, and building effective AI applications.

Today • 10:28 AM
create a summary of session 2 , including flash cards and interview questions


Thoughts
Note on Read-Only Mode: This notebook is currently set to read-only mode, which means persistent artifacts (such as interactive Flashcard apps or saved notes in the Studio panel) cannot be created or modified here. If you would like to generate persistent artifacts or save new materials, please create a personal copy of this notebook.
However, I have provided the complete summary, flashcards, and interview questions directly here in our chat!
📚 Week 1 — Session 2: Summary, Flashcards & Interview Questions
1. Executive Summary of Session 2
Session 2 of the Agentic AI Bootcamp focuses on moving from standard generative text completion to autonomous, goal-driven agentic systems and structured application architectures
.

Key Pillars Covered:
Automation in the Agentic Era
Traditional Automation: Relies on rigid, deterministic, rule-based logic and fixed if/else workflows
. It breaks when encountering edge cases or ambiguous inputs, requiring manual human exception handling
.

Agentic Automation: Driven by goals rather than fixed rules
. An LLM-powered agent operates in an iterative loop (Goal → Planning → Memory/Context Retrieval → Tool Execution → Reflection/Retry → Output) to handle edge cases and adaptively solve complex workflows
.

Levels of Agent Autonomy (Level 0 to Level 5)
Level 0 (Human Does Everything): AI acts as a basic query or drafting tool (e.g., ChatGPT Q&A, spellcheck)
.

Level 1 (Human-in-the-Loop / HITL): AI recommends actions, but nothing executes without explicit human approval (e.g., drafting an email or underwriting approval)
.

Level 2 (Human-on-the-Loop / HOTL): AI acts autonomously within set boundaries, while humans monitor and intervene only when necessary (e.g., customer support resolution, auto-scaling)
.

Level 3 (Human-over-the-Loop): AI manages workflows and decision-making end-to-end; humans set high-level goals and review outcomes
.

Level 4 (High Autonomy): AI independently decomposes complex goals, uses tools, and recovers from errors with minimal intervention (e.g., autonomous coding agents)
.

Level 5 (Fully Autonomous Systems): AI operates completely independently across complex long-horizon tasks
.

The 6-Step Agentic Application Framework Building robust agentic software follows a modular 6-layer architecture
:

Domain Knowledge: Internal documents, FAQs, databases, and business rules
.

Goals & Inputs: The specific objective or user trigger (e.g., resolving a support ticket)
.

Workflow / Process: Logic steps for retrieval, analysis, validation, and step planning
.

Decisions: Rule and context-based evaluations (e.g., determining refund eligibility or risk classification)
.

Actions: Real-world execution via external APIs, databases, or communication channels
.

Autonomy & Governance: HITL/HOTL oversight, safety guardrails, monitoring, and approval rules
.

Agentic Frameworks: n8n vs. LangChain vs. Raw SDK

Without Frameworks: Code quickly turns into an unmaintainable "spaghetti mess" of fragile prompt wrappers and manual error-handling loops
.

n8n (Low-Code): Drag-and-drop visual workflow builder utilizing nodes (Trigger, Data/Set, AI/LLM, Logic/IF, Action/App, Code) to connect SaaS apps in hours without complex code
.

LangChain & LangGraph (Code-Based Orchestration): Open-source developer frameworks offering modular primitives (Models, Prompts, Chains, Memory, Retrievers, Vector Stores, Tools, Agents, Output Parsers) to construct custom stateful agents and RAG pipelines
.

Raw SDK: Direct API integration with no abstraction layers; ideal when latency is critical, debugging needs to be exact, or simple single-call workflows are sufficient
.

Two Foundational Concepts: Structured Output & Function Calling
Structured Output: Constrains model generation to conform strictly to a predefined schema (such as JSON Schema or Pydantic)
. This converts messy natural language into type-safe data that software systems can safely ingest without regex or retry hacks
.

Function Calling: The mechanism by which LLMs interface with external tools

. The model does not execute code itself; instead, it outputs a structured JSON payload requesting a specific function and specifying its parameters
. The host program executes the code and returns the output to the LLM to complete the response loop
.

🎴 Flashcards for Study & Revision

Card 1
Front: What is the core difference between Traditional Automation and Agentic Automation?
Back: Traditional Automation follows fixed, deterministic if/else rules and breaks on unexpected edge cases
. Agentic Automation is goal-driven; it uses an LLM in a loop with tools and memory to adaptively reason, handle ambiguity, and recover from errors
.

Card 2
Front: What distinguishes Level 1 (HITL) autonomy from Level 2 (HOTL) autonomy in AI agents?
Back: In Level 1 (Human-in-the-Loop), the AI only recommends actions and requires explicit human approval before any action takes place
. In Level 2 (Human-on-the-Loop), the AI acts autonomously within pre-defined boundaries, while humans monitor execution and step in only on exceptions
.


Card 3
Front: What are the 6 layers of the Agentic AI Application Framework?
Back:
Domain Knowledge (Context & Data)
Goals & Inputs (Triggers & Objectives)
Workflow / Process (Logic & Step planning)
Decisions (Judgments & Evaluations)
Actions (API calls & System execution)
Autonomy & Governance (Guardrails & Human oversight)

Card 4
Front: When should you build an agent using n8n versus LangChain / LangGraph?
Back: Use n8n when you need speed, simple SaaS integrations (e.g., Slack, Gmail, Google Sheets), and visual workflow editing for non-engineers
. Use LangChain / LangGraph when you need deep programmatic control, custom Python tools, complex RAG state management, and multi-step branching logic
.

Card 5
Front: What is Structured Output and why is it crucial for AI applications?
Back: Structured Output forces an LLM to generate responses that strictly adhere to a predefined JSON schema
. It eliminates formatting hallucinations, missing keys, and invalid values, enabling downstream application software to process output with type safety
.

Card 6
Front: Does an LLM execute the function code when performing Function Calling?
Back: No. The LLM only generates a structured tool-call request containing the function name and its extracted JSON arguments
. The developer's application code executes the function in its own runtime environment and sends the result back to the model
.

🎯 Technical Interview Questions & Answers

Q1: Compare deterministic workflow automation with agentic AI workflows. When should an engineering team stick to traditional scripts instead of an AI agent?
Model Answer: Traditional automation relies on static, rule-based execution paths (e.g., cron jobs, Zapier webhooks, IF/ELSE logic)
. It is fast, cheap, completely predictable, and optimal for structured, repetitive tasks with zero ambiguity
. Agentic automation introduces an LLM reasoning engine into a dynamic loop that can interpret unstructured inputs, choose tools dynamically, and handle unexpected edge cases
.

An engineering team should stick to traditional scripts when the inputs are fully structured (e.g., parsing a standardized CSV), the business rules are non-negotiable and strictly deterministic, or latency/cost constraints render LLM invocation impractical
.

Q2: Walk through the 5-step tool calling loop in OpenAI or LangChain. How does context pass between the user, application, and model?
Model Answer:
Tool Definition & Request: The application sends a user prompt along with JSON schemas defining available functions to the model
.

Tool Call Response: The model determines a function call is needed and returns a tool_calls payload containing a unique call_id, function name, and JSON arguments
.

Local Execution: The application parses the tool call, executes the requested function locally (e.g., fetching a database or calling a weather API), and captures the output
.

Submitting Tool Output: The application appends a new message with role tool (including the call_id and raw result) to the conversation history and resubmits it to the model
.

Final Response Generation: The model ingests the tool output and synthesizes a natural language answer or executes further tool calls if needed
.

Q3: What are the core architectural tradeoffs between building an agent using an SDK directly versus using an orchestration framework like LangChain or LangGraph?
Model Answer:
Raw SDK: Offers complete zero-abstraction control over every token sent and received, minimal dependency overhead, straightforward step-by-step debugging, and optimal latency performance
. However, you must manually write state management, retry logic, memory handling, and tool dispatching
.

Orchestration Frameworks (LangChain / LangGraph): Provide pre-built primitives for vector stores, memory buffers, message parsers, and state-graph loops
. This enables rapid prototyping and standardizes complex multi-agent workflows, but introduces abstraction overhead, higher library complexity, and potential debugging friction when tracing hidden internal prompts
.

Q4: Explain how Structured Output differs from standard JSON mode in model APIs, and how it works under the hood.
Model Answer: Standard JSON mode guarantees that the model outputs syntactically valid JSON, but it does not guarantee that the JSON conforms to a specific schema—keys can still be omitted or hallucinated
. Structured Output guarantees strict adherence to a provided JSON schema
. Under the hood, modern model providers enforce this at the decoding level using constrained context-free grammars (CFGs) or logit bias masking during token sampling, ensuring invalid tokens that violate the target schema cannot be selected
.

Q5: In designing an enterprise customer support agent, how do you map human governance (HITL / HOTL) onto high-risk vs. low-risk operational steps?
Model Answer: Based on the Agentic AI Application Framework, governance is applied at the Actions and Autonomy layers
:

Low-Risk Actions (e.g., querying order status, providing FAQ answers, re-sending receipts): Deployed under Level 2 (Human-on-the-Loop) autonomy, where the agent executes actions independently while logging output for audit teams
.

High-Risk Actions (e.g., processing refunds over $100, cancelling subscriptions, or modifying account security): Deployed under Level 1 (Human-in-the-Loop) autonomy
. The agent extracts context, formulates the proposed decision, and generates a structured approval request for a human agent to review and confirm before system execution
.
