<!-- markdownlint-disable -->

# Hardening Report: GitGuardian--ggshield-action/v1.50.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **GitGuardian--ggshield-action/v1.50.0** was hardened automatically. 3 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple unpinned action/image references found using mutable tags instead of full 40-character commit SHAs or SHA digests:
- action.yml: `image: "docker://gitguardian/ggshield:v1.50.0"` uses a mutable version tag instead of a SHA digest (e.g. `docker://gitguardian/ggshield@sha256:<digest>`).
- .github/workflows/main.yml: `uses: actions/checkout@v2` uses a mutable tag.
- .github/workflows/tag.yml: `uses: actions/checkout@v4` and `uses: actions/create-release@v1` both use mutable tags.

Locations:

- `action.yml:16`
- `.github/workflows/main.yml:10`
- `.github/workflows/tag.yml:10`
- `.github/workflows/tag.yml:12`

### missing-permissions (severity: medium)

.github/workflows/main.yml has no top-level `permissions:` key and the `scanning` job also has no `permissions:` key. Without explicit permissions, the workflow runs with the default (potentially broad) token permissions.

Locations:

- `.github/workflows/main.yml:1`

### missing-permissions (severity: medium)

.github/workflows/tag.yml has no top-level `permissions:` key and the `release` job also has no `permissions:` key. Without explicit permissions, the workflow runs with the default (potentially broad) token permissions.

Locations:

- `.github/workflows/tag.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all findings:
1. Pinned docker://gitguardian/ggshield:v1.50.0 to sha256:7ee7d0bd69b279ac4b5eec13674f7509075fa5ebfecbe6f43fbfeea6af9eedfe in action.yml (preserving docker:// scheme and tag inline)
2. Pinned actions/checkout@v2 to commit SHA 0717577d45739eb3c851188b29f50ed6c0b2194e in main.yml
3. Pinned actions/checkout@v4 to commit SHA 11d5960a326750d5838078e36cf38b85af677262 in tag.yml
4. Pinned actions/create-release@v1 to commit SHA 0cb9c9b65d5d1901c1f53e5e66eaf4afd303e70e in tag.yml
5. Added top-level `permissions: {}` and job-level `permissions: contents: read` to main.yml
6. Added top-level `permissions: {}` and job-level `permissions: contents: write` to tag.yml (write required for creating GitHub releases)

