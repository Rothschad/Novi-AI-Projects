# Superpowers: Agentic Software Development Methodology

**Source**: https://github.com/obra/superpowers  
**Version**: v6.0.3  
**Maintainer**: Prime Radiant

## What Is Superpowers?

Superpowers is a comprehensive software development methodology designed specifically for coding agents. It provides a structured workflow that guides agents through systematic planning, implementation, and review processes rather than jumping directly into code generation.

**Key Principle**: *Process before code — structured workflows replace ad-hoc approaches.*

## Core Philosophy

### 1. Test-Driven Development (Mandatory)
- Red-Green-Refactor cycles are non-negotiable
- Write tests BEFORE writing implementation code
- Evidence-based validation instead of assumptions
- Every feature must be verifiable

### 2. Systematic Processes
- Workflows replace ad-hoc decisions
- Clear stages: brainstorm → plan → implement → test → review
- Documented procedures for every task type
- Repeatable, not reactive

### 3. Simplicity as a Goal
- Complexity reduction through careful design
- Minimal moving parts per task
- Prefer explicit over implicit
- Documentation-first approach

### 4. Verification-First Mindset
- Assume nothing, verify everything
- Reproducible results before declaring success
- Testing is not optional
- Multiple review stages catch mistakes early

## Workflow Stages

### Stage 1: Brainstorming (Socratic Dialogue)
**Purpose**: Refine vague specifications into digestible design sections

**Process**:
1. Ask clarifying questions about the feature
2. Identify assumptions and hidden requirements
3. Break down complex features into components
4. Document decisions and rationale
5. Create a design document

**Output**: Clear specifications, acceptance criteria, success metrics

### Stage 2: Planning (Breaking Into Tasks)
**Purpose**: Transform design into 2-5 hour tasks with exact file paths

**Process**:
1. Identify all files that need changes
2. Create atomic tasks (not "build dashboard" but "create vote count component")
3. List exact file paths: `src/components/VoteCounter.tsx`
4. Define verification steps for each task
5. Estimate time per task
6. Order tasks by dependencies

**Task Format**:
```
Task: Create VoteCounter component
Files: src/components/VoteCounter.tsx
Verification:
  - Component renders without errors
  - Displays vote counts for all districts
  - Updates in real-time when new votes arrive
  - Handles loading state
Time: 2 hours
```

### Stage 3: Implementation (Subagent-Driven)
**Purpose**: Execute plan with code review at each stage

**Process**:
1. Execute one task at a time
2. Run verification steps after each task
3. Code review after every 2-3 tasks
4. Fix issues before proceeding
5. Never skip verification

**Two-Stage Review**:
- **Stage 1**: Does the code work? (Functional verification)
- **Stage 2**: Is the code good? (Code quality review)

### Stage 4: Testing (Red-Green-Refactor)
**Purpose**: Ensure every feature works and is maintainable

**Red-Green-Refactor Cycle**:
1. **Red**: Write a test that fails (feature doesn't exist yet)
2. **Green**: Write minimum code to make test pass
3. **Refactor**: Improve code without breaking tests

### Stage 5: Review & Completion
**Purpose**: Final quality check before declaring task done

**Code Review Checklist**:
- [ ] Code is readable and well-named
- [ ] Tests are comprehensive (not just happy path)
- [ ] Security: No credentials in code, inputs validated
- [ ] Performance: No N+1 queries, reasonable bundle size
- [ ] Documentation: Complex logic is explained
- [ ] Dependencies: No unnecessary packages
- [ ] Git history: Commits are logical and descriptive

## Best Practices: Superpowers for Public Good App

### 1. Planning Phase (Day 1)
- Use Socratic dialogue to refine requirements
- Document in DESIGN.md
- Create task breakdown with file paths
- Define verification steps for each task

### 2. Implementation Phase (Days 2-3)
- For each task: Write failing test (RED)
- Implement minimum code (GREEN)
- Refactor for quality (REFACTOR)
- Run verification steps
- Code review before moving on
- Commit with clear message

### 3. Testing Phase (Day 3)
- Unit tests for business logic (80%+ coverage)
- Integration tests for API endpoints
- E2E tests for user workflows
- Edge case handling
- Security tests (XSS, auth, input validation)

### 4. Review & Completion (Day 4)
- Code quality review (readability, security)
- Performance review (bundle size, API response time)
- Security audit (CORS, auth, input validation)
- Documentation (README, deployment guide)

## Superpowers vs. Anthropic Skills

| Aspect | Anthropic Skills | Superpowers |
|--------|------------------|------------|
| **Focus** | Task patterns | Development methodology |
| **Scope** | Specific skills | End-to-end workflow |
| **Use Case** | Repeatable tasks | Software development |
| **Structure** | Modular, mix-and-match | Staged, sequential |
| **Output** | Consistent results | Production-ready code |
| **Testing** | Not emphasized | Mandatory (TDD) |
| **Review** | Optional | Multi-stage, required |

## Common Pitfalls to Avoid

### ❌ Don't:
1. Jump to coding without planning (violates Superpowers)
2. Write code before tests (violates TDD)
3. Skip verification steps (violates verification-first mindset)
4. Make tasks too large (>5 hours = should be broken down)
5. Skip code review (Quality requires review)
6. Assume requirements are clear (Always brainstorm first)
7. Test only happy path (Edge cases matter)
8. Merge without all tests passing (Tests are non-negotiable)

### ✓ Do:
1. Brainstorm and design first
2. Write tests before code
3. Verify every task before moving on
4. Keep tasks small and atomic
5. Review code at each stage
6. Ask clarifying questions
7. Test edge cases and errors
8. Require green tests before merge

## Key Resources

- **GitHub**: https://github.com/obra/superpowers
- **Discord Community**: Active support and examples
- **Commercial Support**: Available from Prime Radiant
- **Release Notes**: Track v6.0.3 changes

## Summary: Superpowers Framework

Superpowers is a **structured workflow for agents building software**:

1. **Brainstorm** → Design clarification
2. **Plan** → Task breakdown with verification
3. **Implement** → TDD, test-first approach
4. **Test** → Red-green-refactor cycles
5. **Review** → Multi-stage code quality checks

**Core Mindset**: Process > Code, Tests > Assumptions, Verification > Hope

For the Public Good app: Follow Superpowers for development, use Anthropic Skills for repeatable patterns within that workflow.
