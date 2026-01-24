# Demo of Git Branching Strategy


## Why “stage → main” causes blocking

When you merge feature branches into stage for QA, stage becomes a bundle of features:

Feature A might pass QA, Feature B might fail.

If promotion is “merge stage into main”, then A can’t ship without B unless you start doing revert gymnastics or cherry-picks.

Over time, stage drifts from main, and the merge itself can introduce conflicts or unexpected changes.

## Potential solution

- Make stage disposable and don't “merge stage → main” as promotion.

- QA happens from feature branches deployed to staging.

- Promotion to production is always a PR -> main.

- stage gets reset to main frequently.


## If we adopt disposable staging, it’s worth documenting something like:

❌ Never merge stage → main

✅ Always reset stage from main

✅ Promote via PRs into main

Options to help support this flow include:

- a GitHub Actions job to auto-reset stage after a prod deploy (If that is deemed to be disirable)

- branch protection setup that prevents accidental stage → main merges