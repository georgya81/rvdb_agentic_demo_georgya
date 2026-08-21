---
name: Daily App Update
description: Add a dated daily update entry and accessible dialog to the sample app.
on:
  schedule:
    - cron: "0 0 * * *"
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
engine: copilot
tools:
  edit:
safe-outputs:
  create-pull-request:
    allowed-files:
      - index.html
    max: 1
---

Update `index.html` for the current workflow run.

1. Determine the workflow run's date in UTC, using `date -u` in the workflow environment. Format it as the existing navigation does: an ordinal day followed by the full month name, such as `1st of August`. Use a lowercase month-day slug for IDs, such as `august-1-dialog`.
2. Inspect the existing Daily Updates navigation and dialogs before editing. Add one navigation button to `.daily-updates-list` for today's UTC date and one matching accessible `<dialog>` in the existing structure. The button must use `type="button"`, `aria-haspopup="dialog"`, `aria-controls`, and `data-dialog-trigger`. The dialog must use the matching `id`, `aria-labelledby`, and `aria-describedby` attributes, and its content must follow the existing header, close button, heading, and answer markup.
3. Make the dialog clearly confirm that the daily update ran for the UTC date. Match the existing wording, ID conventions, indentation, and styling. Do not modify `styles.css` or any file other than `index.html`.
4. Before editing, search for the date, its navigation control, and its dialog. If any matching date/update already exists, make no change. Preserve every existing daily update and never duplicate a date, navigation control, or dialog.
5. If no change is needed, emit a `noop` safe output. Otherwise, request exactly one pull request through the configured safe output after editing `index.html`.

Review the resulting HTML for valid nesting and matching IDs before requesting the safe output.
