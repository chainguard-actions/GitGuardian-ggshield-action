<!-- markdownlint-disable -->

# Hardening Report: GitGuardian--ggshield-action/v1.55.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **GitGuardian--ggshield-action/v1.55.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The Docker action image reference uses a mutable version tag instead of an immutable SHA digest. `image: "docker://gitguardian/ggshield:v1.55.0"` can be silently replaced if the tag is moved, enabling a supply-chain attack. It should be pinned to a full SHA256 digest, e.g. `image: "docker://gitguardian/ggshield@sha256:<64-hex-char-digest> # v1.55.0"`.

Locations:

- `action.yml:17`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the Docker image reference in action.yml from `docker://gitguardian/ggshield:v1.55.0` to `docker://gitguardian/ggshield:v1.55.0@sha256:e2be72a60b51f9c06cf2527e00ed526721ec3b22339634fd8bb7c0f44fe8fb74`. The docker:// scheme and version tag are preserved inline, with the immutable SHA256 digest appended to prevent supply-chain attacks via mutable tag reassignment.

