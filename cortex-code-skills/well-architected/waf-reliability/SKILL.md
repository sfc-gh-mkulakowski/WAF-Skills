---
name: waf-reliability
description: >
  Run the WAF Reliability pillar assessment.
  Use for disaster recovery, failover, business continuity, replication,
  data durability, fault tolerance, and recovery objectives (RTO/RPO).
  Triggers: reliability pillar, DR review, disaster recovery, failover,
  replication, business continuity, RTO, RPO, high availability.
parent_skill: waf-orchestrator
---
# WAF Pillar: Reliability

## When to Load
Load this skill after the orchestrator confirms:
- scope + goals/constraints
- user selected "Reliability"

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
	1. Recovery objectives:
	• Defined RTO (Recovery Time Objective)? (Yes/No/Value)
	• Defined RPO (Recovery Point Objective)? (Yes/No/Value)
	2. Replication & failover:
	• Database replication configured? (Yes/No)
	• Failover groups configured? (Yes/No)
	• Client redirect configured? (Yes/No)
	3. Data protection:
	• Time Travel retention policy defined? (Yes/No/Days)
	• Fail-safe awareness? (Yes/No)
	• Regular data backups/exports? (Yes/No)
	4. Multi-region / multi-cloud:
	• Secondary region configured? (Yes/No)
	• Cross-cloud replication needed? (Yes/No)
	5. Testing & runbooks:
	• DR drills performed regularly? (Yes/No/Frequency)
	• Documented failover runbooks? (Yes/No)
	6. Dependencies:
	• External system dependencies documented? (Yes/No)
	• Graceful degradation patterns in place? (Yes/No)

**STOP** until user responds.

### Step 2: Assess against best-practice themes
Evaluate and summarize findings in these categories:
A) Recovery Objectives & SLAs
- RTO/RPO alignment with business requirements
B) Replication & Failover Architecture
- Database replication, failover groups, client redirect readiness
C) Data Durability & Protection
- Time Travel, Fail-safe, backup strategies
D) Multi-Region / Multi-Cloud Resilience
- Geographic distribution, cross-cloud considerations
E) DR Testing & Operational Readiness
- Drill frequency, runbook documentation, team readiness
F) Dependency Management
- External system awareness, graceful degradation

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
A structured Reliability pillar assessment with prioritized recommendations and optional automation candidates.
