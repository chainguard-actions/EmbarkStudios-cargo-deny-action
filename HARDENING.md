<!-- markdownlint-disable -->

# Hardening Report: EmbarkStudios--cargo-deny-action/v2.1.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **EmbarkStudios--cargo-deny-action/v2.1.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow uses `actions/checkout@v4`, which is a mutable tag reference rather than a pinned 40-character commit SHA. If the tag is moved (e.g. by a supply-chain compromise), the action will silently execute different code. Pin to a full SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`.

Locations:

- `.github/workflows/test.yml:8`

### missing-permissions (severity: medium)

The workflow file `.github/workflows/test.yml` has no top-level `permissions:` key and the only job (`build`) also has no job-level `permissions:` key. Without explicit permissions the job inherits the default repository token permissions, which may be broader than necessary. Add a top-level `permissions: {}` block (or minimal specific scopes such as `contents: read`) to follow the principle of least privilege.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both findings in .github/workflows/test.yml: (1) Pinned `actions/checkout@v4` to full SHA `actions/checkout@34e114876b0b11c390a56381ad16ebd13914f8d5 # v4` to prevent supply-chain attacks via mutable tag references. (2) Added `permissions: {}` at the top level to restrict the GITHUB_TOKEN to no permissions by default, following the principle of least privilege.

