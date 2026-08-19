<!-- markdownlint-disable -->

# Hardening Report: garygrossgarten--github-action-scp/0.10.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **garygrossgarten--github-action-scp/0.10.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow uses `actions/checkout@v6`, which is pinned to a mutable tag rather than an immutable 40-character commit SHA. This means the action could be silently updated or replaced with malicious code without any change to the workflow file. It should be pinned to a full SHA, e.g. `actions/checkout@<40-char-sha> # v6`.

Locations:

- `.github/workflows/scp-example-workflow.yml:14`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key, and the `build` job also has no `permissions:` key. Without explicit permissions, the workflow inherits the default repository permissions (which may include broad write access). A minimal `permissions:` block (e.g. `contents: read`) should be added at the top level or per-job.

Locations:

- `.github/workflows/scp-example-workflow.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

1. Pinned `actions/checkout@v6` to its full commit SHA `d23441a48e516b6c34aea4fa41551a30e30af803` with a `# v6` comment for readability. 2. Added a top-level `permissions: contents: read` block to restrict the workflow to the minimum required permissions, preventing unintended write access from default repository settings.

