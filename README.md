Well Architected Framework Cortex Code Skills

(1) recommended repo layout, 
(2) the orchestrator SKILL.md, 
(3) a pillar SKILL.md (I’m starting with Security & Governance), 
(4) a shared context schema, 
(5) eval cases template + what to validate, and (6) a tight demo script.

Everything below follows the skill structure + stopping-point patterns in your best-practices doc and the repo/eval workflow guidance .

1) Recommended repo layout
This matches how the skills repo expects each skill to be a self-contained directory with SKILL.md 
README
.

cortex-code-skills/
└── well-architected/
    ├── waf-orchestrator/
    │   └── SKILL.md
    ├── waf-security-governance/
    │   └── SKILL.md
    ├── waf-reliability/
    │   └── SKILL.md
    ├── waf-performance/
    │   └── SKILL.md
    ├── waf-cost-optimization/
    │   └── SKILL.md
    ├── waf-operational-excellence/
    │   └── SKILL.md
    └── evals/
        └── eval_cases.csv
Why this structure: it keeps each pillar skill small and testable (recommended in skill best practices) and makes eval-driven iteration straightforward .

2) WAF Orchestrator: well-architected/waf-orchestrator/SKILL.md

---
name: waf-orchestrator
description: >
  Run a Snowflake Well-Architected Framework (WAF) engagement end-to-end.
  Use when users ask for: well-architected review, WAF assessment, best practices review,
  architecture assessment, health check, posture review, pillar review (security, reliability,
  performance, cost, operational excellence). Triggers: WAF, well architected, posture review,
  best practices assessment, architecture review.
---
# Snowflake Well-Architected Framework (WAF) Orchestrator
This skill runs a structured WAF engagement by:
1) scoping the engagement,
2) routing to pillar skills,
3) consolidating findings into a customer-ready output,
4) mapping items to automation candidates (PHC / Blueprints) when applicable.
## When to Use / Load
Use this skill when the user wants a WAF engagement, pillar assessment, or best-practices posture review.
Do NOT use for:
- single SQL tuning requests
- unrelated Snowflake feature Q&A

## Workflow
### Step 1: Capture scope (MANDATORY)
Ask the user:
What is the scope of the WAF engagement?
	1. Entire Snowflake account / platform posture
	2. Specific workload (e.g., ingestion, analytics, ML/GenAI, data sharing)
	3. Single pillar deep dive
Please select (1-3) and briefly describe the workload (if #2).

**STOP** until user responds.
### Step 2: Capture goals + constraints (MANDATORY)
Ask the user:
What are the top goals and constraints?
Goals (pick up to 3):
	• Reduce risk / improve security posture
	• Improve reliability / DR / recovery
	• Improve performance / concurrency
	• Reduce cost / improve FinOps
	• Improve operability (monitoring, incident response)
Constraints:
	• Regulated data? (Yes/No)
	• Multi-cloud / cross-region needs? (Yes/No)
	• Timeline: (weeks/months)

**STOP** until user responds.
### Step 3: Select pillars (MANDATORY)
Ask the user:
Which pillar(s) should we run?
	1. Security & Governance
	2. Reliability
	3. Performance Optimization
	4. Cost Optimization & FinOps
	5. Operational Excellence
Please select (1-5).

**STOP** until user responds.

### Step 4: Route to pillar skills (Intent Table)
Use a single routing table (keep routing logic centralized).
| Pillar | Load Skill Directory |
|---|---|
| 1 | well-architected/waf-security-governance |
| 2 | well-architected/waf-reliability |
| 3 | well-architected/waf-performance |
| 4 | well-architected/waf-cost-optimization |
| 5 | well-architected/waf-operational-excellence |

For each selected pillar:
1) **Load** the pillar skill.
2) Provide the shared context (see “Context Schema” below).
3) Run the pillar workflow and collect outputs.
### Step 5: Consolidate findings (MANDATORY)
Combine pillar outputs into:
- Executive summary (what matters + why)
- Key risks (top 3-5)
- Quick wins (1-2 week items)
- Strategic improvements (30-90 day items)
- Suggested next steps and owners (SE/TAM/PS/Partner)
### Step 6: Automation mapping (Optional)
If the user asks, or if findings are repetitive/measurable:
- Flag items suitable for Proactive Health Check (PHC)
- Flag items suitable for Blueprint defaults/accelerators

