Well Architected Framework Cortex Code Skills

(1) recommended repo layout, 
(2) the orchestrator SKILL.md, 
(3) a pillar SKILL.md (I’m starting with Security & Governance), 
(4) a shared context schema, 
(5) eval cases template + what to validate, and (6) a tight demo script.

Everything below follows the skill structure + stopping-point patterns in your best-practices doc and the repo/eval workflow guidance .

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
