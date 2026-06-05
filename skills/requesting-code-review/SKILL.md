---
name: requesting-code-review
description: Use when completing tasks, implementing major features, or before merging to verify work meets requirements
---

# Requesting Code Review

Perform a code review to catch issues before they cascade. Use the review checklist to evaluate the work product against requirements and code quality standards.

**Core principle:** Review early, review often.

## When to Request Review

**Mandatory:**
- After completing major feature
- Before merge to main

**Optional but valuable:**
- When stuck (fresh perspective)
- Before refactoring (baseline check)
- After fixing complex bug

## How to Request

**1. Get git SHAs:**
```bash
BASE_SHA=$(git rev-parse HEAD~1)  # or origin/main
HEAD_SHA=$(git rev-parse HEAD)
```

**2. Review using the checklist at `code-reviewer.md`:**

Review the diff between BASE_SHA and HEAD_SHA against the plan or requirements. Use the checklist to evaluate plan alignment, code quality, architecture, testing, and production readiness.

**3. Act on feedback:**
- Fix Critical issues immediately
- Fix Important issues before proceeding
- Note Minor issues for later
- Push back if feedback is wrong (with reasoning)

## Example

```
[Just completed Task 2: Add verification function]

Let me request code review before proceeding.

BASE_SHA=$(git log --oneline | grep "Task 1" | head -1 | awk '{print $1}')
HEAD_SHA=$(git rev-parse HEAD)

[Review diff against Task 2 from plan/deployment-plan.md]
  DESCRIPTION: Added verifyIndex() and repairIndex() with 4 issue types

[Review findings]:
  Strengths: Clean architecture, real tests
  Issues:
    Important: Missing progress indicators
    Minor: Magic number (100) for reporting interval
  Assessment: Ready to proceed

[Fix progress indicators]
[Continue to Task 3]
```

## Integration with Workflows

**Executing Plans:**
- Review after each task or at natural checkpoints
- Get feedback, apply, continue

**Ad-Hoc Development:**
- Review before merge
- Review when stuck

## Red Flags

**Never:**
- Skip review because "it's simple"
- Ignore Critical issues
- Proceed with unfixed Important issues
- Argue with valid technical feedback

**If reviewer wrong:**
- Push back with technical reasoning
- Show code/tests that prove it works
- Request clarification

See checklist at: requesting-code-review/code-reviewer.md
