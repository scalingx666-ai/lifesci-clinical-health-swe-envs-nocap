# Issue

**Title:** docs: backup and restore, with the nightly script

## Description

. Also covers the documentation half of #16 (the code half of that
issue is void — see the comment there).

There was no backup documentation at all: `pg_dump` appears nowhere in the
repository, and for a project whose premise is that a person keeps their own
health record, "health data is irreplaceable" was a claim with no procedure
behind it.

### The issues' own commands were stale, in ways that fail quietly

- **`mirobody_charts` does not exist.** The `ChartService` MCP tools that
  rendered PNGs through a Node toolchain were removed; DeepAgent writes a
  ```vis-chart``` block the frontend renders, so nothing writes chart files.
- **Volume names are project-prefixed.** `mirobody_upload` is really
  `<project>_mirobody_upload`, so `docker run -v mirobody_upload:/data:ro … tar`
  **creates a new empty volume and archives nothing, exit code 0.** The script
  runs `docker volume inspect` before reading anything.
- **The database service is `pg`**, so the container is `mirobody-pg-1`, not
  `mirobody-db-1`. Commands use `docker compose exec pg`.
- **`./deploy.sh --mode=build`** — deploy.sh takes no arguments and already does
  `compose down`, `up -d --remove-orphans`, then tails logs.
- **Tarring a running cluster's data directory** copies files that move under
  the tar. `pg_dump` is consistent by construction.

### The part neither issue had: the four volumes are not equally precious

| Volume | Back up? | Why |
| --- | --- | --- |
| `mirobody_postgres` | **yes, `pg_dump`** | everything, plus LangGraph `checkpoint_*` conversation memory; all in the `theta_ai` schema with `vector(1024)` + hnsw |
| `mirobody_upload` | **yes, if it exists** | `storage/factory.py` prefers OSS/S3 and falls back to local — a cloud deployment's real target is the bucket |
| `mirobody_redis` | **no, by default** | worker task queues (`LPUSH`/`BLPOP`, no TTL) and locks; in-flight work, so a stale AOF re-runs or drops it. `INCLUDE_REDIS=1` for forensics |
| `mirobody_site_packages` | **never** | pip cache keyed on a hash of pyproject+requirements; restoring it reinstates dependencies the code no longer imports — the 245 MB SDK dropped in this same release would come straight back |

### Verified by running it, both directions

- `shell/backup.sh` against the live stack: dumps `holistic_db`, verifies the
  archive, skips the absent upload volume **with a message** rather than writing
  45 empty bytes, prunes by pattern.
- The dump restored into a scratch database: **29 tables in `theta_ai`, `vector`
  extension present** — so no re-embedding after a restore (that is only for
  changing the embedding provider/model). Scratch database dropped afterwards.
- The uploads tar round-tripped through two scratch volumes with content intact.

Running it is what produced the script's shape: `pg_dump > file` on the host
cannot be verified, because a custom-format archive is not seekable through a
pipe — `pg_restore --list` reported *"did not find magic string in file header"*
for a file whose header was fine. So it dumps and verifies **inside** the
container, then copies out.

Backup is scripted; restore is documented and stays a human decision — a script
that runs `psql` against a live database is a footgun, and the one time you need
it you want to be reading the steps.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `443a9f0c58cc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.