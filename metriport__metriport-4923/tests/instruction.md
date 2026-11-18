# Issue

**Title:** ENG-1306 More unit normalization updates

## Description

Part of ENG-1306

### Description

- Covering more edge case units for normalization
- Found them using this logs insights query - [link](https://us-west-1.console.aws.amazon.com/cloudwatch/home?region=us-west-1#logsV2:logs-insights$3FqueryDetail$3D~(end~0~start~-3600~timeType~'RELATIVE~tz~'LOCAL~unit~'seconds~editorString~'fields*20*40timestamp*2c*20*40message*0a*7c*20sort*20*40timestamp*20desc*0a*7c*20filter*20*40message*20like*20*2fDetected*20unmapped*20Observation*20unit*2f*0a*7c*20parse*20*40message*20*27*22unit*22*3a*22*2a*22*27*20as*20sourceUnit*0a*7c*20parse*20*40message*20*27*22normalized*22*3a*22*2a*22*27*20as*20normalizedUnit*0a*7c*20parse*20*40message*20*27*22map*22*3a*5b*2a*5d*5d*27*20as*20map*0a*7c*20limit*2010000~queryId~'78fde09b-d617-4c83-90b6-8c2a3f256584~source~(~'*2faws*2flambda*2fFhirToBundleLambda~'*2faws*2flambda*2fFHIRConverterLambda)~lang~'CWLI))

### Testing
- N/A

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Enhanced unit recognition for critical health measurements. System now supports additional unit synonyms and format variations for glucose levels, kidney function assessments, body mass index calculations, and diabetes monitoring metrics. Improves compatibility with diverse clinical data formats and sources.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2b85d851fe6d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.