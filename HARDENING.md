<!-- markdownlint-disable -->

# Hardening Report: GitGuardian--ggshield-action/v1.50.3

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **GitGuardian--ggshield-action/v1.50.3** was hardened automatically. 3 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple action/image references use mutable tags instead of pinned SHA digests, making the action vulnerable to supply-chain attacks:

- action.yml: `image: "docker://gitguardian/ggshield:v1.50.3"` — Docker image uses a version tag, not a SHA digest (e.g., `docker://gitguardian/ggshield@sha256:<digest>`).
- .github/workflows/main.yml: `uses: actions/checkout@v2` — tag reference, not a 40-char commit SHA.
- .github/workflows/tag.yml: `uses: actions/checkout@v4` — tag reference, not a 40-char commit SHA.
- .github/workflows/tag.yml: `uses: actions/create-release@v1` — tag reference, not a 40-char commit SHA.

Locations:

- `action.yml:15`
- `.github/workflows/main.yml:10`
- `.github/workflows/tag.yml:11`
- `.github/workflows/tag.yml:14`

### missing-permissions (severity: medium)

.github/workflows/main.yml has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the workflow inherits the default (potentially broad) repository permissions.

Locations:

- `.github/workflows/main.yml:1`

### missing-permissions (severity: medium)

.github/workflows/tag.yml has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the workflow inherits the default (potentially broad) repository permissions. The `release` job uses `GITHUB_TOKEN` to create releases, so at minimum `contents: write` should be explicitly declared.

Locations:

- `.github/workflows/tag.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all findings across 3 files:

1. action.yml: Pinned `docker://gitguardian/ggshield:v1.50.3` to `docker://gitguardian/ggshield:v1.50.3@sha256:b3d2fd20d5d9e555adf83da755e88e960b1fcd6c49766daa77119d53a8378958` (preserving docker:// scheme and version tag inline).

2. .github/workflows/main.yml: Pinned `actions/checkout@v2` to `actions/checkout@ee0669bd1cc54295c223e0bb666b733df41de1c5 # v2`. Added `permissions: {}` top-level block since the workflow requires no GitHub API permissions.

3. .github/workflows/tag.yml: Pinned `actions/checkout@v4` to `actions/checkout@34e114876b0b11c390a56381ad16ebd13914f8d5 # v4` and `actions/create-release@v1` to `actions/create-release@0cb9c9b65d5d1901c1f53e5e66eaf4afd303e70e # v1`. Added `permissions: contents: write` top-level block since the release job creates GitHub releases via GITHUB_TOKEN.

