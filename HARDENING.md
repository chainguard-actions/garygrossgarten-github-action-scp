<!-- markdownlint-disable -->

# Hardening Report: garygrossgarten--github-action-scp/v0.8.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **garygrossgarten--github-action-scp/v0.8.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow uses actions/checkout@v2, which is pinned to a mutable tag rather than an immutable 40-character commit SHA. This means the action could be silently updated or replaced, creating a supply-chain risk.

Locations:

- `.github/workflows/scp-example-workflow.yml:12`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and the only job (`build`) also has no job-level `permissions:` key. Without explicit permissions, the GITHUB_TOKEN is granted its default (potentially broad) permissions, violating the principle of least privilege.

Locations:

- `.github/workflows/scp-example-workflow.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed two findings in .github/workflows/scp-example-workflow.yml: (1) Added `permissions: {}` at the top level to enforce least-privilege for the GITHUB_TOKEN — the workflow only runs SCP copy steps using secrets and does not need any GitHub API permissions. (2) Pinned `actions/checkout@v2` to its full commit SHA `0717577d45739eb3c851188b29f50ed6c0b2194e` with a `# v2` comment to prevent supply-chain attacks via mutable tags.

