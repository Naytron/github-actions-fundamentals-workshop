# Solutions

Completed, working workflow files for each lab. They live **outside** `.github/workflows/` on purpose — nothing here runs until you copy it into `.github/workflows/` in your own repository.

| File | Lab | Copy to |
| --- | --- | --- |
| `01-debug-me-fixed.yml` | 1 | replaces `.github/workflows/debug-me.yml` |
| `02-ci.yml` | 2 | `.github/workflows/ci.yml` |
| `03-deploy-gated.yml` | 3 | `.github/workflows/deploy.yml` (requires `staging`/`production` environments) |
| `04-reusable-build.yml` | 4 | `.github/workflows/reusable-build.yml` |
| `04-caller.yml` | 4 | `.github/workflows/use-reusable.yml` |
| `05-use-custom-actions.yml` | 5 | `.github/workflows/try-actions.yml` |
| `06-migrated-ci.yml` | 6 | `.github/workflows/migrated-ci.yml` |
| `07-self-hosted.yml` | 7 | `.github/workflows/self-hosted.yml` **in your private runner-playground repo** |
| `08-capstone-pipeline.yml` | 8 | `.github/workflows/pipeline.yml` |

Conventions used throughout (and worth stealing for real projects):

- **Actions pinned to full commit SHAs** with the version tag as a comment — tags can be moved, SHAs can't.
- **Least-privilege `permissions:`** at the top level, elevated only where a job needs it.
- **`concurrency` groups** so stale CI runs cancel, but deploys never do.
- **`timeout-minutes`** on every job — nothing should be able to hang for the 6-hour default.
