# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Maintainer active | "last 5 default-branch commits" dates under Repo facts (eval) / commit list on repo front page (live) | At least one commit within 90 days of the capture date (eval) or today (live) | required |
| Repo in use | "latest release" and "last push to any branch" under Repo facts, plus "archived:" flag (eval) / Releases box and front-page commit date (live) | Repo is not archived, AND (latest release within 12 months OR last push within 90 days) | required |
| Scope fits a newcomer | Issue body and comment thread text | FAIL if any of: (a) issue explicitly says its parts should be filed/tracked as separate issues, or anticipates different contributors each taking a different piece — NOT simply one author's checklist of related edits needed to complete a single cohesive task, even if one item is marked lower-priority or optional within that same task, (b) thread shows unresolved design disagreement with no maintainer decision, (c) issue is a pure usage/support question ("how do I..."), (d) a maintainer states the fix requires core/internal changes, (e) the issue has a history of two or more closed/unmerged PR attempts, (f) it is a feature request with zero maintainer engagement (no comments, no maintainer-applied label like good-first-issue/help-wanted/accepted) and no confirmation the maintainers actually want the feature built — this does not apply to documentation or bug-fix issues, only to speculative new-feature proposals. Otherwise PASS — a long or detailed body covering several related edits within one cohesive task is not itself an umbrella issue; judge whether the work is meant to be split across contributors or is unvetted, not the length of the writeup. | required || Not already claimed | "this issue: assignees" and "linked PRs" under Repo facts, plus Comments section (eval) / issue sidebar and thread (live) | No assignee, no open linked PR, and no claim comment ("I'll take this," "working on this") within the last 14 days that a maintainer hasn't contradicted | required |
| AI-contribution policy allows it | "contribution policy" line under Repo facts (eval) / CONTRIBUTING.md, AI_POLICY.md, or PR template (live) | No outright ban on AI-generated contributions (silence or stated conditions both pass) | required |
| Good-first-issue signal | Issue labels | Labeled `good first issue` or `help wanted` | preferred |
| Fast maintainer response | "maintainer first-response sample" under Repo facts (eval) / recent issues sorted by activity (live) | Median first response from an Owner/Member/Collaborator within 30 days | preferred |
| Adoption scale | Star count on the repo line (eval) / repo front page (live) | Repo has more than 100 stars | preferred |

## Verdict rule

Accept if all required checks pass. If any required check fails or is unclear, reject — unclear is treated as fail. Preferred checks never affect the verdict; among accepted issues, rank higher the ones with more preferred checks passing (ties broken by whichever has the more recent maintainer response).
