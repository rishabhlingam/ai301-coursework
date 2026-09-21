# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

* * *

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/64

**Verdict output**

    Ranked read-out — all three accepted:
    
    1. #73 — README vs .env.example disagree on the LLM key. Docs-only, two files named in the body, no test setup to get running; the smallest possible first PR. Also the newest issue (opened 2026-09-16, same day as the latest commits).
    2. #64 — Relevance-scorer test fixture has full overlap. One test fixture, with an exact repro command (pytest tests/unit/test_relevance_scorer.py -q) and the failing assertion quoted.
    3. #72 — verify_password raising UnknownHashError. Still bounded (two files), but it's behavior change in core/security.py plus removing an xfail marker — the most moving parts of the three.
    
    Two caveats on that ordering: the fit profile in scope.md is still the placeholder (Write a few sentences here.), so I ranked on work size rather than your background — fill that in and the order may change. And the ordering is a tiebreak only: all three score identically on your preferred checks (good-first-issue label present; responds-to-issues fails for all of them — of the last 5 issues only #69 has any comments, and both are from jacho15 with author_association: NONE, so there is no maintainer reply to time). Per your rule, that preferred fail changes no verdict.
    
    One rubric gap worth noting: you have no check for the contribution/AI policy surface. It happens not to bite here — the repo has no CONTRIBUTING.md, AI_POLICY.md, or AGENTS.md, only a PR template — but an eval issue built around a stated AI ban would sail through this rubric.
    
    [
      {
        "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/64",
        "checks": [
          {"name": "repo-last-push-to-any-branch", "grade": "pass", "evidence": "pushedAt 2026-09-16T21:48:27Z — 4 days before capture date 2026-09-20"},
          {"name": "maintainer-alive", "grade": "pass", "evidence": "Last 5 commits by Andrew Burke: 3 on 2026-09-16, 2 on 2026-08-24 — all within 90 days"},
          {"name": "is-issue-assigned", "grade": "pass", "evidence": "\"assignees\": [] on issue #64"},
          {"name": "open-linked-pr", "grade": "pass", "evidence": "No connected/cross-referenced PR events on the timeline; repo has zero PRs in any state"},
          {"name": "check-for-pause", "grade": "pass", "evidence": "Comment thread is empty (0 comments); no pause or postponement language anywhere"},
          {"name": "check-for-claimers", "grade": "pass", "evidence": "0 comments on the issue, so no expressions of interest"},
          {"name": "responds-to-issues", "grade": "fail", "evidence": "Of the last 5 issues only #69 has comments, both from jacho15 with author_association NONE — no maintainer reply to measure"},
          {"name": "is-good-first-issue", "grade": "pass", "evidence": "Labels include \"good first issue\" (added 2026-09-10T21:38:12Z)"}
        ],
        "verdict": "accept"
      }
    ]

* * *

## Eval iterations

**Run history**

One run occurred. The first attempt at a full run did not complete: a Windows-specific `UnicodeEncodeError` (the `claude` subprocess's stdin defaulted to `cp1252`, which cannot encode emoji/unicode characters present in several bundles) crashed the writer thread for multiple items, so several issues returned `ERROR (claude exited 1: ...)` instead of a verdict. This was fixed by setting `PYTHONUTF8=1` before invoking the harness, which forces UTF-8 mode regardless of the console's codepage. The rubric itself was not changed between the failed attempt and the successful run, only the environment was fixed. The completed run scored **18/20 scored items (bar: 18/20: PASS)**, matching the agreement line in the committed `eval-run.txt`.

**Issue analysis**

`issue-09` — my rubric graded **reject**; gold's verdict was **accept**. My rubric failed it on `check-for-pause` and `check-for-claimers`: the comment thread shows a 2022 comment ("I'd like to take a swing at this") with a maintainer reply ("go for it"), followed by a stale bot auto-comment in 2023 and nothing since. My checks read that old comment as an active claim and treated the thread as showing engagement, so both checks failed and the required-check rule rejected the issue. Gold treats a four-year-old, unfollowed-up claim as effectively abandoned rather than as someone currently working on it. My rubric doesn't yet distinguish a recent claim from a stale one.

**Check rationale**

> `check-for-claimers` — Evidence: issue comment thread. Pass condition: no one commented their interest on the issue. Weight: required.

I wrote this check because "nobody else is already on it" was one of the four families named in lecture, and a comment expressing interest is the most direct, checkable signal that another contributor is already positioned to claim the issue This avoids me duplicating someone else's work or stepping on a claim in progress.

**Trade-offs**

This check has no time bound, it fails on *any* comment expressing interest, regardless of how old it is or whether it was followed up. That caused problem with `issue-09`. A single stale, unfollowed 2022 comment was enough to fail the check and reject an otherwise good issue. The trade-off is that this check is safe against active competition but blind to claims that were abandoned long ago. It will keep producing false rejects like `issue-09` until it's revised to only count comments within some recency window.

* * *

## Selection rationale

**Selection rationale**

1. I have experience in Python and in text chunking, and #64 is a bug in a relevance-scorer test fixture close enough to that background that I expect to be productive quickly rather than spending most of my time just orienting in unfamiliar code. It's also the smaller of my two realistic options in scope (one test fixture, one exact repro command), which fits the time I have for a first issue.
  
2. The verdict correctly identified that #64 is bounded (one fixture file), unclaimed, and has an exact repro command and failing assertion already quoted in the issue so I know precisely how to reproduce the bug before I start. What the rubric couldn't weigh is my own comfort with the domain: text-chunking/relevance-scoring logic is closer to what I've worked with than, say, #72's password-hashing behavior change, so I'm likely to spot the actual cause faster than the rubric's evidence alone would suggest.
  
3. I expect claiming it to be low-risk: the repo has zero PRs in any state and no maintainer response history to judge typical reply speed from,but the issue is unclaimed and unassigned with no comments at all, so there's no visible competition. The main uncertainty is simply how quickly a maintainer responds once I comment, since there's no prior data to estimate that from.
  

* * *

Related paths: `eval-run.txt` in this directory; your skill's files in `tools/issue-select/`.
