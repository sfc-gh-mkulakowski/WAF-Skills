---
name: waf-performance
description: >
  Run the WAF Performance Optimization pillar assessment.
  Use for query performance, warehouse sizing, clustering, caching,
  concurrency, resource optimization, and workload management.
  Triggers: performance pillar, query optimization, warehouse sizing,
  clustering, caching, concurrency, slow queries, resource contention.
parent_skill: waf-orchestrator
---
# WAF Pillar: Performance Optimization

## When to Load
Load this skill after the orchestrator confirms:
- scope + goals/constraints
- user selected "Performance Optimization"

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
	1. Warehouse strategy:
	• Warehouse sizing approach defined? (Yes/No)
	• Multi-cluster warehouses used? (Yes/No)
	• Auto-suspend/resume configured? (Yes/No/Values)
	2. Query performance:
	• Query profiling/monitoring in place? (Yes/No)
	• Known slow queries or bottlenecks? (Yes/No)
	• Query tagging used? (Yes/No)
	3. Data organization:
	• Clustering keys defined for large tables? (Yes/No)
	• Search optimization service used? (Yes/No)
	• Materialized views used? (Yes/No)
	4. Caching & efficiency:
	• Result cache awareness? (Yes/No)
	• Warehouse cache optimization considered? (Yes/No)
	5. Concurrency management:
	• Resource monitors configured? (Yes/No)
	• Workload segregation (separate warehouses by workload)? (Yes/No)
	• Query queuing issues observed? (Yes/No)
	6. Data loading:
	• Optimized file sizes for loading? (Yes/No)
	• Parallel loading strategies? (Yes/No)
	• Snowpipe or streaming ingestion? (Yes/No)

**STOP** until user responds.

### Step 2: Assess against best-practice themes
Evaluate and summarize findings in these categories:
A) Warehouse Strategy & Sizing
- Right-sizing, multi-cluster configuration, auto-suspend/resume
B) Query Performance & Optimization
- Query profiling, optimization patterns, execution plan analysis
C) Data Organization & Clustering
- Clustering keys, search optimization, micro-partition efficiency
D) Caching & Result Reuse
- Result cache utilization, warehouse cache optimization
E) Concurrency & Workload Management
- Resource monitors, workload isolation, queue management
F) Data Loading & Ingestion Performance
- File sizing, parallel loading, streaming ingestion patterns

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
A structured Performance Optimization pillar assessment with prioritized recommendations and optional automation candidates.