### Step 7: Present final deliverable (MANDATORY CHECKPOINT)
Present the final report in this structure:
1) Scope + goals
2) Pillar summaries (R/Y/G)
3) Prioritized backlog (Now / Next / Later)
4) Automation candidates (PHC / Blueprints)
5) Proposed engagement plan (who does what)
**STOP** and ask:
Do you want this formatted as:
	1. Customer-ready summary
	2. Internal delivery plan (RACI)
	3. Both
Please select (1-3).

## Stopping Points
- After Step 1 scope selection
- After Step 2 goals/constraints
- After Step 3 pillar selection
- After Step 7 final deliverable (format confirmation)
## Output
A structured WAF assessment with prioritized recommendations and optional mapping to PHC/Blueprint candidates.
This follows the “required sections + stopping points + clear triggers” guidance .

3) First pillar to implement: Security & Governance (why + SKILL.md)
Start with Security & Governance because it consistently appears in every customer segment (regulated/non-regulated), is easiest to structure into repeatable questions, and yields clear, high-confidence outputs that eval well.
well-architected/waf-security-governance/SKILL.md

---
name: waf-security-governance
description: >
  Run the WAF Security & Governance pillar assessment.
  Use for Snowflake access control, RBAC, privacy, encryption, network security,
  data collaboration controls, governance policies, and auditability.
  Triggers: security pillar, governance pillar, RBAC review, masking policies,
  row access policies, encryption, key management, private connectivity, compliance.
parent_skill: waf-orchestrator
---
# WAF Pillar: Security & Governance
## When to Load
Load this skill after the orchestrator confirms:
- scope + goals/constraints
- user selected “Security & Governance”
## Inputs (from orchestrator context)
Use:
- engagement_scope
- workload_type
- regulated_data
- multi_cloud_or_region
- priority_goals
If any are missing, request them and STOP.
## Workflow
### Step 1: Current-state discovery (MANDATORY)
Ask the user:
Answer what you can (unknown is fine):
	1. Identity & access:
	• Do you use database roles? (Yes/No/Unknown)
	• Any role design standard (e.g., functional roles)? (Yes/No)
	2. Data protection:
	• Masking policies? (Yes/No)
	• Row access policies? (Yes/No)
	• Tokenization / external privacy tooling? (Yes/No)
	3. Network posture:
	• Private connectivity enforced (e.g., PrivateLink/PSC)? (Yes/No)
	• Network rules / policies configured? (Yes/No)
	4. Key management:
	• Customer-managed keys (BYOK) or similar? (Yes/No)
	• Key rotation requirements? (Yes/No)
	5. Audit & monitoring:
	• Central audit approach (event tables/account usage) in place? (Yes/No)
	• Any security monitoring integration? (Yes/No)
	6. Data collaboration:
	• Sharing / clean rooms used? (Yes/No)
	• Any restrictions on outbound sharing? (Yes/No)

**STOP** until user responds.

### Step 2: Assess against best-practice themes
Evaluate and summarize findings in these categories:
A) Authentication & Access Control
- Least privilege, separation of duties, standardized role design
B) Policy-Based Data Protection
- Masking / row access policies; consistency and coverage
C) Network Security / Zero Trust
- Private connectivity, network policy posture
D) Encryption & Key Management
- Key ownership model, rotation expectations, lifecycle considerations
E) Monitoring, Auditability, and Governance
- Audit data access patterns; operational guardrails
F) Collaboration & Privacy-Preserving Analytics
- Data sharing controls; clean-room and privacy patterns (if used)

### Step 3: Findings format (R/Y/G)
For each category, classify:
- Red: material risk / gap
- Yellow: improvement area
- Green: aligned

### Step 4: Recommendations (Prioritized)
Provide:
- “Now (1-2 weeks)”
- “Next (30-60 days)”
- “Later (90+ days)”
If a recommendation implies making changes, do NOT apply changes.
Only propose.
### Step 5: Automation mapping (Optional)
If the user asks about automation:
- Identify which checks could be measured regularly (PHC candidates)
- Identify which controls could be standardized defaults (Blueprint candidates)
### Step 6: MANDATORY CHECKPOINT
Before returning to orchestrator, present:
- 3–5 key findings
- Top 5 recommended actions
- 1–3 automation candidates (if applicable)
Ask:
Approve these findings for inclusion in the consolidated WAF report? (Yes/No/Edits)

**STOP** until user responds.
## Stopping Points
- After Step 1 (discovery)
- After Step 6 (approval gate)
## Output
A structured Security & Governance pillar assessment with prioritized recommendations and optional automation candidates.
This uses explicit approval gates and stopping points as required in the best practices .

