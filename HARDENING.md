<!-- markdownlint-disable -->

# Hardening Report: GitGuardian--ggshield-action/v1.52.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **GitGuardian--ggshield-action/v1.52.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The Docker action image reference uses a mutable version tag (`v1.52.0`) instead of an immutable SHA digest. This means the action could silently pull a different (potentially malicious) image if the tag is moved. The reference `docker://gitguardian/ggshield:v1.52.0` should be replaced with a pinned digest such as `docker://gitguardian/ggshield@sha256:<64-hex-char-digest>`.

Locations:

- `action.yml:17`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Replaced the mutable Docker image tag `docker://gitguardian/ggshield:v1.52.0` with the immutable SHA256 digest `docker://gitguardian/ggshield@sha256:c0e22a63b07c8356a3bb8369e632ee169ad6ddecde2151a2aa37b6a49fea9c86` in action.yml line 17. The original tag is preserved as a comment outside the YAML string quotes for readability.

