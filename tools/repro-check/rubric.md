# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check                  | Evidence                                                               | Pass condition                                                                                                                                                                                            | Weight                       |
| ---------------------- | ---------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------- |
| ai-policy              | check Contribution policy                                              | no objection against use of AI or if requires for disclosure check if the chandidate has provided appropiate disclosure in the thread or report                                                           | required                     |
| bug-repro-match        | check Candidate repro report                                           | the bug reproduced by the cadidate should be exactly same as the bug mentioned in the issue or a solid explanation for why the bug could not be reproduced                                                | required                     |
| bug-repro-step-match   | check Candidate repro report                                           | the candidate's repro report must have the exact steps that are given in the issue details required to reproduce the bug or a solid explanation for why the step could not be performed                   | required                     |
| bug-repro-output-match | check Candidate repro report                                           | the candidate's repro report must have the exact output for each step that are given in the issue details required to reproduce the bug or a solid explanation for why the output could not be generated. | required                     |
| env-check              | check Candidate repro report                                           | the candidate's repro report must contain system and version information of the required software used by the candidate and it should match the version specified in the repo deatils                     | required                     |
| comment-language-check | Candidate claim comment, read against normal OSS community conventions | The comment expresses interest and intent without demanding exclusive assignment, guaranteeing a timeline, or otherwise presuming a claim before a maintainer responds.                                   |  |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

Ready if and only if all 4 above checks are Passed (P)
Hold, if any of the checks is Fail (F) or Unclear/Missing (?)