4) Shared context schema (passed from orchestrator → pillar skills)
Keep this small (skills compete for context window) 
SKILL_BEST_PRACTICES
.

## Context Schema (Orchestrator → Pillars)
engagement:
  engagement_id: <string>
  engagement_scope: <"account" | "workload" | "single_pillar">
  workload_type: <string | null>   # ingestion, analytics, ml/genai, sharing, etc.
  regulated_data: <"yes" | "no" | "unknown">
  multi_cloud_or_region: <"yes" | "no" | "unknown">
  timeline: <string | null>
goals:
  priority_goals: [<string>, ...]  # up to 3
  constraints: [<string>, ...]     # e.g., "no downtime", "bank regulatory", etc.
artifacts:
  available_inputs: [<string>, ...]  # e.g., "PHC output", "account usage exports", "RBAC doc"

5) Eval-driven development: what to write + how to validate
The repo guidance is explicit: eval cases are the spec and you measure improvements via Pass@k . The handbook also clarifies each eval has setup/execution/validation steps and validation should be a checklist .
A practical eval plan (WAF-focused)
Start with 6 eval cases:
	1. Full WAF, all pillars, regulated, multi-region
	2. Single pillar: Security, regulated, private connectivity required
	3. Single pillar: Cost, “high spend / warehouse sprawl”
	4. Workload scope: streaming ingestion + reliability concerns
	5. Workload scope: GenAI app + governance concerns
	6. “Confusion test”: user asks a vague request; orchestrator must stop and ask scope/pillars
CSV template (fields vary by your internal eval harness)
I won’t invent exact column names, but your docs confirm you need:
	• a unique CONV_ID
	• clear user instruction (“WHAT not HOW”)
	• prerequisites
	• validation type + checklist
	• skill directories included in the run
Example structure you can adapt:

CONV_ID,USER_INSTRUCTION,PREREQUISITES,SKILL_DIRECTORIES,VALIDATION
waf-orch-scope-gating,"Run a WAF review. I’m not sure which pillar. Ask me the right questions first.",,"well-architected/waf-orchestrator","generic: must ask scope + goals + pillar selection; must STOP after questions"
waf-sec-regulated,"Do a Security & Governance WAF review for a regulated healthcare workload with strict network isolation.",,"well-architected/waf-orchestrator;well-architected/waf-security-governance","generic: must produce R/Y/G categories + prioritized Now/Next/Later + approval gate"
Validation checklist examples
Use checklist-style validation as recommended 
Coding Agent Developer Handbook
:
	• Did it ask scope first?
	• Did it ask goals/constraints?
	• Did it route correctly to the pillar skill?
	• Did pillar output include R/Y/G?
	• Did it include a prioritized backlog?
	• Did it include a mandatory approval gate?

6) Data Summit demo script (8–10 minutes, crisp)
Goal: show “WAF is executable” + “Snowflake differentiator: guidance → automation”.
Demo flow
	1. Set the scene (30s)
		○ “Customer wants a WAF review for a GenAI + analytics platform. They need security posture, cost control, and reliability.”
	2. Trigger orchestrator (30s)
		○ Prompt: “Run a Snowflake Well-Architected review.”
		○ Show it asks scope/goals/pillars (this is the trust moment).
	3. Choose “workload” + 2 pillars (60s)
		○ Workload: “GenAI app on Snowflake + analytics”
		○ Pillars: “Security & Governance” + “Cost Optimization”
	4. Run Security pillar (2–3 min)
		○ Show structured discovery questions
		○ Show R/Y/G output + Now/Next/Later
		○ Show approval gate
	5. Run Cost pillar (2–3 min)
		○ Show it produces actionable cost controls and governance patterns
	6. Consolidation + automation mapping (2 min)
		○ Orchestrator produces final report:
			§ Exec summary
			§ Top risks + quick wins
			§ “Candidates for PHC automation / Blueprint defaults”
	7. Close (30s)
		○ “WAF isn’t a PDF. It’s an engagement engine: consistent, repeatable, measurable.”

7) How customers should use this (for what + when)
Use Cortex Code WAF skills:
	• Before go-live (preventive posture)
	• Quarterly operational reviews (repeatable governance)
	• Post-incident (systematic reliability/process improvements)
	• Before scale / new workloads (performance + cost guardrails)
	• During modernization (standardize practices + reduce drift)
And internally, your teams use the same thing to ensure a consistent deliverable across SE/TAM/PS/Partners.<img width="1480" height="12070" alt="image" src="https://github.com/user-attachments/assets/d489db0f-766a-4d4f-8920-e6ea8d5a1b45" />
