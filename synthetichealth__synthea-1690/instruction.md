# Issue

**Title:** Correct the cost of psychotherapy and psychological assessment

## Description

SNOMED `228557008` (Cognitive and behavioral therapy) and `405783006` (Psychological assessment) were both priced at $5,132.80/$10,265.59/$20,531.19. Both modules that use `228557008` emit it as a single Procedure of 30 to 60 minutes, so a therapy session was costing between five and twenty thousand dollars.

I mean, I know US Healthcare is expensive, but wow! That's a bit much. The neighbouring row for psychodynamic interpersonal therapy, 304822001, is $69.20/$199.75/$330.29. Far more realistic/reasonable.

The values date to `9408e06` (2018), "update procedure cost min/max with 50% and 200% of mean, just to get something in there", which fanned out an existing point estimate of $10,265.59. That estimate is consistent with a mean inpatient stay charge rather than an outpatient session price.

Reprice both rows against published fee schedules and cite the sources in the COMMENTS column, following the convention of the rest of the file:

  228557008  $78.93 / $139.00 / $335.00   one 30-60 minute session
  405783006 $166.91 / $450.00 / $1,200.00  one evaluation

The sources are a bit extensive. I wanted to provide references for future users and ground the numbers in something real.

`405783006` appears only as a CarePlan activity today and so emits no cost, but it carried the same placeholder and is corrected alongside.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7e08387c68a7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.