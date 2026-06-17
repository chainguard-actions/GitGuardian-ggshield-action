<!-- markdownlint-disable -->

# Hardening Report: GitGuardian--ggshield-action/v1.52.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **GitGuardian--ggshield-action/v1.52.1** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action uses a Docker image referenced by a mutable version tag rather than an immutable SHA digest. `image: "docker://gitguardian/ggshield:v1.52.1"` should be replaced with a SHA-pinned reference such as `image: "docker://gitguardian/ggshield@sha256:<64-hex-char-digest>"`. A mutable tag means the image content can change without notice, enabling supply-chain attacks.

Locations:

- `action.yml:17`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Replaced the mutable Docker image tag `docker://gitguardian/ggshield:v1.52.1` with the immutable SHA-pinned reference `docker://gitguardian/ggshield@sha256:021f583af9ff26f69bc9e7cf813ba16bb9e328f08205f6d2139613cdf15cd63e` in action.yml line 17. The original tag is preserved as a comment for readability.

