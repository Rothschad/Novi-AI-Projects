# Agent Skills Installed

**Total Skills**: 91  
**Installation Date**: 2026-06-24  
**Storage**: `.agents/skills/` (symlinked to `.claude/skills/`)

---

## Collections Installed

### 1. Superpowers (obra/superpowers) - 6 Skills
Development methodology for coding agents with TDD focus.

- **brainstorming** — Socratic design refinement before coding
- **test-driven-development** — RED-GREEN-REFACTOR cycle
- **writing-plans** — Detailed implementation planning
- **subagent-driven-development** — Fast iteration with two-stage review
- **systematic-debugging** — Root cause analysis process
- **using-git-worktrees** — Parallel development branches

---

### 2. Context Engineering (muratcankoylan/Agent-Skills-for-Context-Engineering) - 10 Skills
Context window management and multi-agent optimization.

**Foundational:**
- **context-fundamentals** — Context anatomy and importance
- **context-degradation** — Context failure patterns
- **context-compression** — Compression strategies

**Architectural:**
- **multi-agent-patterns** — Orchestrator, peer-to-peer, hierarchical
- **memory-systems** — Short/long-term, graph-based memory
- **tool-design** — Creating tools for agents
- **filesystem-context** — Using filesystem for dynamic context
- **hosted-agents** — Background agents with sandboxed VMs

**Operational:**
- **context-optimization** — Compaction, masking, caching
- **latent-briefing** — State transfer via KV cache
- **evaluation** — Frameworks for evaluating agent systems
- **advanced-evaluation** — LLM-as-a-Judge techniques

---

### 3. Marketing Skills (coreyhaines31/marketingskills) - 45 Skills
Marketing tasks for technical marketers and founders.

**Conversion & Engagement:**
- **cro** — Page/form optimization
- **signup** — Registration flows
- **onboarding** — Post-signup activation
- **popups** — Modals and overlays
- **paywalls** — In-app upgrade moments
- **lead-magnets** — Lead generation
- **offers** — Product offers and positioning

**Content & Copy:**
- **copywriting** — Marketing page copy
- **copy-editing** — Edit existing content
- **cold-email** — B2B cold outreach
- **emails** — Automated email flows
- **social** — Social media content
- **content-strategy** — Content planning
- **marketing-psychology** — Behavioral principles

**SEO & Discovery:**
- **seo-audit** — Technical and on-page SEO
- **ai-seo** — AI search optimization
- **programmatic-seo** — Scaled page generation
- **site-architecture** — Page hierarchy
- **schema** — Structured data
- **directory-submissions** — Directory optimization

**Paid & Distribution:**
- **ads** — Google, Meta, LinkedIn campaigns
- **ad-creative** — Bulk ad creation
- **analytics** — Event tracking setup
- **ab-testing** — Experiment design
- **aso** — App Store Optimization

**Strategy & Planning:**
- **marketing-plan** — Full marketing strategy
- **marketing-ideas** — Content brainstorming
- **competitors** — Competitor analysis
- **competitor-profiling** — Detailed profiles
- **customer-research** — Customer interviews
- **product-marketing** — Product positioning
- **brand-guidelines** — Brand consistency
- **co-marketing** — Partnership campaigns
- **community-marketing** — Community building
- **launch** — Product launch strategy
- **public-relations** — PR and media
- **prospecting** — Lead prospecting
- **referrals** — Referral programs
- **revops** — Revenue operations
- **sales-enablement** — Sales support

---

### 4. Anthropic Skills (anthropics/skills) - 18 Skills
Official skill examples and document manipulation.

**Document Skills:**
- **docx** — Create/edit Word documents
- **pdf** — Work with PDFs
- **pptx** — Create presentations
- **xlsx** — Work with Excel files

**Creative & Design:**
- **algorithmic-art** — Generative art
- **canvas-design** — HTML5 canvas graphics
- **frontend-design** — Frontend design patterns
- **image** — Image generation/manipulation
- **theme-factory** — Design system generation
- **video** — Video generation/editing

**Development & Technical:**
- **webapp-testing** — Web app testing
- **mcp-builder** — MCP server generation
- **slack-gif-creator** — Slack gif creation
- **web-artifacts-builder** — Web artifact creation

**Utilities:**
- **claude-api** — Claude API reference
- **skill-creator** — Create custom skills
- **writing-skills** — Writing improvement

---

