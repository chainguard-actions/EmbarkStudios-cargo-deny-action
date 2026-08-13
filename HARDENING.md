<!-- markdownlint-disable -->

# Hardening Report: EmbarkStudios--cargo-deny-action/v2.0.20

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **EmbarkStudios--cargo-deny-action/v2.0.20** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow uses `actions/checkout@v4`, which is pinned to a mutable tag rather than an immutable 40-character commit SHA. A tag can be moved to point to a different (potentially malicious) commit, enabling supply-chain attacks. It should be replaced with the full SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`.

Locations:

- `.github/workflows/test.yml:8`

### missing-permissions (severity: medium)

The workflow file `.github/workflows/test.yml` has no top-level `permissions:` block and the only job (`build`) also has no job-level `permissions:` block. Without explicit permissions, the workflow inherits the repository's default token permissions (which may be `write-all` for older repositories), granting broader access than necessary. A minimal `permissions:` block (e.g. `contents: read`) should be added.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed hardened/action/.github/workflows/test.yml: (1) Pinned actions/checkout@v4 to its full commit SHA (34e114876b0b11c390a56381ad16ebd13914f8d5) with a # v4 comment for readability. (2) Added a top-level `permissions: contents: read` block to enforce least-privilege access — the workflow only needs to check out code, so read access to contents is sufficient.

