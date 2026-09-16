---
"on":
  pull_request_target:
    types: [edited]
    branches: [ghaw-merge-upper-control-20260915]

permissions:
  contents: read
  copilot-requests: none

features:
  samples: true

checkout: false

engine:
  id: copilot
  version: "1.0.80"
max-turns: 4
timeout-minutes: 10

tools:
  bash: false
  cli-proxy: false
  github: false

safe-outputs:
  merge-pull-request:
    target: triggering
    allowed-branches: ["ghaw-merge-control-trigger-20260915"]
    max: 1
    github-token: ${{ secrets.GHAW_MERGE_TOKEN }}
    samples:
      - merge_method: squash
---

# Owned triggering-target control

This is an authorized security test using only researcher-owned accounts, branches, and inert canaries.

Call `merge_pull_request` exactly once with `merge_method` set to `squash`. Omit `pull_request_number` so the configured triggering pull request is used. Do not call any other tool or act on any other pull request.
