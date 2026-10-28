<!-- markdownlint-disable -->

# Hardening Report: GitGuardian--ggshield-action/v1.56.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **GitGuardian--ggshield-action/v1.56.1** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The Docker action's runs.image points to a mutable tag instead of a SHA digest: `image: "docker://gitguardian/ggshield:v1.56.1"`. Pin it to a digest instead, e.g. `docker://gitguardian/ggshield@sha256:<digest> # v1.56.1`.

Locations:

- `action.yml:17`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned runs.image to docker://gitguardian/ggshield:v1.56.1@sha256:16be3720bb9ef6fc7b4768d6b8c546cf836c8e9fa19a1012556bbaf8af5c4983. The Docker args are unchanged.

