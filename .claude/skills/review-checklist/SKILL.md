---
name: review-checklist
description: Runs my standard four-point review on a product brief before it goes any further. Use when I ask to review a brief, run the review checklist, or check a brief before it goes to someone. Checks for a named owner, a success measure, scope that matches from start to end, and a problem explained before the fix. Review only; it never edits the brief.
---

# Review checklist

Run the same four checks on any brief, every time. The user points you at a brief (a file path, a wiki page or pasted text). If they haven't said which, ask which brief, then start.

Read the whole brief first. Then run the four checks in order. For each, give a result and the evidence for it.

## The four checks

1. **Names who owns it.** Pass only if a specific person or role is named as accountable for the brief or the work. "The team", "engineering" or a blank "Owner" field doesn't pass. If the brief names an author but no owner, mark it Partial and say so.

2. **Says how we'll know it worked.** Pass only if it names something we can observe (a metric, a behavior or a threshold) and where the number would come from. A baseline or target is a bonus; if it's missing, say so. "Improve the experience" or "users are happier" doesn't pass. If the measure needs data we don't have, mark it Partial and name the gap.

3. **The scope at the end matches the scope at the start.** Compare what the brief promises at the top (goal, who it's for, what's in) with what it commits to at the end (the plan, the "doesn't do" list, open items, anything added later). Flag anything that appears at the end and wasn't in the start, anything promised at the start that vanishes, and a "doesn't do" list that contradicts the plan.

4. **Explains the problem before it proposes a fix.** Pass only if the problem is stated, with evidence, before any solution language appears. If the fix shows up first, or the problem is only implied, it fails. Note whether the evidence is observed or inferred.

## Rules

- Quote or point to the exact line behind every result. No result without evidence.
- Never invent an owner, a metric or a scope. If it isn't in the brief, it's a gap. Say what's missing and who could fill it, but don't fill it in.
- Don't edit the brief. This is a review, not a rewrite.
- Don't judge whether the idea is good. Only run the four checks.
- Keep it short and plain.

## Output

Use this shape every time:

```
Brief: <title or path>

1. Owner:                 ✓ / ~ / ✗  <one line of evidence>
2. How we'll know:        ✓ / ~ / ✗  <one line of evidence>
3. Scope start vs. end:   ✓ / ~ / ✗  <one line of evidence>
4. Problem before fix:    ✓ / ~ / ✗  <one line of evidence>

Verdict: ready to go further / fix these first
Gaps: <numbered list, most important first, each with who could close it>
```

Use ✓ for pass, ~ for partial and ✗ for fail. If all four pass, the verdict is "ready to go further" and the gaps line says "none".
