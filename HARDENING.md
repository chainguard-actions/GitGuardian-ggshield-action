<!-- markdownlint-disable -->

# Hardening Report: GitGuardian--ggshield-action/v1.52.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **GitGuardian--ggshield-action/v1.52.1** was hardened automatically. 3 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

action.yml uses a Docker image pinned to a mutable tag (`docker://gitguardian/ggshield:v1.52.1`) instead of an immutable SHA digest. This means the image can be silently replaced with a different version, enabling supply-chain attacks. It should be pinned to a SHA digest, e.g. `docker://gitguardian/ggshield@sha256:<64-hex-char-digest>`.

Locations:

- `action.yml:17`

### unpinned-uses (severity: high)

Workflow files reference external actions using mutable tags instead of full 40-character commit SHAs. Failing references: main.yml — `actions/checkout@v2`; tag.yml — `actions/checkout@v4` and `actions/create-release@v1`. These should be pinned to their full commit SHA (e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`) to prevent supply-chain attacks.

Locations:

- `.github/workflows/main.yml:12`
- `.github/workflows/tag.yml:10`
- `.github/workflows/tag.yml:13`

### missing-permissions (severity: medium)

Neither .github/workflows/main.yml nor .github/workflows/tag.yml declares a top-level `permissions:` block, and no job within either file declares its own `permissions:` block. Without explicit permissions, the GITHUB_TOKEN is granted its default (broad) permissions, violating the principle of least privilege.

Locations:

- `.github/workflows/main.yml:1`
- `.github/workflows/tag.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all three findings: (1) Pinned Docker image in action.yml from mutable tag `docker://gitguardian/ggshield:v1.52.1` to immutable digest `docker://gitguardian/ggshield:v1.52.1@sha256:021f583af9ff26f69bc9e7cf813ba16bb9e328f08205f6d2139613cdf15cd63e`. (2) Pinned `actions/checkout@v2` to SHA `ee0669bd1cc54295c223e0bb666b733df41de1c5` in main.yml, `actions/checkout@v4` to SHA `34e114876b0b11c390a56381ad16ebd13914f8d5` and `actions/create-release@v1` to SHA `0cb9c9b65d5d1901c1f53e5e66eaf4afd303e70e` in tag.yml. (3) Added `permissions: {}` to main.yml (no special permissions needed) and `permissions: contents: write` to tag.yml (required for the create-release action to publish GitHub releases).

