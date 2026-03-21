How I Built a Multi-Agent Development Pipeline That Works Like a Full Engineering Team
From natural language requirements to automated commits — with specialized agents, safety guardrails, and zero context switching.
By Lucas da Silva Santos — Full Stack Developer | Co-founder at Repetz
I've been building production systems for over four years.
A hospital performance platform with 10+ years in production, compliant with Brazilian federal healthcare regulatory standards, handling financial, clinical, and compliance data at scale.
I know what production pressure looks like. I know what it costs when something breaks. And I know how much cognitive load it takes to go from a client's words to a reliable, tested, committed implementation.
This year, I stopped managing that load manually.
Instead, I architected a team.
The Problem I Was Solving
The bottleneck in software development is rarely pure coding ability.
It's context switching.
Writing the technical spec. Implementing the backend. Building the frontend. Writing tests. Reviewing your own code. Committing safely.
Each of those is a different mental mode. Switching between them is expensive. And when you're working across complex production systems — legacy codebases, strict security requirements, integrations with external systems — the cost of a context switch isn't just lost time. It's risk.
I needed a way to stay at the architectural layer, where my judgment actually matters, and let the execution layer run without me managing every transition.
The Architecture: Specialization Over Generalization
Most developers use AI as a single assistant that does everything. I took a different approach: each agent has one job, one context, and one set of tools.
This mirrors how real engineering teams work. You wouldn't ask your backend engineer to write your Jira tickets and your test suite at the same time. The same principle applies here.
The pipeline has up to 5 active agents, depending on task complexity. Some run sequentially. Others run in parallel when the task allows it.

🗂️ Requirements Transcription Agent

The entry point. Takes the client's request in natural language and converts it into a structured technical card — formatted for Jira or Trello.
This is where "non-technical to technical" translation happens, before any code is written. No ambiguity. No lost context. No requirements that mean different things to different people.

🧠 Planning Agent (Orchestrator)

The most critical agent in the pipeline.
Its job: read the technical card, understand the full project context, and delegate tasks to the most appropriate specialist agent.
It knows the architecture. The stack. The legacy constraints. The business rules. The security requirements.
It decides: Does this go to the frontend agent? Backend? Both in parallel? Does it need a review loop?

🎨 Frontend Specialist Agent

Handles all UI and client-side implementation. Has deep context about the project's frontend stack, component patterns, styling conventions, and UX standards.

⚙️ Backend Specialist Agent

Handles server-side logic, database interactions, API design, and integration layers. Aware of the project's data model, security requirements, and legacy code patterns.
In a system like the hospital platform — where you have 10+ years of production history, a public API consumed by third parties, and Spring Security managing access control across sensitive healthcare data — this context isn't optional. It's what separates safe changes from dangerous ones.

🧪 Automated Testing Agent

Generates and runs the test suite for whatever was implemented. Validates coverage, edge cases, and regression safety before anything reaches the commit stage.
The Model Strategy
I use two different AI models in this pipeline — but never on the same task simultaneously.
The deliberate design: one model implements, the other reviews.
Different models have different blind spots. Using one to review the other creates a natural adversarial review layer — without human intervention at every step. The planning agent always runs on the best available model. Specialist agents run on the model most appropriate to the task.
The .md Directive System: Context as Infrastructure
Every agent operates with two layers of context:
Global Directives — a project-agnostic file containing personal coding philosophy, architectural patterns applied across all projects, and general conventions for naming, structure, and documentation.
Project-Specific Directives — a per-project file containing the architecture and tech stack, security rules and sensitive data handling, legacy code constraints and known risks, and a business rule database accessible to all agents via repository.
This is what made the approach viable for complex systems. Agents can't just know how to code. They need to know this system's rules, history, and constraints. The .md system is how that context becomes infrastructure.
Safety Guardrails
This was non-negotiable. The pipeline has explicit protections built into every project-specific agent:

Sensitive data protection — credentials, tokens, and PII never exposed in output or commits
Destructive Git command prevention — force pushes, branch deletions, and history rewrites blocked at the instruction level
Database access control — agents operate with awareness of what they can and cannot touch
Business rule enforcement — a per-project knowledge base ensures domain constraints are respected

Working on systems that handle clinical and financial data in production taught me that safety guardrails aren't optional. They're architecture.
The Full Flow
Client requirement (natural language)
        ↓
Requirements Transcription Agent
→ Structured technical card (Jira/Trello)
        ↓
Planning Agent
→ Task breakdown + agent delegation
        ↓
Frontend Agent + Backend Agent
→ Sequential or parallel depending on task
        ↓
Automated Testing Agent
→ Test generation + validation
        ↓
Cross-model Review
→ One model reviews the other's output
        ↓
Automated Git commit (via Git CLI)
What This Changes in Practice
I built Repetz (repetz.com.br) — a SaaS for pet shop management — using this pipeline throughout development. It went from requirements to production with paying customers, with a codebase I can maintain and evolve confidently.
The difference isn't just speed. It's the quality of attention I bring to the parts that actually require human judgment — architecture decisions, product tradeoffs, security review, and client communication.
The pipeline handles the transitions between execution modes. I stay at the layer where experience matters.
What's Next
This pipeline is project-agnostic by design. The .md directive system makes it configurable for any stack, any domain, any legacy constraint.
I'm continuing to evolve the agent specializations and the cross-model review strategy as the tooling matures.
If you're building in this space or thinking about multi-agent architectures for software development, I'd love to connect.

Lucas da Silva Santos
Full Stack Developer | Co-founder at Repetz
