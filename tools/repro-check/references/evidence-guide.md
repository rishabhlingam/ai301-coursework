# Evidence guide: where proof lives in a reproduction package

<!--THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this filefinished; the scaffolding fades). The skill uses this guide as its map:for every kind of proof a rubric check names, this file says WHERE tofind it in a package and WHAT GOOD LOOKS LIKE when you do.Under each family heading below, write:- Where it lives: the exact places to look. In an eval bundle (which  section of the package: the issue context, the repo-facts block, the  claim comment, the repro report and its parts). In live mode (where  on GitHub or in the draft: the issue thread, the repo's docs, the  student's draft comment).- What good looks like: one or two sentences someone else could apply.  Prefer observable conditions ("the versions named match what the  issue targets, or the difference is called out") over adjectives  ("environment is thorough").A rubric check whose evidence this guide cannot locate is a checknobody else can execute; the rubric swap showed you what that feelslike. Write the map you wish your grader had.-->

Every rubric check needs an evidence source. This guide maps the following criterion to concrete places you can look: on github.com when you are reviewing a reproduction package for a repo issue by hand, and in the snapshot bundle when you are in eval mode. It closes with one repo-level surface the criterion do not cover: the contribution policy. If a signal is not listed here, name your own source in the rubric; just make it somewherea grader can actually look.

| Criterion | On github.com | In the eval bundle |
| --- | --- | --- |
| did candidate reproduce the bug correctly | on the comment thread of the issue | "Candidate repro report" |
| did candidate show correct steps of bug reproduction | on the comment thread of the issue | "Candidate repro report" |
| did candidate show correct step outputs for bug reproduction | on the comment thread of the issue | "Candidate repro report" |
| did candidate mention environment and version information | on the comment thread of the issue | "Candidate repro report" |
| did candidate adhere to OSS community conventions in comments | on the comment thread of the issue | "Candidate claim comments" |

## The fifth surface: are you allowed to contribute the way you work?

An issue can pass all four families and still be a dead end, becausethe repo's rules reject your workflow before a maintainer reads a lineof your code. Some projects ban AI-generated contributions outright;many more set conditions (disclose AI use, personally understand andtest every change, human-review AI output). In this course yourcontribution workflow is AI-assisted, so this surface applies to you.

| Signal | On github.com | In the eval bundle |
| --- | --- | --- |
| Contribution policy | `CONTRIBUTING.md` in the repo root or `.github/`, and any contributor docs it links out to; the policy often hides one click away from the repo | the "contribution policy" line under Repo facts |
| Dedicated AI policy files | files like `AI_POLICY.md` or `AI_USAGE_POLICY.md`; an `AGENTS.md` file is the opposite signal, instructions written for AI coding agents | quoted or summarized on the same line |
| Templates | PR and issue templates sometimes require an AI-use disclosure checkbox | the same line |

How to grade what you find:

* **An outright ban** ("we do not accept AI-generated code") is a fail:submitting AI-assisted work against a stated ban wastes themaintainer's time and yours, however good the issue looks.
* **Conditions are not bans.** Disclosure, personal understanding,testing, and human-review requirements are terms to follow, notreasons to walk away. Most policies you will meet are this kind.
* **Silence passes.** Most repos state nothing; that is not arestriction.

## Reading the repo-facts block honestly

The bundle's repo-facts block is captured on a stated date. Every recencythreshold in your rubric ("within 90 days") is measured against thatcapture date, not against today. Live mode measures against today.

<!-- Where the words meet the repo: the claim comment against theissue, the comments against the repo's stated templates andcontribution policy (including AI-use disclosure requirements), andwhat specific-and-honest looks like next to boilerplate. -->
