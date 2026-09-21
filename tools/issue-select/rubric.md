Rubric: is this a good first issue?
===================================

<!--THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checksyou define here. It ships empty on purpose: the judgment is your work.A filled rubric must contain:1. At least one row in the checks table. Each row needs all four columns: - Check: a short name (used in the output JSON). - Evidence: exactly what to look at, and where. Name the source (repo-facts block, issue body, comment thread, or the locations in references/evidence-guide.md). "The repo" is not a source; "the last 5 default-branch commit dates" is. - Pass condition: a condition someone else could apply and get your answer. Prefer thresholds with numbers ("a maintainer commented within 30 days") over adjectives ("maintainer is responsive"). - Weight: `required` (a fail here rejects the issue) or `preferred` (never changes the verdict; a nice-to-have that helps rank the issues you accept).2. A verdict rule below the table: how the check grades combine into accept or reject, including how `unclear` is treated. The verdict space is binary. If you write no rule for `unclear`, the skill treats it as fail.Cover what actually kills first contributions. The lecture named fourfamilies: the maintainer is alive, the repo is in use, the scope fits anewcomer, and nobody else is already on it. A rubric that ignores a familywill fail eval issues designed around that family.-->

Checks
------

| Check                        | Evidence                    | Pass condition                                               | Weight    |
| ---------------------------- | --------------------------- | ------------------------------------------------------------ | --------- |
| repo-last-push-to-any-branch | Repo Facts                  | within last 60 days                                          | required  |
| maintainer-alive             | last 5 commits              | 2 in last 90 days                                            | required  |
| is-issue-assigned            | Assigness list of the issue | no assignee                                                  | required  |
| open-linked-pr               | linked PRs                  | no linked PR that are open                                   | required  |
| check-for-pause              | issue comment thread        | no signs of the issue being paused or postposed indefinitely | required  |
| check-for-claimers           | issue comment thread        | no one commenetd their interest on the issue                 | required  |
| responds-to-issues           | reply time in last 5 issues | a reply within 30 days                                       | preferred |
| is-good-first-issue          | issue lables                | has a good first issue label                                 | preferred |

Verdict rule
------------

<!-- State how the grades above combine into accept or reject, and howunclear is treated. Example shape (write your own): "accept if everyrequired check passes; preferred checks never change the verdict, theyrank accepted issues; unclear counts as fail." -->

All weight = required checks must pass for a vertict of Accept,

else, the vertict is Reject.
