# /spec-forge

> Turn vague ideas into battle-tested implementation plans

**spec-forge** transforms rough feature descriptions into comprehensive, sectionized implementation plans through structured research, stakeholder interviews, and multi-LLM review.

## The Problem

```
You: "Claude, build me an auth system"
Claude: *starts coding immediately*
Result: Back-and-forth iterations, missed edge cases, scope creep
```

## The Solution

```
You: "/spec-forge @planning/auth-spec.md"
spec-forge: Research → Interview → Spec → Plan → External Review → Sections
Result: Clear implementation roadmap, reviewed by multiple LLMs, ready for execution
```

## Table of Contents

- [Workflow](#workflow)
- [Quick Start](#quick-start)
- [When to Use](#when-to-use)
- [Output Files](#output-files)
- [External Review](#external-review)
- [Resuming](#resuming)
- [Best Practices](#best-practices)
- [Implementing the Plan](#implementing-the-plan)
- [Integration with ralph-loop (Optional)](#integration-with-ralph-loop-optional)
- [File Structure](#file-structure)

## Workflow

```
┌─────────────────────────────────────────────────────────────────┐
│                      spec-forge pipeline                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   /spec-forge @spec.md                                          │
│          │                                                      │
│          ▼                                                      │
│   ┌──────────────┐     ┌──────────────┐     ┌──────────────┐    │
│   │   Research   │ ──▶ │  Interview   │ ──▶ │     Spec     │    │
│   │  (optional)  │     │  (5-10 Q&A)  │     │  Synthesis   │    │
│   └──────────────┘     └──────────────┘     └──────────────┘    │
│                                                   │             │
│                                                   ▼             │
│   ┌──────────────┐     ┌──────────────┐     ┌──────────────┐    │
│   │   Section    │ ◀── │   Integrate  │ ◀── │   External   │    │
│   │  Splitting   │     │   Feedback   │     │  LLM Review  │    │
│   └──────────────┘     └──────────────┘     └──────────────┘    │
│          │                                                      │
│          ▼                                                      │
│   ┌──────────────────────────────────────────────────────────┐  │
│   │  sections/section-01-*.md  sections/section-02-*.md ...  │  │
│   │  (Self-contained, parallel-ready implementation units)   │  │
│   └──────────────────────────────────────────────────────────┘  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

## Quick Start

**1. Create a spec file**

```bash
mkdir -p planning
cat > planning/auth-spec.md << 'EOF'
# Authentication System

Need OAuth2 login with Google and GitHub.
Sessions stored in Redis, JWT for API auth.
EOF
```

Your spec can be detailed or just bullet points - the interview phase extracts the details.

**2. Run spec-forge**

```
/spec-forge @planning/auth-spec.md
```

**3. Follow the prompts**

Answer research and interview questions. Review the generated plan. Done.

## When to Use

**Use spec-forge when:**
- Requirements are fuzzy and need clarification
- The feature is complex enough to benefit from external review
- You want implementation sections that can be worked on in parallel
- You prefer thinking before coding

**Skip spec-forge when:**
- Simple bug fixes or one-file changes
- Requirements are already crystal clear
- You just want to start coding

## Output Files

After running spec-forge, your planning directory contains:

```
planning/
├── your-spec.md                 # Your original input
├── claude-research.md           # Web + codebase research findings
├── claude-interview.md          # Q&A transcript
├── claude-spec.md               # Synthesized specification
├── claude-plan.md               # Implementation plan
├── claude-integration-notes.md  # Review feedback decisions
├── claude-ralph-loop-prompt.md  # Ready-to-run ralph-loop prompt
├── reviews/
│   ├── gemini-review.md         # Gemini's feedback
│   └── codex-review.md          # Codex's feedback
└── sections/
    ├── index.md                 # Section manifest & dependencies
    ├── section-01-*.md          # Implementation unit 1
    ├── section-02-*.md          # Implementation unit 2
    └── ...
```

### Key Files

| File | Purpose |
|------|---------|
| `claude-plan.md` | The main deliverable - complete implementation plan |
| `sections/*.md` | Self-contained units ready for implementation |
| `reviews/*.md` | External perspectives on your plan |
| `claude-ralph-loop-prompt.md` | One-command execution with ralph-loop |

## External Review

spec-forge uses **Gemini CLI** and **Codex CLI** to get independent reviews of your plan.

### Requirements

Install at least one:

```bash
# Gemini CLI (Google)
# See: https://github.com/google-gemini/gemini-cli

# Codex CLI (OpenAI)
# See: https://github.com/openai/codex
```

### What Reviewers Check

Both LLMs analyze your plan for:
- Potential footguns and edge cases
- Missing considerations
- Security vulnerabilities
- Performance issues
- Architectural problems
- Unclear requirements

### No CLI Installed?

If neither CLI is available, spec-forge will skip the external review step and continue with the workflow.

## Resuming

If the workflow is interrupted (context limit, need a break), just re-run with the same spec:

```
/spec-forge @planning/auth-spec.md
```

spec-forge detects existing files and resumes from where it left off.

### Resume Points

| Files Found | Resumes At |
|-------------|------------|
| `claude-research.md` | Interview |
| `+ claude-interview.md` | Spec synthesis |
| `+ claude-spec.md` | Plan generation |
| `+ claude-plan.md` | External review |
| `+ reviews/` | Feedback integration |
| `+ sections/index.md` | Section writing |
| `+ all sections` | Ralph-loop prompt generation |
| `+ claude-ralph-loop-prompt.md` | Done |

## Best Practices

1. **Start with something** - Even a few bullet points. The interview phase extracts details.

2. **Answer thoroughly** - The interview is where hidden requirements surface. Don't rush it.

3. **Review critically** - External LLMs catch blind spots but may over-engineer. You decide what to integrate.

4. **Use sections** - Each section file is self-contained. Work on them in parallel or hand them off.

5. **Iterate** - If the plan isn't right, edit `claude-plan.md` and re-run section generation.

## Implementing the Plan

After spec-forge completes, you have self-contained section files ready for implementation. Choose your approach:

### Option A: Manual Implementation (Recommended)

Best for: learning the codebase, maintaining control, reviewing as you go.

```bash
# 1. Check the dependency order
cat planning/sections/index.md

# 2. Open first section
cat planning/sections/section-01-foundation.md

# 3. Implement following the acceptance criteria

# 4. Move to next section, repeat
```

Each section file contains:
- Background context
- Requirements
- Implementation details
- Acceptance criteria (checklist)
- Files to create/modify

You can implement sections yourself, delegate to another Claude session, or hand off to a team member.

### Option B: Autonomous with ralph-loop (Optional)

Best for: hands-off execution, large plans, overnight runs.

```bash
/ralph-loop @planning/claude-ralph-loop-prompt.md --completion-promise "COMPLETE" --max-iterations 100
```

See [Integration with ralph-loop](#integration-with-ralph-loop-optional) for details.

---

## Integration with ralph-loop (Optional)

spec-forge generates `claude-ralph-loop-prompt.md` for optional integration with [ralph-loop](https://github.com/anthropics/claude-plugins-official/tree/main/plugins/ralph-loop).

### What is ralph-loop?

Ralph Loop is an iterative execution technique that keeps Claude working on a task until completion. It uses a Stop hook to create a self-referential feedback loop - Claude works, checks progress, and continues until the completion criteria are met.

### One-Command Execution

After spec-forge completes, it generates `claude-ralph-loop-prompt.md` with all section content embedded. Execute the entire plan with:

```bash
/ralph-loop @planning/claude-ralph-loop-prompt.md --completion-promise "COMPLETE" --max-iterations 100
```

That's it. Walk away and come back to working code.

### The Workflow

```
┌─────────────────────────────────────────────────────────────────┐
│                    spec-forge + ralph-loop                      │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   1. /spec-forge @planning/feature.md                           │
│      └── Generates sections + claude-ralph-loop-prompt.md       │
│                                                                 │
│   2. (Optional) Review sections/index.md for dependencies       │
│                                                                 │
│   3. /ralph-loop @planning/claude-ralph-loop-prompt.md \        │
│        --completion-promise "COMPLETE" --max-iterations 100     │
│                                                                 │
│   4. Walk away. Come back to working code.                      │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### What the Prompt Does

The generated `claude-ralph-loop-prompt.md` instructs ralph-loop to:

1. Parse the section index for dependencies
2. Execute each section in the correct order
3. Verify acceptance criteria for each section
4. Track progress in `PROGRESS.md`
5. Continue until all sections are done (or hit max iterations)

### Executing Individual Sections

If you prefer to execute sections one at a time:

```bash
# Execute section 01 (usually foundation/setup)
/ralph-loop "Implement the following section. Follow all requirements exactly.

$(cat planning/sections/section-01-foundation.md)

When ALL acceptance criteria are met and tests pass:
- Output <promise>SECTION-01-COMPLETE</promise>

If blocked after 10 iterations, document blockers and output <promise>SECTION-01-BLOCKED</promise>" --completion-promise "SECTION-01" --max-iterations 30
```

### Tips

1. **Set max-iterations** - Always use `--max-iterations` as a safety net (50-100 is reasonable for full execution)
2. **Review PROGRESS.md** - Check progress during long executions
3. **Respect dependencies** - If executing manually, check `sections/index.md` for the dependency graph

### Installing ralph-loop

```bash
# Via Claude Code plugin marketplace
/plugin marketplace add anthropics/claude-plugins-official
/plugin install ralph-loop
/plugin enable ralph-loop
```

## File Structure

```
~/.claude/skills/spec-forge/
├── SKILL.md                    # Main skill definition
├── README.md                   # This file
└── references/
    ├── research-protocol.md    # How research works
    ├── interview-protocol.md   # Interview guidelines
    ├── external-review.md      # CLI review setup
    ├── section-index.md        # Index creation rules
    └── section-splitting.md    # Section file format
```

## Differences from Similar Tools

| Feature | spec-forge |
|---------|------------|
| API Keys Required | No - uses CLI tools |
| TDD Phase | No - focused on planning |
| Python Scripts | No - pure Claude skill |
| External Review | Via Gemini + Codex CLI |
| Resume Support | Yes - automatic |

---

**Author:** Leo
**License:** MIT
