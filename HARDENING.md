<!-- markdownlint-disable -->

# Hardening Report: EmbarkStudios--cargo-deny-action/v2.1.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **EmbarkStudios--cargo-deny-action/v2.1.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file uses actions/checkout@v4, which is a mutable tag reference rather than a pinned 40-character commit SHA. This means the action could be silently updated to a different (potentially malicious) version without any change to the workflow file, creating a supply-chain risk.

Locations:

- `.github/workflows/test.yml:7`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad (e.g., write access to contents). Explicit minimal permissions should be declared.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both findings in hardened/action/.github/workflows/test.yml: (1) Pinned actions/checkout@v4 to its full commit SHA (34e114876b0b11c390a56381ad16ebd13914f8d5) with the tag preserved as a comment for readability. (2) Added a top-level `permissions: {}` block to explicitly deny all token permissions, since the workflow only builds and runs Docker containers and requires no GitHub token access.

