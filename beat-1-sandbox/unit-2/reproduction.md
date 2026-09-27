# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

---

## Your identity upstream

**GitHub username**

rishabhlingam

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/64#issuecomment-5860507863

Hi! I'd like to work on this as a contribution. I can confirm the issue: `test_query_with_partial_overlap` uses the query "Python Django web framework" against a chunk that contains all four query terms, so the scorer's 1.0 return is correct behavior and the test's `assert score < 0.9` is what's wrong, not the scorer. I'll reproduce this locally and put together a repro report, then look at rewriting the fixture so the chunk only partially overlaps the query terms.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/64#issuecomment-5860512624

## Candidate repro report

Environment: Python 3.12.3, pytest 9.1.1, structlog 26.1.0, Ubuntu 24.04.4 LTS (x86_64)

Steps:

```
$ pytest tests/unit/test_relevance_scorer.py -q
```

Output:

```
..x................                                                      [100%]
18 passed, 1 xfailed in 0.06s
```

The target test is already marked `xfail(strict=True)` for this issue, so the default run reports it as an expected failure rather than a raw error. To capture the underlying assertion, re-ran the single test bypassing the marker:

```
$ pytest tests/unit/test_relevance_scorer.py::TestRelevanceScorer::test_query_with_partial_overlap -v --runxfail
```

Output:

```
tests/unit/test_relevance_scorer.py::TestRelevanceScorer::test_query_with_partial_overlap FAILED

    query = "Python Django web framework"
    chunks = [{"text": "Django is a Python web framework for rapid development"}]
    score = scorer.score(query, chunks)
>   assert 0.3 < score < 0.9  # Partial overlap should be in middle range
E   assert 1.0 < 0.9

Captured stdout call:
2026-09-27 22:13:30 [info] relevance_scored  avg_score=1.0 chunks_count=1 query_len=4

1 failed in 0.06s
```

Expected: per the test's own comment, a "partial overlap" fixture should score strictly between 0.3 and 0.9.

Actual: all four query tokens (python, django, web, framework) appear in the chunk, giving full keyword coverage. RelevanceScorer.score() correctly returns 1.0 for full coverage; the fixture's assert 0.3 < score < 0.9 fails because the chunk isn't a partial-overlap case at all, confirming the issue's diagnosis that the fixture, not the scorer, is wrong.



**Verdict output**

```
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/64",
  "checks": [
    {"name": "ai-policy", "grade": "pass", "evidence": "No AI policy surface in repo: docs/CONTRIBUTING.md has no AI section, 0 code-search hits for AI_POLICY or AGENTS.md, PR template has no disclosure checkbox — silence passes."},
    {"name": "bug-repro-match", "grade": "pass", "evidence": "Issue says 'observed: assert 1.0 < 0.9 fails'; report shows 'E assert 1.0 < 0.9' in the same test_query_with_partial_overlap with avg_score=1.0."},
    {"name": "bug-repro-step-match", "grade": "pass", "evidence": "Report runs the issue's literal step '$ pytest tests/unit/test_relevance_scorer.py -q' before adding the --runxfail variant."},
    {"name": "bug-repro-output-match", "grade": "pass", "evidence": "Bare -q run yielded '18 passed, 1 xfailed' not the issue's output; report attributes this to xfail(strict=True), which the source file confirms, then surfaces 'assert 1.0 < 0.9' via --runxfail."},
    {"name": "env-check", "grade": "pass", "evidence": "Python 3.12.3 / pytest 9.1.1 / structlog 26.1.0 / Ubuntu 24.04.4 all satisfy pyproject.toml's requires-python >=3.11, pytest>=7.4.0, structlog>=24.1.0."},
    {"name": "comment-language-check", "grade": "pass", "evidence": "Claim reads 'I'd like to work on this as a contribution' — no demand for exclusive assignment, no timeline guarantee, no presumed claim."}
  ],
  "verdict": "accept"
}
```



## Eval iterations

**Run history**

1. Run 1 (rubric.md sha256 `b2c17fac37ee5b8c`, 2026-09-27T21:50:53Z): 15/20 agreement. Below the 18/20 bar. Failed the disclosure category floor (0/1). pkg-16, pkg-19, pkg-20 wrongly graded accept.
2. Run 2 (rubric.md sha256 `a61c6a60401a21da`, 2026-09-27T21:55:46Z): 18/20 agreement. Meets the bar (PASS). Final committed run, matches `eval-run.txt`.

**Package analysis**

Package: pkg-16 (pandas-dev/pandas#66656). Gold label: reject.

Run 1 verdict: accept (wrong). Run 2 verdict: reject (correct).

Why it read wrong: the issue requires confirming the bug on the latest release or main branch, which the reporter and a commenter both did. The candidate instead used pandas 1.5.3, about two major versions behind, with no explanation. My original `env-check` only asked whether version info was present, not whether it matched what the repo required. A full but stale environment block was enough to pass.

Why it reads right now: I added a clause requiring the reported version to match the version specified in the repo details. Under that reading, pandas 1.5.3 against a repo requiring latest/main fails the check, and the package correctly holds.

**Check rationale**

Quoted from `rubric.md`, `env-check` row, as it reads now:

> "the candidate's repro report must contain system and version information of the required software used by the candidate and it should match the version specified in the repo deatils"

Why: the original check tested only presence of version info, which a stale-but-honest environment can satisfy. Run 1 showed that failure on pkg-16. I rejected keeping it presence-only and added the match-against-repo-requirements clause so the check tests whether the environment is actually valid, not just documented.

**Trade-offs**

pkg-01 and pkg-05 are still misgraded (gold: accept, verdict: reject) in both runs. The `env-check` fix didn't touch them. Both fail `bug-repro-step-match` / `bug-repro-output-match`, which require the issue's exact steps and output or a solid explanation for any deviation. Candidates who substitute an equivalent but non-literal step (e.g. pkg-01 using `--offline` instead of `-v`, and skipping one of two comparison runs without justification) get read as unexplained deviations and fail. Fixing the disclosure-category misses left this strictness untouched, so it still costs two false rejects on otherwise valid repros.
