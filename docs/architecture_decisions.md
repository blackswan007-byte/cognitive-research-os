\# Architecture Design Decisions (ADR)

\*\*Project:\*\* Cognitive Research OS (CROS)  
\*\*Methodology Reference:\*\* Gulli, A. (2024). \*Agentic Design Patterns: A Hands-On Guide to Building Intelligent Systems\*. O'Reilly Media.

\---

\#\# 1\. Overview  
This document outlines the architectural choices made during the development of CROS. The primary goal was to move away from standard "Zero-Shot" prompting (asking an LLM to do everything in one go) towards a modular \*\*Multi-Agent System\*\* that mimics the specialized cognitive functions of a human research team.

\#\# 2\. Implemented Design Patterns

\#\#\# 2.1. The Reflection Pattern (Chapter 4\)  
\* \*\*Problem:\*\* Large Language Models (LLMs) are prone to hallucination when asked to generate complex analyses in a single pass. They tend to commit to their first token generation, leading to "snowballing" errors.  
\* \*\*Solution:\*\* Implementation of a dedicated \*\*Analytical Engine (Agent 02)\*\*.  
\* \*\*Mechanism:\*\* Instead of generating the final report immediately, this agent is instructed to perform an internal monologue. It explicitly critiques the raw data provided by Agent 01 using a "Dual Reality Protocol" (Digital vs. Physical validation).  
\* \*\*Benefit:\*\* Increases the reliability of deductions by forcing a "pause and think" step before synthesis.

\#\#\# 2.2. Tool Use Pattern (Chapter 5\)  
\* \*\*Problem:\*\* LLMs are text prediction engines, not calculators. They struggle with arithmetic consistency and statistical anomaly detection (e.g., Benford's Law).  
\* \*\*Solution:\*\* The \*\*Data Inquisitor\*\* agent.  
\* \*\*Mechanism:\*\* This agent is strictly bound to a \`Tool Definitions\` constraint. It is forbidden from performing visual analysis and must generate Python code (Pandas/Scipy) to execute statistical tests.  
\* \*\*Benefit:\*\* Moves the system from "stochastic guessing" to "deterministic execution" for data auditing.

\#\#\# 2.3. Prompt Chaining & Routing (Chapter 1 & 2\)  
\* \*\*Problem:\*\* Context windows can get cluttered, and a single persona cannot hold conflicting perspectives (e.g., being a Creative Innovator AND a Forensic Auditor simultaneously).  
\* \*\*Solution:\*\* Decomposition of the workflow into distinct files (\`src/core-research/\`).  
\* \*\*Mechanism:\*\*  
    1\.  \*\*Context Architect:\*\* Divergent thinking (Expands noise/data).  
    2\.  \*\*Analytical Engine:\*\* Convergent thinking (Filters logic).  
    3\.  \*\*Narrative Curator:\*\* Stylistic formatting (Polishes output).  
\* \*\*Benefit:\*\* Each agent maintains a high-fidelity persona without "leaking" instructions from the other phases.

\---

\#\# 3\. System Prompt Engineering Standards  
Based on Gulli's framework (p. 482), all agents in this repository strictly adhere to the following component structure:

1\.  \*\*Role and Goal:\*\* Clearly defined identity (e.g., "You are a Ghostwriter").  
2\.  \*\*Constraints and Rules:\*\* Negative constraints (e.g., "NO Listicles", "Trust No Row").  
3\.  \*\*Process Instructions:\*\* Step-by-step cognitive protocols (e.g., "Phase 1: Gut Check").  
4\.  \*\*Output Format:\*\* Strict structural requirements to ensure compatibility between agents.

\---

\#\# 4\. Future Roadmap  
\* \*\*Memory Management (Chapter 8):\*\* Implementing a long-term memory vector database to allow agents to recall previous case studies.  
\* \*\*Planning (Chapter 6):\*\* Allowing the system to dynamically generate its own research plan rather than following a fixed linear chain.  
