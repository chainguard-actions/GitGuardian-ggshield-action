<!-- markdownlint-disable -->

# Hardening Report: GitGuardian--ggshield-action/v1.49.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **GitGuardian--ggshield-action/v1.49.0** was hardened automatically. 5 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Workflow file uses tag-based (mutable) refs instead of pinned full-length SHA commit hashes. Failing references: `actions/checkout@v2` (line 11). These can be silently updated to point to malicious code.

Locations:

- `.github/workflows/main.yml:11`

### unpinned-uses (severity: high)

Workflow file uses tag-based (mutable) refs instead of pinned full-length SHA commit hashes. Failing references: `actions/checkout@v4` (line 8) and `actions/create-release@v1` (line 11). These can be silently updated to point to malicious code.

Locations:

- `.github/workflows/tag.yml:8`
- `.github/workflows/tag.yml:11`

### unpinned-uses (severity: high)

The action.yml Docker image reference uses a mutable version tag (`docker://gitguardian/ggshield:v1.49.0`) instead of an immutable SHA digest (e.g. `docker://gitguardian/ggshield@sha256:<64-hex-char-digest>`). A tag can be re-pointed to a different image without notice, enabling supply-chain attacks.

Locations:

- `action.yml:15`

### missing-permissions (severity: medium)

Workflow file has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the GITHUB_TOKEN is granted its default (often broad) permissions. Add a top-level `permissions: {}` block and grant only the minimum required scopes.

Locations:

- `.github/workflows/main.yml:1`

### missing-permissions (severity: medium)

Workflow file has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the GITHUB_TOKEN is granted its default (often broad) permissions. Add a top-level `permissions: {}` block and grant only the minimum required scopes (e.g. `contents: write` for creating releases).

Locations:

- `.github/workflows/tag.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 5 findings across 3 files:
1. main.yml: Pinned actions/checkout@v2 → @ee0669bd1cc54295c223e0bb666b733df41de1c5 # v2; added top-level `permissions: {}`.
2. tag.yml: Pinned actions/checkout@v4 → @34e114876b0b11c390a56381ad16ebd13914f8d5 # v4; pinned actions/create-release@v1 → @0cb9c9b65d5d1901c1f53e5e66eaf4afd303e70e # v1; added top-level `permissions: contents: write` (minimum required for creating releases).
3. action.yml: Pinned docker://gitguardian/ggshield:v1.49.0 → docker://gitguardian/ggshield:v1.49.0@sha256:74a990937b163323c4ffaf3b7f76a856be4617fbae4231563d1db990193f59c4, preserving the docker:// scheme and version tag inline.

