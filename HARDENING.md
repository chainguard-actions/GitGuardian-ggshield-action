<!-- markdownlint-disable -->

# Hardening Report: GitGuardian--ggshield-action/v1.50.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **GitGuardian--ggshield-action/v1.50.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action uses a Docker image pinned by mutable version tag rather than an immutable SHA digest. `image: "docker://gitguardian/ggshield:v1.50.0"` uses the tag `v1.50.0`, which can be silently overwritten by the image registry, enabling supply-chain attacks. It should be replaced with a SHA-digest reference such as `image: "docker://gitguardian/ggshield@sha256:<64-hex-char-digest>"`

Locations:

- `action.yml:16`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Replaced the mutable Docker image tag reference `docker://gitguardian/ggshield:v1.50.0` with the immutable SHA digest reference `docker://gitguardian/ggshield@sha256:7ee7d0bd69b279ac4b5eec13674f7509075fa5ebfecbe6f43fbfeea6af9eedfe` in action.yml line 16. The original tag is preserved as a comment outside the YAML quotes for readability.

