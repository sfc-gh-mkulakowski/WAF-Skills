---
name: waf-operational-excellence
description: >
  Run the WAF Operational Excellence pillar assessment.
  Use for monitoring, alerting, incident response, automation, CI/CD,
  change management, and operational maturity.
  Triggers: operational excellence pillar, monitoring, alerting, observability,
  incident response, automation, CI/CD, DevOps, change management.
parent_skill: waf-orchestrator
---
# WAF Pillar: Operational Excellence

## When to Load
Load this skill after the orchestrator confirms:
- scope + goals/constraints
- user selected "Operational Excellence"

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
	1. Monitoring & observability:
	• Snowflake monitoring dashboards in place? (Yes/No)
	• Account usage data analyzed regularly? (Yes/No)
	• External monitoring integration (SIEM/observability tools)? (Yes/No)
	2. Alerting & notifications:
	• Alerts configured for critical events? (Yes/No)
	• Alert routing/escalation defined? (Yes/No)
	• Proactive vs reactive alerting balance? (Proactive/Reactive/Mixed)
	3. Incident response:
	• Incident response process documented? (Yes/No)
	• On-call rotation defined? (Yes/No)
	• Post-incident review process? (Yes/No)
	4. Automation & CI/CD:
	• Infrastructure as Code (IaC) for Snowflake? (Yes/No)
	• CI/CD pipelines for data pipelines? (Yes/No)
	• Automated testing for data quality? (Yes/No)
	5. Change management:
	• Change approval process? (Yes/No)
	• Environment promotion strategy (dev/test/prod)? (Yes/No)
	• Rollback procedures documented? (Yes/No)
	6. Documentation & knowledge:
	• Runbooks maintained? (Yes/No)
	• Architecture documentation current? (Yes/No)
	• Team training/enablement program? (Yes/No)

**STOP** until user responds.

### Step 2: Assess against best-practice themes
Evaluate and summarize findings in these categories:
A) Monitoring & Observability
- Dashboard coverage, account usage analysis, external integrations
B) Alerting & Notification Strategy
- Alert configuration, routing, proactive vs reactive balance
C) Incident Response & Recovery
- Process maturity, on-call, post-incident reviews
D) Automation & CI/CD Maturity
- IaC adoption, pipeline automation, testing automation
E) Change Management & Governance
- Approval processes, environment strategy, rollback readiness
F) Documentation & Knowledge Management
- Runbook maintenance, architecture docs, team enablement

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
A structured Operational Excellence pillar assessment with prioritized recommendations and optional automation candidates.
