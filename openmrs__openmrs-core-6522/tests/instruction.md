# Issue

**Title:** TRUNK-6793: Add optional OpenTelemetry metrics export

## Description

<!--- Add a pull request title above in this format -->
<!--- real example: 'TRUNK-5111: Replace use of deprecated isVoided' -->
<!--- 'TRUNK-JiraIssueNumber: JiraIssueTitle' -->
## Description of what I changed
<!--- Describe your changes in detail -->
<!--- It can simply be your commit message, which you must have -->
OpenMRS now speaks OpenTelemetry!

openmrs-core can now export OpenTelemetry metrics. bundles the OTel Java agent and attaches it when `OMRS_OTEL_ENABLED`=true.

off by default. nothing changes for anyone who doesn't opt in.

### Why do we need this?

Implementers currently have no standard way to see whether an openmrs server is healthy. everyone builds their own thing, in whatever shape, so nothing's shareable.

OTel is a CNCF standard that basically every observability backend speaks. So instead of us picking a monitoring vendor for people, we emit a standard format and they point it wherever:

_"openmrs exports standard OTel. Grab it however you like."_

**Why core and not the distro:** bahmni, kenyaEMR, ugandaEMR and the rest all build on core. distro-only means each of them reimplements it. also the attach logic has to live in startup.sh anyway, and that's here.

**Why the java agent and not a JMX scraper**: runs in-process, exposes nothing. a scraper needs every deployment to open a JMX/RMI port, which is a rough default for a clinical system.

### What changed

Dockerfile: downloads the agent to /openmrs/otel in the production stage, checksum-verified, same pattern as the tini and tomcat downloads. Pure java so no TARGETARCH handling needed.

startup.sh: appends -javaagent: to CATALINA_OPTS when the flag is set. mirrors the existing OMRS_DEV_DEBUG_PORT block right above it. uses ${VAR-} since the script runs under -u.

that's it. everything past the on/off flag is standard `OTEL_*` variables, so the config surface is the OTel spec rather than something we invented.

Sample config:
```
        OMRS_OTEL_ENABLED: true
        OTEL_EXPORTER_OTLP_ENDPOINT: http://alloy:4317
        OTEL_EXPORTER_OTLP_PROTOCOL: grpc
        OTEL_SERVICE_NAME: openmrs-backend
        OTEL_JMX_TARGET_SYSTEM: tomcat
        OTEL_METRICS_EXPORTER: otlp
        OTEL_TRACES_EXPORTER: none
        OTEL_LOGS_EXPORTER: none
```

### The cost

The jar adds ~24MB to every openmrs-core image whether you use it or not. that's the real tradeoff.

No runtime cost when disabled, the -javaagent flag just never gets added. 

### Tested

Validated end to end on the reference application: agent → gRPC → Alloy → Prometheus → Grafana. 

Distro PR: 

<img width="1624" height="923" alt="image" src="https://github.com/user-attachments/assets/c0a9b2ff-48ce-4f5f-82d5-4b5774804567" />


## Issue I worked on
<!--- This project only accepts pull requests related to open issues -->
<!--- Want a new feature or change? Discuss it in an issue first! -->
<!--- Found a bug? Point us to the issue/or create one so we can reproduce it! -->
<!--- Just add the issue number at the end: -->
see https://openmrs.atlassian.net/browse/TRUNK-6793

## Checklist: I completed these to help reviewers :)
<!--- Put an `x` in the box if you did the task -->
<!--- If you forgot a task please follow the instructions below -->
- [x] My IDE is configured to follow the [**code style**](https://wiki.openmrs.org/display/docs/Java+Conventions) of this project.

  No? Unsure? -> [configure your IDE](https://wiki.openmrs.org/display/docs/How-To+Setup+And+Use+Your+IDE), format the code and add the changes with `git add . && git commit --amend`

- [ ] I have **added tests** to cover my changes. (If you refactored
  existing code that was well tested you do not have to add tests)

  No? -> write tests and add them to this commit `git add . && git commit --amend`

- [ ] I ran `./mvnw clean package` right before creating this pull request and
  added all formatting changes to my commit.

  No? -> execute above command

- [ ] All new and existing **tests passed**.

  No? -> figure out why and add the fix to your commit. It is your responsibility to make sure your code works.

- [x] My pull request is **based on the latest changes** of the master branch.

  No? Unsure? -> execute command `git pull --rebase upstream master`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `71f68a5547c8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.