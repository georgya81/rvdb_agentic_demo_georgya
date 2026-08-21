---
name: Weekly Report Status
description: Publish a concise weekly activity report for the repository.
on:
  schedule:
    - cron: "0 9 * * 1"
  workflow_dispatch:
permissions:
  contents: read
  issues: read
  pull-requests: read
  copilot-requests: write
engine: copilot
safe-outputs:
  create-issue:
    title-prefix: "[weekly-report] "
    max: 1
---

Create a concise activity report for the previous seven days and publish it as a new issue.

1. Use the workflow run's UTC time as the report end time. Cover the previous seven complete days relative to that UTC time.
2. Review repository activity from that window, including:
   - commits
   - issues opened, closed, or updated
   - pull requests opened, merged, closed, or updated
3. Summarize the activity clearly and briefly. Group the report by commits, issues, and pull requests. Include useful counts and short highlights when activity exists.
4. If no relevant activity occurred in the previous seven days, state that clearly in the issue body.
5. Publish exactly one issue using the configured `create-issue` safe output. Use a title that starts with `[weekly-report] ` and includes the report window.
6. Do not modify repository files.
