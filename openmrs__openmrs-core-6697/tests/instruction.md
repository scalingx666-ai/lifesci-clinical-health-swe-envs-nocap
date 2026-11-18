# Issue

**Title:** TRUNK-6832: Apply explicitly set DB connection settings to an existing runtime properties file

## Description

> **Depends on #6687** (uses its `escape_property`, and changes the same merge block). Based on that branch so only this commit shows; it will retarget to master once #6687 is merged.

## Description of what I changed

`startup-init.sh` writes the DB connection settings (`OMRS_DB_*`, and the deprecated `OMRS_CONFIG_CONNECTION_*`) only into the installation properties, which OpenMRS reads only on first install. On later starts only `OMRS_EXTRA_*` and `admin.password.locked` reach the existing runtime properties file, so a changed DB password, user or URL in the environment never reaches an existing instance. After a password rotation OpenMRS keeps the old one and fails to connect, with nothing in the log pointing at the cause.

On each start with an existing runtime properties file, `connection.username`, `connection.password`, `connection.url` and `connection.driver_class` are now written into it from the environment:

- Only for settings **set explicitly**. Anything left to the image's defaults keeps the file's value, so instances that don't set these variables are unaffected.
- `connection.url` is rewritten when `OMRS_DB_URL` or any setting it is built from (`OMRS_DB`, `OMRS_DB_HOSTNAME`, `_PORT`, `_NAME`, `_ARGS`, `_EXTRA_ARGS`, `_JDBC_PROTOCOL`, or their `OMRS_CONFIG_*` names) is set. For an instance installed by the image, the rebuilt URL is the one already in the file: the default arguments are the same on 2.7.x through master, and the installer writes the URL unchanged.
- `connection.driver_class` is written whenever `connection.url` is (its protocol depends on `OMRS_DB`), or when `OMRS_DB_DRIVER_CLASS` is set.
- Keys are matched as Java parses them (`key = value`, `key:value`, continuation lines), and only entries for the keys being set are replaced. Other entries in the runtime file, including duplicates added by hand, are left as they are.
- `OMRS_EXTRA_CONNECTION_*` still takes precedence, as it does on first install.
- Values are escaped for the properties format (#6687), and the log names the keys updated, not their values.

**Rationale:** the environment is where these settings are configured, so it should be the source of truth on every start, not only the first. The alternative, documenting `OMRS_EXTRA_CONNECTION_*` for changes after install, already works but means setting the same secret in two variables.

**Behaviour change:** if these variables are set but the runtime file has since been edited by hand (e.g. a different password or URL parameters), the environment now wins on the next start. If anyone relies on the current behaviour, please say so here or on TRUNK-6832.

**Behaviour change (admin password lock):** the existing `admin.password.locked` merge uses the same key matching. Before, a hand-edited `admin.password.locked = false` (spaced, or with `:`) wasn't recognised as the same key, so it beat `OMRS_ADMIN_PASSWORD_LOCKED`. Now the environment wins, as it already did for the exact `admin.password.locked=` spelling. This applies on every start of an existing instance, whether or not any DB variables are set.

## Testing

Ran the whole `startup-init.sh` under `bash -aeu` against a temporary `OMRS_HOME`, with an existing runtime properties file written by `java.util.Properties.store` (as OpenMRS writes it), then read it back with `java.util.Properties`:

| Environment | Result |
|---|---|
| `OMRS_CONFIG_CONNECTION_SERVER/DATABASE/USERNAME/PASSWORD` (password changed, containing `\`) | password updated exactly; username and URL rewritten with the same values; other keys kept |
| nothing DB-related set | file unchanged |
| only `OMRS_DB_PASSWORD` | only `connection.password` updated |
| `OMRS_DB_PASSWORD` and `OMRS_EXTRA_connection_password` | the extra property wins |
| first install (no runtime file) | unchanged behaviour |
| installed as mysql, restarted with `OMRS_DB=mariadb` | URL and driver class both switch to MariaDB |
| only `OMRS_DB_DRIVER_CLASS` | only `connection.driver_class` updated |
| `connection.password = rotated` appended by hand, no DB variables set | `rotated` kept |
| hand-edited `connection.password = old`, `OMRS_DB_PASSWORD=new` | `new` |
| hand-edited `admin.password.locked = false`, `OMRS_ADMIN_PASSWORD_LOCKED=true` | `true` |

I have not built the image.

## Issue I worked on

see https://issues.openmrs.org/browse/TRUNK-6832

## Checklist: I completed these to help reviewers :)

- [x] My IDE is configured to follow the [**code style**](https://wiki.openmrs.org/display/docs/Java+Conventions) of this project. (Shell script only)
- [ ] I have **added tests** to cover my changes. (No test harness exists for `startup-init.sh`; tested manually as above)
- [ ] I ran `./mvnw clean package` right before creating this pull request and added all formatting changes to my commit. (No Java changes)
- [ ] All new and existing **tests passed**.
- [x] My pull request is **based on the latest changes** of the master branch. (Via #6687)

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `33915e6db5c0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.