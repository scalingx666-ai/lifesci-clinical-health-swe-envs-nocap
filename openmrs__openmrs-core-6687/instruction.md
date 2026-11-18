# Issue

**Title:** TRUNK-6829: Fix case, duplicates, backslashes and escaping in properties written by startup-init.sh

## Description

## Description of what I changed

Four fixes to how `startup-init.sh` writes runtime and server properties, one commit per ticket. They change the same few lines, so they are reviewed and backported together.

- **TRUNK-6829:** `OMRS_EXTRA_*` names containing any lower case letter keep their case (e.g. `OMRS_EXTRA_mail_smtp_socketFactory_class` → `mail.smtp.socketFactory.class`). All upper case names are lowercased as before. Also replaces the unquoted `tr [:upper:] [:lower:]`, whose arguments were subject to pathname expansion: with a one-character file such as `u` or `e` in the working directory, no extra properties were written.
- **TRUNK-6830:** when several `OMRS_EXTRA_*` variables give the same property, the first in sorted order is used and the others are logged and ignored. Previously the last won on first install and the first on later starts.
- **TRUNK-6831:** extra properties are written with `printf` instead of `echo -e`, so backslash sequences in values are no longer interpreted (differently on each path).
- **TRUNK-6835:** values written to the server and runtime properties files are escaped for the Java properties format (`\`, line breaks, leading whitespace). A backslash in `OMRS_DB_PASSWORD`, for example, now reaches OpenMRS unchanged.

**Behaviour changes:**
- A mixed-case name that relied on being lowercased now keeps its case, e.g. `OMRS_EXTRA_Initializer_DOMAINS` used to set `initializer.domains` and now sets `Initializer.DOMAINS`. Such names need to be written all upper case, or in the property's exact case.
- Anyone who escaped backslashes in these variables by hand to work around the old handling will now get doubled backslashes.

**Not covered:** non-ASCII values. The install script is read with `Properties.load(InputStream)` (ISO-8859-1) and runtime properties as UTF-8.

## Testing

No automated tests cover `startup-init.sh`. I ran the properties section of the script under `bash -aeu` for both a first install and an existing runtime properties file, and loaded the output with `java.util.Properties` as OpenMRS does:

- On `master`, each of the four problems reproduces.
- On this branch, a value containing `\t`, `\\`, `=`, `:`, `#`, leading spaces, CR and LF, and a DB password containing `\`, read back exactly as set on both paths. Mixed-case and duplicate names behave as described above.

I have not built the image or started a container with it. The four commits cherry-pick cleanly onto 2.9.x and 2.8.x.

## Issue I worked on

see https://issues.openmrs.org/browse/TRUNK-6829, https://issues.openmrs.org/browse/TRUNK-6830, https://issues.openmrs.org/browse/TRUNK-6831, https://issues.openmrs.org/browse/TRUNK-6835

## Checklist: I completed these to help reviewers :)

- [x] My IDE is configured to follow the [**code style**](https://wiki.openmrs.org/display/docs/Java+Conventions) of this project. (Shell script only)
- [ ] I have **added tests** to cover my changes. (No test harness exists for `startup-init.sh`; tested manually as above)
- [ ] I ran `./mvnw clean package` right before creating this pull request and added all formatting changes to my commit. (No Java changes)
- [ ] All new and existing **tests passed**.
- [x] My pull request is **based on the latest changes** of the master branch.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d455beb296f8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.