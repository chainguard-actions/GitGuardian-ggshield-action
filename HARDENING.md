<!-- markdownlint-disable -->

# Hardening Report: GitGuardian--ggshield-action/v1.57.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **GitGuardian--ggshield-action/v1.57.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Docker action runs.image uses a mutable tag instead of a SHA digest: `image: "docker://gitguardian/ggshield:v1.57.0"`. Pin it to an immutable digest, e.g. docker://gitguardian/ggshield@sha256:<digest> # v1.57.0.

Locations:

- `action.yml:17`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned runs.image to docker://gitguardian/ggshield:v1.57.0@sha256:d3d524a9c4b8ec938c75f5a2517b1c53805e141d5b57eeedd42ceb402c3285ff, keeping the docker:// scheme and the tag inline. I left the Docker args unchanged.

