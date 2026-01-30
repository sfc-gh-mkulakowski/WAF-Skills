---
name: waf-cost-optimization
description: >
  Run the WAF Cost Optimization & FinOps pillar assessment.
  Use for credit consumption, warehouse spend, storage costs, cost allocation,
  budget management, resource governance, and FinOps practices.
  Triggers: cost pillar, FinOps, credit usage, warehouse costs, storage costs,
  cost optimization, budget, spend analysis, chargeback.
parent_skill: waf-orchestrator
---
# WAF Pillar: Cost Optimization & FinOps

## When to Load
Load this skill after the orchestrator confirms:
- scope + goals/constraints
- user selected "Cost Optimization & FinOps"

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
	1. Cost visibility:
	• Cost monitoring/dashboards in place? (Yes/No)
	• Credit consumption tracked by workload/team? (Yes/No)
	• Storage costs monitored? (Yes/No)
	2. Resource governance:
	• Resource monitors configured? (Yes/No)
	• Warehouse auto-suspend enabled? (Yes/No/Values)
	• Warehouse sprawl concerns? (Yes/No)
	3. Budget management:
	• Budgets defined and alerts configured? (Yes/No)
	• Cost allocation/chargeback model? (Yes/No)
	• FinOps practices in place? (Yes/No)
	4. Compute efficiency:
	• Warehouse sizing reviewed regularly? (Yes/No)
	• Idle warehouse time monitored? (Yes/No)
	• Serverless features evaluated? (Yes/No)
	5. Storage efficiency:
	• Data retention policies defined? (Yes/No)
	• Time Travel retention optimized? (Yes/No)
	• Unused tables/clones cleanup process? (Yes/No)
	6. Data transfer:
	• Cross-region/cross-cloud transfer costs tracked? (Yes/No)
	• Data sharing cost model understood? (Yes/No)

**STOP** until user responds.

### Step 2: Assess against best-practice themes
Evaluate and summarize findings in these categories:
A) Cost Visibility & Monitoring
- Dashboards, consumption tracking, attribution
B) Resource Governance & Controls
- Resource monitors, auto-suspend, warehouse management
C) Budget Management & FinOps
- Budget alerts, chargeback models, FinOps maturity
D) Compute Efficiency
- Warehouse optimization, idle time reduction, serverless adoption
E) Storage Efficiency
- Retention policies, Time Travel optimization, cleanup processes
F) Data Transfer & Sharing Costs
- Cross-region costs, sharing cost models

### Step 3: Findings format (R/Y/G)
For each category, classify:
- Red: material risk / gap
- Yellow: improvement area
- Green: aligned

### Step 4: Recommendations (Prioritized)
Provide:
- "Now (1-2 weeks)"
- "Next (30-60 days)"
- "Later (90+ days)"

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
A structured Cost Optimization & FinOps pillar assessment with prioritized recommendations and optional automation candidates.
