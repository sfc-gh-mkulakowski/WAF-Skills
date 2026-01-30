# Snowflake Well-Architected Framework (WAF) Skills

A set of Cortex Code skills for running structured Snowflake Well-Architected Framework engagements.

## Overview

These skills enable consistent, repeatable WAF assessments by guiding users through structured discovery questions, best-practice evaluations, and prioritized recommendations across five pillars.

## Skill Structure

```
well-architected/
├── waf-orchestrator/SKILL.md          # Main entry point
├── waf-security-governance/SKILL.md   # Pillar 1
├── waf-reliability/SKILL.md           # Pillar 2
├── waf-performance/SKILL.md           # Pillar 3
├── waf-cost-optimization/SKILL.md     # Pillar 4
├── waf-operational-excellence/SKILL.md # Pillar 5
└── evals/eval_cases.csv               # Test cases
```

## When to Use

| Scenario | Description |
|----------|-------------|
| Before go-live | Preventive posture review |
| Quarterly reviews | Repeatable governance assessments |
| Post-incident | Systematic reliability/process improvements |
| Before scale/new workloads | Performance + cost guardrails |
| During modernization | Standardize practices + reduce drift |

## How to Trigger

Use natural language prompts like:
- "Run a WAF review"
- "Do a well-architected assessment"
- "Best practices review for my Snowflake account"
- "Security pillar deep dive"
- "Cost optimization assessment"

## Workflow

### 1. Orchestrator Entry
The `waf-orchestrator` skill is the main entry point. It:
1. Captures engagement scope (account/workload/single pillar)
2. Gathers goals and constraints
3. Routes to selected pillar skills
4. Consolidates findings into a final report

### 2. Pillar Assessments
Each pillar skill follows a consistent pattern:
1. **Discovery**: Structured questions about current state
2. **Assessment**: Evaluation against best-practice themes
3. **Findings**: R/Y/G classification per category
4. **Recommendations**: Prioritized as Now/Next/Later
5. **Approval Gate**: User confirms findings before consolidation

### 3. Final Deliverable
The orchestrator produces:
- Executive summary
- Key risks (top 3-5)
- Quick wins (1-2 week items)
- Strategic improvements (30-90 days)
- Automation candidates (PHC/Blueprints)

## Pillars

### 1. Security & Governance
- Authentication & access control (RBAC, least privilege)
- Policy-based data protection (masking, row access)
- Network security (PrivateLink, network policies)
- Encryption & key management
- Audit & monitoring
- Data collaboration controls

### 2. Reliability
- Recovery objectives (RTO/RPO)
- Replication & failover architecture
- Data durability (Time Travel, Fail-safe)
- Multi-region/multi-cloud resilience
- DR testing & operational readiness
- Dependency management

### 3. Performance Optimization
- Warehouse strategy & sizing
- Query performance & optimization
- Data organization & clustering
- Caching & result reuse
- Concurrency & workload management
- Data loading performance

### 4. Cost Optimization & FinOps
- Cost visibility & monitoring
- Resource governance & controls
- Budget management & FinOps maturity
- Compute efficiency
- Storage efficiency
- Data transfer costs

### 5. Operational Excellence
- Monitoring & observability
- Alerting & notifications
- Incident response
- Automation & CI/CD
- Change management
- Documentation & knowledge management

## Stopping Points

The skills include mandatory stopping points to ensure user engagement:

| Location | Purpose |
|----------|---------|
| After scope selection | Confirm engagement boundaries |
| After goals/constraints | Validate priorities |
| After pillar selection | Confirm assessment focus |
| After pillar discovery | Validate current-state understanding |
| After pillar findings | Approve before consolidation |
| After final report | Choose output format |

## Context Schema

Data passed between orchestrator and pillar skills:

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

## Output Formats

Final deliverables can be formatted as:
1. **Customer-ready summary**: External-facing report
2. **Internal delivery plan (RACI)**: Team assignment matrix
3. **Both**: Combined documentation

## Automation Mapping

Findings can be mapped to:
- **PHC (Proactive Health Check)**: Recurring measurable checks
- **Blueprint candidates**: Standardized defaults/accelerators

## Evaluation

Test cases in `evals/eval_cases.csv` cover:
- Full WAF with all pillars
- Single pillar assessments
- Workload-scoped reviews
- Scope gating (confusion tests)

### Validation Checklist
- Did it ask scope first?
- Did it ask goals/constraints?
- Did it route correctly to pillar skills?
- Did pillar output include R/Y/G?
- Did it include prioritized backlog?
- Did it include mandatory approval gates?

## Best Practices

1. **Always complete discovery**: Don't skip current-state questions
2. **Respect stopping points**: Wait for user responses
3. **Propose, don't apply**: Recommendations only; no automatic changes
4. **Use R/Y/G consistently**: Red=risk, Yellow=improvement, Green=aligned
5. **Prioritize clearly**: Now (1-2 weeks), Next (30-60 days), Later (90+ days)
