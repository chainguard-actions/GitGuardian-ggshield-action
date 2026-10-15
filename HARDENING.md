<!-- markdownlint-disable -->

# Hardening Report: GitGuardian--ggshield-action/v1.56.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **GitGuardian--ggshield-action/v1.56.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The Docker action references the image `docker://gitguardian/ggshield:v1.56.0` using a mutable version tag (`v1.56.0`) rather than an immutable SHA digest. If the tag is moved to a different image layer (e.g., by a supply-chain compromise or accidental overwrite), the action will silently execute different code. The image reference should be pinned to a full SHA256 digest, e.g. `image: docker://gitguardian/ggshield@sha256:<64-hex-char-digest> # v1.56.0`.

Locations:

- `action.yml:16`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the Docker image reference in action.yml from `docker://gitguardian/ggshield:v1.56.0` to `docker://gitguardian/ggshield:v1.56.0@sha256:0b016c9530c3df9700ef5703322195c3d53fc1653505a811a59218f1f811bc4a`. The `docker://` scheme and version tag are preserved inline alongside the immutable digest.

