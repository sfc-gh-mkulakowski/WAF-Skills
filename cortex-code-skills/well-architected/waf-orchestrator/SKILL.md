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
2) Provide the shared context (see "Context Schema" below).
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

## Context Schema (Orchestrator → Pillars)
```yaml
engagement:
  engagement_id: <string>
  engagement_scope: <"account" | "workload" | "single_pillar">
  workload_type: <string | null>
  regulated_data: <"yes" | "no" | "unknown">
  multi_cloud_or_region: <"yes" | "no" | "unknown">
  timeline: <string | null>
goals:
  priority_goals: [<string>, ...]
  constraints: [<string>, ...]
artifacts:
  available_inputs: [<string>, ...]
```

## Output
A structured WAF assessment with prioritized recommendations and optional mapping to PHC/Blueprint candidates.
