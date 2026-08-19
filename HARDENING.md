<!-- markdownlint-disable -->

# Hardening Report: EmbarkStudios--cargo-deny-action/v2.0.15

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **EmbarkStudios--cargo-deny-action/v2.0.15** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow uses `actions/checkout@v4`, which is a mutable tag reference rather than a pinned 40-character commit SHA. This means the action could be silently updated to a different (potentially malicious) version without any change to the workflow file, creating a supply-chain risk.

Locations:

- `.github/workflows/test.yml:7`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key, and the only job (`build`) also has no job-level `permissions:` key. This means the workflow runs with GitHub's default permissions (which include `contents: write` for some events), violating the principle of least privilege. A minimal permissions block (e.g., `permissions: {}` or `contents: read`) should be added.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed two findings in .github/workflows/test.yml: (1) Pinned `actions/checkout@v4` to the full commit SHA `11d5960a326750d5838078e36cf38b85af677262` with `# v4` comment for readability. (2) Added `permissions: {}` at the top level of the workflow to enforce least privilege, since the workflow only builds and runs a Docker image locally and requires no GitHub API permissions.

