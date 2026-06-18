When AI Wasn't the Hard Part: Lessons from a Workflow Automation Project
Case Study: Building a 95% Accurate AI Email Responder ("My Office Intern")
Olamide Aborowa, MBA, PMP, PSM
June 2026

Building a 95% Accurate AI Email Responder: Lessons from the Real World
Goal
Build an AI-powered email responder capable of handling customer inquiries with 95% accuracy while operating safely within a real business workflow.
The original vision was simple:
Email arrives → AI understands it → AI responds automatically.
I assumed the choice of language model would do most of the heavy lifting.
It didn't.
The Biggest Lesson
The most important realization was that not every business task should be delegated entirely to an LLM.
I initially tried to automate parking dispute workflows.
Eventually I discovered a simpler and safer use case:
Information gathering.
Instead of asking the AI to determine outcomes, the system asks the AI to gather the information required for a human investigation.
That shift dramatically improved reliability.
Initial Assumptions
Like many people entering AI development, I believed the challenge was primarily selecting the right model.
I thought a sufficiently capable LLM could:
Understand customer intent
Determine the correct action
Apply company policy
Generate an accurate response
Send it automatically
In hindsight, I was treating the model as the entire system.
The model was only one component.
What Failed
Assumption #1: The model would understand every scenario
It didn't.
I quickly discovered that customer emails required classification before any response could be generated.
The system first needed to answer:
"What kind of email is this?"
Assumption #2: One prompt could handle every workflow
It couldn't.
Different inquiries required different handling paths.
Routing became necessary.
The system needed to determine:
"Which workflow should handle this?"
Assumption #3: Company documentation was enough
It wasn't.
Providing operational guides improved responses but introduced a new problem:
The AI began making claims it could not actually verify.
For example:
"We reviewed your account."
"We confirmed payment was not received."
The model was following patterns from documentation rather than facts available to it.
Assumption #4: Good responses meant safe automation
They didn't.
Even well-written responses could contain unsupported claims, incorrect assumptions, or policy violations.
A validation layer became necessary.
The system needed to check the AI's work before any response could be trusted.
Architecture Evolution
The project gradually evolved from:
LLM → Response
to:
Classification
→ Routing
→ Operational Guide
→ Generation
→ Validation
→ Governance
→ Workflow Decision
Over time I added:
State management
Persistence
Workflow statuses
Queue management
Metrics
Audit history
Validation rules
Automation controls
Ironically, the majority of the engineering effort occurred around the model rather than inside the model.
In simpler terms:
Over time I discovered the AI could not operate reliably without additional operational infrastructure. The system eventually required:
State management to track workflow progress
Persistence to maintain continuity between interactions
Queue management to support operator review
Metrics to measure performance and identify failure patterns
Audit history to understand system decisions
Validation rules to detect unsupported claims
Automation controls to prevent unsafe actions
Key Pivot
My original goal was fully autonomous email handling.
After testing real customer inquiries, I realized dispute resolution involved too much uncertainty and business risk to automate reliably.
The system was redesigned around information gathering rather than decision making.
This reduced risk, improved consistency, and aligned the automation with a predictable workflow.
What I Learned
Building AI for real-world operations is less about generating text and more about designing systems.
The model is important.
But the surrounding architecture determines whether the solution is trustworthy.
The question changed from:
"Can the AI write a response?"
to:
"Can the workflow safely support the response?"
That distinction changed the entire project.
Current Direction
Today the system focuses on governed automation.
The AI assists with information gathering, routing, and draft generation while workflow controls determine what can be automated and what requires human review.
The goal remains the same:
Deliver reliable automation without sacrificing operational accuracy.

