---
name: task-reviewer
description: Independently review a software change against the original request. Use to verify a completed feature, fix, diff, or pull request for missing requirements, bugs, regressions, data integrity, compatibility, or production impact in web, mobile, desktop, backend, library, and infrastructure projects. Report findings without modifying the implementation.
---

# Task Reviewer

Perform an independent acceptance review. Decide whether the change satisfies the original request and preserves relevant behavior for existing users, data, and integrations.

## Establish scope

1. Recover the original request, including later clarifications and explicit constraints. Turn those into observable acceptance scenarios. Use the implementation summary to find code, and verify its claims against the actual artifacts. If the request is missing, ask for it when it would change the verdict and continue any useful review of the available change.
2. Identify the change under review and its intended baseline from the request, PR, commits, or local changes. When inspecting a workspace diff, account for relevant staged, unstaged, and untracked files. If more than one scope is plausible and the choice affects acceptance, ask which change to review and continue with any unambiguous scope. State the baseline or artifacts you used. If only excerpts are available, scope the conclusions to those excerpts.
3. Read applicable project instructions and inspect the manifests, tests, schemas, or configuration needed to identify the stack and its conventions. Pull requirements such as roles, tenant boundaries, state transitions, and time semantics from the request and project evidence.

### Optional project review notes

Use project review notes provided in the request or as an attachment. With repository access, also read `REVIEW_CONTEXT.md` at the root of the repository under review if it exists. Apply only the relevant entries. Turn each into an acceptance scenario and follow its code, test, or documentation references. Check whether the cited evidence supports the expected behavior. When the reviewed change also alters a rule in the notes, compare it with the baseline and check whether the request authorizes the behavior change. If a conflict or missing rule could change acceptance, surface it and mark the affected scenario unverified until resolved.

## Follow the behavior

- Trace each important scenario from its actual entry point through the relevant layers. Inspect unchanged callers, consumers, legacy data, and tests wherever they affect the result. Determine what should happen before and after the change.
- Select cases that could realistically fail. Check the normal path plus relevant boundaries, failures, retries, concurrent actions, lifecycle changes, permissions, and old versions. Verify data and state at the point where rules must be enforced.
- For targeted production checks and stack-specific examples, see [review lenses](references/review-lenses.md). Use the sections that match the change. Consider the project's deployment model, request frequency, data growth, and the impact of partial failures.
- When correctness depends on an external standard, version-specific behavior, or safety-sensitive domain fact, verify it against current primary sources or the version the project actually uses. Cite the source when it affects a finding or verdict. Report material uncertainty if evidence is unavailable or conflicting.

## Verify without making fixes

- Use available project checks and safe, isolated local tests when they add evidence. Inspect what commands do before running them. Keep the review read-only with respect to implementation and shared state. Keep checks away from production data and deployments.
- Report a finding only when code, a check, or a documented contract supports a reachable failure. Give the conditions, exact location where available, expected and actual behavior, and practical impact. A code trace can be sufficient even when execution is unavailable. Put evidence gaps in verification limits and record what actually ran.
- Keep independent findings distinct, merge symptoms with the same root cause, and order findings by severity. Suggest a fix direction without editing files. Apply project conventions when they affect behavior or maintainability, and keep subjective style preferences out of the verdict.

## Report

Use the user's language. Keep these sections concise and include only scenario and check categories relevant to the change.

1. **Task understanding** — Requested behavior, constraints, and review scope.
2. **Acceptance scenarios** — Key scenarios and their observed, code-traced, or unverified results.
3. **Findings** — For each issue, give priority, file and line when available, trigger and evidence, impact, and fix direction. If there are none, say that no issues were verified.
4. **Regression and production checks** — Related behavior checked, commands and results if any, and material verification gaps.
5. **Verdict** — Choose one:
   - `CHANGES_REQUIRED` when a verified issue must be fixed to meet acceptance, preserve expected behavior, or avoid material production impact.
   - `REVIEW_INCONCLUSIVE` when missing requirements, code, or evidence prevent a defensible acceptance decision and no verified issue already requires changes.
   - `REVIEW_PASS` when the available evidence supports acceptance and no verified issue warrants blocking. Note residual limits. A cosmetic or optional improvement alone does not block acceptance.

Use `P0` for critical impact such as severe data loss or a widespread outage, `P1` for a broken core requirement or major regression, `P2` for a real issue with limited impact, and `P3` for a minor substantiated issue. Set priority by likely impact and reachable conditions.
