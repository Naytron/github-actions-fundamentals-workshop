# GitHub Actions Fundamentals — Workshop Repository

Companion hands-on repository for the **GitHub Actions Fundamentals** full-day workshop. Each lecture module ends in a lab you run in **your own copy of this repo**, so every concept — events, syntax, secrets, environments, custom actions, runners, CI/CD — is practiced against a real (but tiny) Node.js application.

Built for **solo learners on `github.com`**: one attendee per repository. Features that require an organization (Actions policies, org secrets, runner groups, starter-workflow templates) are covered as **instructor demos** and marked as such in the labs.

## Before You Start

Complete **[Lab 00 — Attendee Setup](labs/00-attendee-setup.md)** first. It creates your copy of this repository from the template, confirms Actions is enabled, and runs your first (pre-shipped) workflow.

## Lab Sequence (full day)

Work through these in order — each lab assumes the previous one's context.

| # | Lab | Deck module | Time |
|---|-----|-------------|------|
| 0 | [Attendee Setup](labs/00-attendee-setup.md) | — | ~20 min |
| 1 | [Your First Workflow](labs/01-first-workflow.md) | Introduction | ~45 min |
| 2 | [Events & Workflow Syntax](labs/02-events-and-syntax.md) | Workflow syntax | ~60 min |
| 3 | [Secrets & Environments](labs/03-secrets-environments.md) | Environments and secrets | ~45 min |
| 4 | [Sharing & Caching](labs/04-sharing-and-caching.md) | Managing workflows & Actions | ~45 min |
| 5 | [Building Custom Actions](labs/05-custom-actions.md) | Building Actions | ~60 min |
| 6 | [Migration](labs/06-migration.md) | Migration | ~40 min |
| 7 | [Runners](labs/07-runners.md) | Runners | ~45 min |
| 8 | [CI/CD Capstone](labs/08-ci-cd-capstone.md) | CI/CD workflows | ~75 min |

Facilitators: see the **[Facilitator Runsheet](labs/facilitator-runsheet.md)** for the run-of-show, the org-demo pre-flight checklist, and risk mitigations.

## What's in This Repo

```
.github/workflows/   Two pre-shipped workflows: hello-world.yml (setup check)
                     and debug-me.yml (intentionally broken — Lab 1 fixes it)
labs/                Step-by-step lab guides 00–08 + facilitator runsheet
app/                 Sample Node.js service: src/, tests/, Dockerfile
                     (zero runtime dependencies → CI runs are fast and cheap)
actions/             Scaffolds for the three custom action types
                     (composite, JavaScript, Docker) — completed in Lab 5
migration-samples/   Jenkinsfile, azure-pipelines.yml, .gitlab-ci.yml that all
                     build the same app — translated to Actions in Lab 6
solutions/           Completed workflow YAML per lab. Stuck or behind? Copy the
                     solution into .github/workflows/ and keep moving.
org-assets/          Starter-workflow template files facilitators copy into an
                     org's .github repository for the Lab 4 instructor demo
scripts/             Self-hosted runner setup helper for Lab 7
```

## How to Use These Labs

1. Finish [Lab 00](labs/00-attendee-setup.md) — everything else depends on it.
2. Do the labs in order. **You author the workflows yourself**; only `hello-world.yml` and `debug-me.yml` ship in `.github/workflows/`.
3. When a lab says *"Instructor demo"*, watch — those steps need an organization you may not have.
4. If you fall behind, copy the matching file from `solutions/` into `.github/workflows/` — the labs are designed so you can rejoin at any checkpoint.
5. Keep an eye on your [Actions usage](https://github.com/settings/billing) — the labs are sized to stay well inside the free tier, but the capstone matrix is the biggest spender.

## Costs & Guardrails

- All lab workflows use small runners (`ubuntu-latest`), 2-cell matrices, and `concurrency` groups with `cancel-in-progress` so abandoned runs don't burn minutes.
- The sample app has **no npm dependencies** — installs are instant, caching still demonstrable via the lockfile.
- Public repos get free GitHub-hosted runner minutes; private repos consume your plan's quota. Lab 3's environment protection rules require a **public repo or GitHub Pro/Team/Enterprise**.
