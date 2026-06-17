<!-- markdownlint-disable -->

# Hardening Report: GitGuardian--ggshield-action/v1.49.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **GitGuardian--ggshield-action/v1.49.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action uses a Docker image referenced by a mutable tag (`v1.49.0`) instead of an immutable SHA digest. If the tag is moved or the image is replaced, the action will silently execute different code. The `image: "docker://gitguardian/ggshield:v1.49.0"` should be replaced with a pinned SHA digest, e.g. `image: "docker://gitguardian/ggshield@sha256:<64-hex-char-digest>"`.

Locations:

- `action.yml:16`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Replaced the mutable Docker image tag `gitguardian/ggshield:v1.49.0` with the immutable SHA256 digest `gitguardian/ggshield@sha256:74a990937b163323c4ffaf3b7f76a856be4617fbae4231563d1db990193f59c4` in action.yml line 16. The original tag is preserved as a comment for readability.

