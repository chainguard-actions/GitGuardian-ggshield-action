<!-- markdownlint-disable -->

# Hardening Report: GitGuardian--ggshield-action/v1.51.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **GitGuardian--ggshield-action/v1.51.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The Docker action references the image `docker://gitguardian/ggshield:v1.51.0` using a mutable version tag (`v1.51.0`) instead of an immutable SHA digest (e.g. `docker://gitguardian/ggshield@sha256:<64-hex-char-digest>`). A mutable tag can be silently redirected to a different image, enabling a supply-chain attack. The image reference should be pinned to a full SHA256 digest.

Locations:

- `action.yml:17`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the Docker image reference in action.yml from the mutable tag `gitguardian/ggshield:v1.51.0` to the immutable digest `gitguardian/ggshield@sha256:feeb08c2be66515cc1a1b4a54c9d27777f6b21993aaef30d3af4a064902725fe`, with the original tag preserved as a comment.

