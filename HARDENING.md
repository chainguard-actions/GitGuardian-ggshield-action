<!-- markdownlint-disable -->

# Hardening Report: GitGuardian--ggshield-action/v1.52.2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **GitGuardian--ggshield-action/v1.52.2** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The Docker action's `runs.image:` field references a mutable version tag (`docker://gitguardian/ggshield:v1.52.2`) instead of an immutable SHA digest. This means the image content can change without any change to the action definition, creating a supply-chain risk. It should be pinned to a specific SHA digest, e.g. `image: docker://gitguardian/ggshield@sha256:<64-hex-char-digest> # v1.52.2`.

Locations:

- `action.yml:17`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Replaced the mutable Docker image tag `docker://gitguardian/ggshield:v1.52.2` with the immutable SHA256 digest `docker://gitguardian/ggshield@sha256:11057725f4a47b587735351b69b1873435bf393050f946916ef05b1b0c4b1cf4` in action.yml line 17. The version tag `v1.52.2` is preserved as a comment outside the YAML quotes for readability.

