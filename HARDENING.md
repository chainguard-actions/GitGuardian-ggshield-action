<!-- markdownlint-disable -->

# Hardening Report: GitGuardian--ggshield-action/v1.53.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **GitGuardian--ggshield-action/v1.53.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple action references use mutable tags instead of pinned full-length SHA commit hashes, making the workflow vulnerable to supply-chain attacks if the tag is moved or the image is replaced.

- action.yml: `image: docker://gitguardian/ggshield:v1.53.0` uses a mutable Docker tag instead of a SHA digest (e.g. `docker://gitguardian/ggshield@sha256:<64-hex-char-digest>`).
- .github/workflows/main.yml: `uses: actions/checkout@v2` — tag ref, not a SHA.
- .github/workflows/tag.yml: `uses: actions/checkout@v4` — tag ref, not a SHA.
- .github/workflows/tag.yml: `uses: actions/create-release@v1` — tag ref, not a SHA.

Locations:

- `action.yml:16`
- `.github/workflows/main.yml:11`
- `.github/workflows/tag.yml:9`
- `.github/workflows/tag.yml:12`

### missing-permissions (severity: medium)

Neither workflow file defines a top-level `permissions:` block, and no job within them defines job-level permissions. Without explicit permissions, the GITHUB_TOKEN is granted its default (potentially broad) permissions, violating the principle of least privilege.

- .github/workflows/main.yml: no `permissions:` key at top level or in the `scanning` job.
- .github/workflows/tag.yml: no `permissions:` key at top level or in the `release` job.

Locations:

- `.github/workflows/main.yml:1`
- `.github/workflows/tag.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all findings:
1. action.yml: Pinned `docker://gitguardian/ggshield:v1.53.0` to its SHA digest `sha256:387ad1467f110ce759a97dc4b25c978e7df58181f8e4793df55d40f89ce7142d`, preserving the `docker://` scheme and tag inline.
2. .github/workflows/main.yml: Pinned `actions/checkout@v2` to full SHA `0717577d45739eb3c851188b29f50ed6c0b2194e` with `# v2` comment; added `permissions: {}` at top level.
3. .github/workflows/tag.yml: Pinned `actions/checkout@v4` to `11d5960a326750d5838078e36cf38b85af677262 # v4` and `actions/create-release@v1` to `0cb9c9b65d5d1901c1f53e5e66eaf4afd303e70e # v1`; added `permissions: {}` at top level and `permissions: contents: write` at the release job level (required to create GitHub releases).