## How to Use These Skills

### Automatic Activation
Skills activate automatically based on task context:

```
"Help me optimize this landing page for conversions"
→ Automatically uses the cro skill

"Write tests for this function"
→ Automatically uses the test-driven-development skill

"Optimize context usage in my agent"
→ Automatically uses the context-optimization skill
```

### Manual Invocation (Rare)
If the agent doesn't recognize the context, call manually:

```
/cro
/test-driven-development
/context-optimization
/brainstorming
```

---

## Quick Reference: Skills by Use Case

### For Development
- `brainstorming` — Design before coding
- `writing-plans` — Break down work
- `test-driven-development` — TDD workflow
- `systematic-debugging` — Debug issues
- `requesting-code-review` — Get code review
- `receiving-code-review` — Accept feedback
- `finishing-a-development-branch` — Finalize PR

### For Multi-Agent Systems
- `multi-agent-patterns` — Architecture design
- `dispatching-parallel-agents` — Parallel execution
- `latent-briefing` — State transfer
- `memory-systems` — Persistent memory
- `context-optimization` — Token efficiency

### For Marketing & Content
- `cro` — Landing page optimization
- `copywriting` — Marketing copy
- `seo-audit` — SEO improvement
- `social` — Social media strategy
- `content-strategy` — Content planning
- `ads` — Ad campaigns
- `product-marketing` — Product positioning

### For Documentation
- `docx` — Word documents
- `pdf` — PDF creation/editing
- `pptx` — Presentations
- `xlsx` — Excel spreadsheets
- `writing-skills` — Writing improvement

### For Design & Creative
- `frontend-design` — UI/UX patterns
- `canvas-design` — Graphics
- `image` — Image generation
- `video` — Video creation
- `algorithmic-art` — Generative art

---

## Skills Directory Structure

```
.agents/skills/
├── brainstorming/
│   ├── SKILL.md              (Main instructions)
│   ├── references/           (Documentation)
│   ├── scripts/              (Code examples)
│   └── examples/             (Usage examples)
├── test-driven-development/
├── context-optimization/
├── cro/
├── ... (81 more skills)
└── xlsx/
```

Each skill contains:
- **SKILL.md** — Instructions and examples
- **references/** — Additional documentation
- **scripts/** — Executable code
- **evals/** — Evaluation criteria

---

## Key Points

1. **Skills are automatic** — No need to call them manually in most cases
2. **Progressive loading** — Only skill names loaded at startup
3. **Composable** — Skills work together and reference each other
4. **Updatable** — Reinstall with `npx skills add` to get latest versions
5. **Customizable** — Create custom skills in `.agents/skills/custom/`

---

## Skill Statistics

| Collection | Count | Purpose |
|-----------|-------|---------|
| **Superpowers** | 6 | Development methodology |
| **Context Engineering** | 10 | Agent optimization |
| **Marketing** | 45 | Marketing & growth |
| **Anthropic** | 18 | Documents & creative |
| **Other** | 12 | Various utilities |
| **TOTAL** | **91** | Complete skill set |

---

## For Public Good App Development

Relevant skills for your project:

### Development
- `brainstorming` — Design app features
- `test-driven-development` — Write tests first
- `writing-plans` — Plan implementation
- `subagent-driven-development` — Parallel development

### Multi-Agent & Context
- `multi-agent-patterns` — If adding subagents
- `context-optimization` — For efficient LLM usage
- `memory-systems` — For persistent state

### Documentation
- `docx`, `pdf`, `pptx` — Create guides and docs
- `markdown` — Documentation

### Marketing (When Launching)
- `cro` — Landing page optimization
- `copywriting` — App description
- `social` — Social media strategy
- `product-marketing` — App positioning

---

## Installation Details

**Installed from:**
- https://github.com/obra/superpowers
- https://github.com/muratcankoylan/Agent-Skills-for-Context-Engineering
- https://github.com/coreyhaines31/marketingskills
- https://github.com/anthropics/skills

**Location:** `.agents/skills/` with `.claude/skills/` symlink  
**Git committed:** Yes, all 693 files tracked  
**Ready to use:** Yes, immediately

---

## Next Steps

1. ✓ Skills installed and committed
2. Start development using Superpowers methodology
3. Use marketing skills when launching the app
4. Leverage context engineering for efficiency
5. Reference Anthropic skills for document generation

Skills are now available to Claude Code and other agents!
