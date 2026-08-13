<!-- markdownlint-disable -->

# Hardening Report: GitGuardian--ggshield-action/v1.52.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **GitGuardian--ggshield-action/v1.52.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple action references and the Docker image use mutable tags instead of pinned SHA digests, making the action vulnerable to supply-chain attacks:
- .github/workflows/main.yml: `uses: actions/checkout@v2` (tag, not SHA)
- .github/workflows/tag.yml: `uses: actions/checkout@v4` (tag, not SHA)
- .github/workflows/tag.yml: `uses: actions/create-release@v1` (tag, not SHA)
- action.yml: `image: "docker://gitguardian/ggshield:v1.52.0"` (mutable tag, not a SHA digest like `@sha256:<64-hex-chars>`)

Locations:

- `.github/workflows/main.yml:12`
- `.github/workflows/tag.yml:11`
- `.github/workflows/tag.yml:14`
- `action.yml:16`

### permissions (severity: medium)

missing-permissions: Neither workflow file defines a top-level `permissions:` key, and no job within them defines job-level permissions. Without explicit permissions, the GITHUB_TOKEN is granted its default (potentially broad) permissions. Each workflow should declare minimal required permissions (e.g. `permissions: contents: read`).

Locations:

- `.github/workflows/main.yml:1`
- `.github/workflows/tag.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, permissions

**Notes:**

Fixed all four unpinned references: pinned actions/checkout@v2 to SHA 0717577d in main.yml; pinned actions/checkout@v4 to SHA 11d5960a and actions/create-release@v1 to SHA 0cb9c9b6 in tag.yml; pinned the Docker image gitguardian/ggshield:v1.52.0 to its sha256 digest in action.yml (preserving the docker:// scheme and tag). Added top-level permissions blocks to both workflow files: contents: read for main.yml and contents: write for tag.yml (required to create GitHub releases).

