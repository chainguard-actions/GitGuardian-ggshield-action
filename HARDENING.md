<!-- markdownlint-disable -->

# Hardening Report: GitGuardian--ggshield-action/v1.51.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **GitGuardian--ggshield-action/v1.51.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple `uses:` references in workflow files use mutable tags instead of pinned full-length SHA commit hashes, making the action vulnerable to supply-chain attacks if those tags are moved. Failing references: `actions/checkout@v2` (main.yml), `actions/checkout@v4` (tag.yml), `actions/create-release@v1` (tag.yml). Additionally, action.yml uses a Docker image with a mutable version tag (`docker://gitguardian/ggshield:v1.51.0`) instead of a SHA digest (e.g. `gitguardian/ggshield@sha256:<digest>`).

Locations:

- `.github/workflows/main.yml:11`
- `.github/workflows/tag.yml:9`
- `.github/workflows/tag.yml:12`
- `action.yml:16`

### missing-permissions (severity: medium)

Neither `.github/workflows/main.yml` nor `.github/workflows/tag.yml` declares a top-level `permissions:` block, and no job in either file has a job-level `permissions:` block. Without explicit permissions, workflows run with the default (potentially broad) token permissions, violating the principle of least privilege.

Locations:

- `.github/workflows/main.yml:1`
- `.github/workflows/tag.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all findings across 3 files:

1. `.github/workflows/main.yml`: Pinned `actions/checkout@v2` → `actions/checkout@0717577d45739eb3c851188b29f50ed6c0b2194e # v2`. Added top-level `permissions: {}`.

2. `.github/workflows/tag.yml`: Pinned `actions/checkout@v4` → `actions/checkout@11d5960a326750d5838078e36cf38b85af677262 # v4` and `actions/create-release@v1` → `actions/create-release@0cb9c9b65d5d1901c1f53e5e66eaf4afd303e70e # v1`. Added top-level `permissions: {}` and job-level `permissions: contents: write` (minimum required for creating releases).

3. `action.yml`: Pinned Docker image `docker://gitguardian/ggshield:v1.51.0` → `docker://gitguardian/ggshield:v1.51.0@sha256:feeb08c2be66515cc1a1b4a54c9d27777f6b21993aaef30d3af4a064902725fe`, preserving the `docker://` scheme and version tag inline.

