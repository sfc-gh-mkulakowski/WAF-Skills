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
- user selected "Security & Governance"

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
A structured Security & Governance pillar assessment with prioritized recommendations and optional automation candidates.
