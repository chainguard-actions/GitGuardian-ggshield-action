<!-- markdownlint-disable -->

# Hardening Report: GitGuardian--ggshield-action/v1.50.3

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **GitGuardian--ggshield-action/v1.50.3** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The Docker action references a mutable image tag instead of an immutable SHA digest. `image: "docker://gitguardian/ggshield:v1.50.3"` uses the tag `v1.50.3`, which can be silently overwritten by the image registry, enabling a supply-chain attack. It should be pinned to a specific SHA256 digest, e.g. `image: "docker://gitguardian/ggshield@sha256:<64-hex-char-digest> # v1.50.3"`.

Locations:

- `action.yml:16`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Replaced the mutable Docker image tag `docker://gitguardian/ggshield:v1.50.3` with the immutable SHA256 digest `docker://gitguardian/ggshield@sha256:b3d2fd20d5d9e555adf83da755e88e960b1fcd6c49766daa77119d53a8378958` in action.yml line 16. The original tag is preserved as a comment for readability.

