# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/36

**Verdict output**

```
1. #36 — POST /reviews endpoint has no test for empty-document profile — accept. Top-ranked: it passes two preferred checks (labeled good first issue, 6-day median maintainer response) against #16's one, and is the smallest bounded unit of the two — one new test in one named file, 2–3 hours, zero prior activity on the thread.

2. #16 — Failed tool calls in tool_results never reach review output — accept. Same required passes, but only one preferred check: no good first issue label (bug, agent, tier-2) and a 4–6 hour estimate spanning two files.

Rejected — #43 — Shared test fixture missing from tests/fixtures/ — sank on Not already claimed: the maintainer closed it on 2026-09-16 with "the profile fixture and the sample resumes were added as shared test infrastructure, so it isn't recreated here." The work is already done, and the issue is closed.

One tension worth flagging: the rubric has no check on issue state, and Not already claimed's three literal sub-conditions (no assignee, no open linked PR, no fresh claim comment) all technically hold for #43 — a strictly literal read would have accepted a closed, already-completed issue. I graded it fail on the check's evidence (the Comments section says the work is done), but the durable fix belongs in rubric.md: add an explicit "issue is open and the work still wanted" required check.

{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/36",
  "checks": [
    {"name": "Maintainer active", "grade": "pass", "evidence": "Newest default-branch commit by Aburke225 dated 2026-09-16, 4 days before today"},
    {"name": "Repo in use", "grade": "pass", "evidence": "archived: false, and last push 2026-09-16T21:50:20Z is within 90 days"},
    {"name": "Scope fits a newcomer", "grade": "pass", "evidence": "Body asks for one test in one named file (tests/unit/test_review_routes.py), 2-3 hours; no umbrella split, no design dispute, no core-internals statement, and it is a maintainer-authored test-coverage task, not a speculative feature"},
    {"name": "Not already claimed", "grade": "pass", "evidence": "assignees: none; timeline holds only six 'labeled' events and no cross-referenced PRs; comments count 0"},
    {"name": "AI-contribution policy allows it", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and .github/PULL_REQUEST_TEMPLATE.md contain no mention of AI/LLM/Copilot use — silence passes"},
    {"name": "Good-first-issue signal", "grade": "pass", "evidence": "Labels include 'good first issue' (added by Aburke225 2026-09-10T21:40:08Z)"},
    {"name": "Fast maintainer response", "grade": "pass", "evidence": "Collaborator first responses on #43 and #52 both 6 days after open; median 6 days < 30"},
    {"name": "Adoption scale", "grade": "fail", "evidence": "stargazers_count: 2, not more than 100"}
  ],
  "verdict": "accept"
}
```

**The verdict must record `accept` for this issue.** Confirmed — verdict is `accept`.

---

## Eval iterations

**Run history**

1. Full run, no `--save-run`: `agreement: 15/20 scored items (bar: 18/20: below the bar)` — categories `claimed 4/4 clear-accept 5/8 dead-repo 3/3 policy 1/1 scope 2/4`.
2. `--only issue-01,issue-04,issue-15,issue-19,issue-20` after first Scope rewrite: `agreement: 0/5 scored items`.
3. `--only issue-01,issue-04,issue-15,issue-19,issue-20` after second Scope rewrite (added abandoned-PR-history and umbrella-vs-cohesive-task language): `agreement: 4/5 scored items` (issue-20 still wrong).
4. `--only issue-01,issue-04,issue-15,issue-19,issue-20` after adding the zero-engagement-feature-request trigger: `agreement: 5/5 scored items`.
5. Full run to confirm: `agreement: 20/20 scored items (bar: 18/20: PASS)` — categories `claimed 4/4 clear-accept 8/8 dead-repo 3/3 policy 1/1 scope 4/4`.
6. Final confirming run with `--save-run eval-run.txt`: `agreement: 20/20 scored items (bar: 18/20: PASS)` — this is the run recorded in the committed `eval-run.txt`.

**Issue analysis**

issue-15 (zulip/zulip#19589). My rubric's verdict: `reject`. Gold label: `reject` (agree). The issue looked superficially like a strong first issue — it carries `good first issue` and `help wanted` labels and a clear feature description — but the comment thread shows a multi-year history of contributors claiming it via `@zulipbot claim` and then going silent, plus two closed, unmerged PRs already attempted against it (`#20840`, `#23123`). My rubric's "Scope fits a newcomer" check treats a history of two or more closed/unmerged PR attempts as a fail condition, on the reasoning that repeated abandoned attempts are evidence the work is harder in practice than the label suggests, even though nothing in the issue body itself signals that difficulty.

**Check rationale**

Quoted as currently written in `rubric.md`, "Scope fits a newcomer" row (Evidence column): "Issue body and comment thread text". Pass condition: "FAIL if any of: (a) issue explicitly says its parts should be filed/tracked as separate issues, or anticipates different contributors each taking a different piece — NOT simply one author's checklist of related edits needed to complete a single cohesive task, even if one item is marked lower-priority or optional within that same task, (b) thread shows unresolved design disagreement with no maintainer decision, (c) issue is a pure usage/support question ('how do I...'), (d) a maintainer states the fix requires core/internal changes, (e) the issue has a history of two or more closed/unmerged PR attempts, (f) it is a feature request with zero maintainer engagement (no comments, no maintainer-applied label like good-first-issue/help-wanted/accepted) and no confirmation the maintainers actually want the feature built — this does not apply to documentation or bug-fix issues, only to speculative new-feature proposals. Otherwise PASS." I wrote it this way because my first version failed on both ends: it rejected long, detailed-but-cohesive issues (false rejects on issue-01, issue-04, issue-19) and accepted an unvetted feature request with zero maintainer engagement and an issue with two abandoned PR attempts (false accepts on issue-15, issue-20). Naming explicit fail triggers, instead of a single vague "is it bounded" condition, fixed both directions at once.

**Trade-offs**

The explicit list of fail triggers in "Scope fits a newcomer" is a closed list — the trade-off is that any real scope problem not on the list (a, b, c, d, e, f) will pass through as unclear-but-passing rather than being caught. I re-ran the five disputed issues with `--only issue-01,issue-04,issue-15,issue-19,issue-20` three times while tuning this check, and confirmed with the final full run that no other issue's grade moved when I tightened trigger (a) to require explicit split-across-contributors language — issue-02, issue-05, issue-08, and the other previously-passing issues kept identical grades across runs, which tells me the tightened wording narrowed the trigger without weakening it elsewhere.

---

## Selection rationale

**Selection rationale**

1. This issue (#36) fits my available time well — it's scoped at 2-3 hours, adding a single test to a single named file, which is realistic for a first contribution without a large time commitment. It's also a good starting point for me to get familiar with the repo's testing conventions before taking on anything larger.
2. The verdict correctly identified that the issue is small, unclaimed, and explicitly labeled by a maintainer as a good first issue, with a fast historical response time (6-day median). What I weighed that the rubric doesn't capture: the issue has zero prior comments, meaning I'll be the first person a maintainer responds to on it — there's no existing thread to learn from about how detailed my PR description should be, so I'll need to look at other merged PRs in the repo for tone and format.
3. I expect claiming it to be straightforward — no assignee, no linked PRs, and a maintainer response history under a week. The main risk is that the repo has very few stars (2) and only one active maintainer identified in the run (Aburke225), so if that person is unavailable, review could stall; but nothing in the evidence suggests contention over the issue itself.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.