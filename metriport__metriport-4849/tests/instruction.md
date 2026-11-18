# Issue

**Title:** filter out roster upload secrets from api stack

## Description

Part of ENG-000

_[Release PRs:]_


### Dependencies
Downstream: 

### Description
Filter out roster upload secrets from api stack.
Change from using arn to name for secrets

### Testing
- Local
  - [x] Quick [test of the filter function using typescript playground](https://www.typescriptlang.org/play/?target=6#code/C4TwDgpgBAyhDGAnCwDOUC8UBKCD2iAJgDyrCICWAdgOYA0UZltAfANwBQHokUAEhQgBhPFQBmFGpigBvKFQCGAWwgAuRuWpSAvpx7QAamCoAbCKlQDhoiVKxzFK9Uy1RdXfVACiVAG4jxSWkZDigoAAsTAHYAOTxgCgl4BQTRAH51ELCw8MEA21QMnHwiUk1aBit8oIAfKCNTc0s8m0l2ULdOdw4xAFcqeFSqKGQlPF8IAFUqXtQIQjgkFFQAMQIAQTAKOERfCngIAAo5pbR1ReQ0BnhWmnUff1uASnOES-QsqBuqMkY35YA6hRgOE8L1gNg8GQIIhJmATHgFIRpKNxhBIdDYfDEQt-mhjnjUNdnpwwpdeohhid3kCQWCIVDgDC4QikV0uH0BkMRhAxhMMUysazcadUATRa9RcTAndvH5qjQXrBCbIOt9fpFYvFEvsUhRRNJvrYAHSauIJJJ60SkqCJKCHACEZu1lqGTx5wApVMJnDVog1LRl6CwzotuqGpsDBRtdsduWsQfd5Mpf1FvrC6uAEUEAAUFBYAO4EEWXGLKcyGvAmMyDKx5wvFi4oMsqMXxhWoJ7pj1eqAAeQARgArBDAY1iRB4JQ+TTmQ4dMKDkeDY0QKizsXU5ZPccUEyCw6HADaAGsICAALrujAsKAOpej41nkBt3P51BFohN4At8w76jwCYvSEHOz5PE8HRdhw2gcv0gz6sMNzVqOdbvp+JbNuWYodPGqDqLgNylC4FT8FGtT1MYZgWFUtwsBwSoEcWZTMPQGgsbenyZlA9L4SUJDEaxAm3vY7hhGIBD2lx7a3NxYj9sOj6+AoQFzrh4GqtkXz+lmW4-uW0g0CgVgwGIwBgPWH6Nniv6HNJMrGo4EBQZpsa6b+7r0kebnlhe0jeSoNowWSKC9vS7I9HB3KGcAxmmeZaFWacNnxr+zjlIqaUsRpPYpgABgKzLYkiJlmRZ6EALQACQyCl5baLl4XcOA0AACrmMAKzDFghzXrevh4BQhCcGYWZgO+8zSAADAwYgKHuE1YJNvqcvBBpMmQhyOZlWgzVQ6htWQnXup85AgNlYlUD1NoZv6VYQMaCI0IcuWAKDkUDVY59XOdkY0WPMADU-2BV8KTwOE9pOedWk-Hdq6IJOiDPYAMuTvTIn25d9N0w2YcMI4cTnXVAs3zYQgOBdBsFcghUDjYgwAACIQBAYBeAAjr0ynEC1LCHAogwcyY+0MBAAAekCDPMQtQEoqA0EUAnHX6PxZgo0gAFIwH2MTGgJiQgLz-PKQwD4rs+Yp856yk0+gChUCAO6oAQwA9d9XEDurmva7rYj66L4tMoQxsKab55in7o4TfmNN2w7TsuzGcm83eGBYAOiuaSCk4FvIEDZ148MEIeMtSGkaRQAARNMEDs8p5fuv9UC5QAOlQXhixHhDqNVA7aC36yG4L2TVQoX3kzBHAAPQT1A5Wz3P89QAdaAz-Pq-cO1hzl3EETROaOrJNy5W3rp6BweEtuGYQ5cMD1mAcUrvwn5K7zBAuFcwFOEB9iCMLfuX6jlxFtfDooloa-HgGIWUDwFTBF0FAKe8g8A7y1GGA+CEH5ZnpCiXkaJpizHmN+VYGwtg7D2AccU7xriQO+rTBmTMWY1xMIcekDAT5QW0FBdeG0t5ILsgUGex8VRnwvvMa+9perZS4k-ZUopX6aXLjmRkfA8A0E2BQAA0uef+FcwDhGAWEUBXEIFQPlDJewyC96ugQpkbQnQoAYO4uCbBfIpgzDmBhNAaxEBqNIfsI4J8qGKhtLQxmzM2YC2YeCVhhJ2GcPWs7cuuAXHoEnJiKAvQirIhPkTCSRpJAUgmnwAAkl4VAYjb43kkdpVM7xn7LDkdkRJjJCrChKvFBsRByoACFlADjwHgbR5cwAFh6UoPpAy6Bv0rlQZAJgUgELxIMs8zN9GdAccY+4piZQNJyLvF04ZrFQxyGRGgeEjnZFGeMzI8hywAMuf08ubhJmaQMc87I2g3mGOqVgrAqIJh4PcYQrxPiYRkP8YSQJrtqnhwlp3GRL97BTOmLM+ZHiln0NWaAkJ9DwnKUicAYW7dYWxN9PEzeABZXo+4KDwmgMU0pAieTJJptWKAP8KCIBGM0zlGThQ1OWOUiRnFqnSMITsiuBUhQ4jaWVYs3TekPIAcMrpqywhNMxCyaVcVZWdPWAicIiBBnDPWKqiV3LNXFW1QlTpKwTDxiNQWFYpry7f3CDCdFKzPk2iMZAzZjxtmIs0qGfeVo9rnL4ZIM5nwXlQHuXga5W0K5xseR8t+mk9V4ANQm25FcM0GpTW8mNtr4zZqcBXYtggC1pqeW-VNBjvXfKcb8nB-y3ELNFMCkhoK-EUOWJChtysoAwoDnU5e5jXUwgAcssAKbgl-TpqEhhESWFDqJQHElHgN7lyQjWGKb4OkeN-OgAcvQ9yEHQD-LS8NRzSwUDOm+QqHFKDvZWZCtZ92WS-NZLChxo2xoVfG2QNyy3l2TTW9N+rEClrULmyDVaDFQsHcOhaUN1WCgtQsK1B75VjMVWajVmSZXWsIDh8ZzrJUYaI9hvNhqAEUcI1hz9JGaOYrnXMBdOLGGHGfWAQl-t5gbsntPVeq9YC9CUM+xAZ0RPzw4OqWGj1notyXugCQVAKCoDdciI+UALKS1Rr9dxHyoArDmmYOF1VibmdHhwWMVmJq3kmu6TOeBs5UFzt4AuiMXXue4pysYyA2XtVU2Z0RUEgA)
- Staging
  - [x] Deploy bamboo finally :)
  - [x] Run bamboo lambda
  - [x] Run a different roster upload lambda
- Production
  - [ ] Deploy Bamboo :)


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

- **New Features**
  - Roster-upload SFTP password can now be specified by name via a new config/env var; scheduled lambdas receive the new variable.

- **Bug Fixes**
  - API service now excludes unused HIE password secrets from deployed secrets, reducing unnecessary secret attachments.

- **Chores**
  - Shared utility for collecting HIE password secret names made public for reuse.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `55b1c146bcf7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.