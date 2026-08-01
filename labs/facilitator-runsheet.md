# Facilitator Runsheet — GitHub Actions Fundamentals

Full-day delivery guide. Attendee-facing content lives in `labs/00`–`08`; this file is for the person at the front of the room.

## Format

- **Audience:** engineers new to Actions; comfortable with git + YAML basics
- **Duration:** ~7 hours content + breaks (full day). Half-day option: Labs 0–4 only.
- **Cadence per module:** slides (10–20 min) → live demo → lab (attendees hands-on) → regroup + Q&A
- **Ratio:** 1 facilitator per ~12 attendees; >20, bring a co-facilitator for lab support

## Run of show

| Time | Block | Slides/deck module | Lab | Demo checkpoint |
| --- | --- | --- | --- | --- |
| 08:30 | Doors + setup help | — | Lab 00 | — |
| 09:00 | Welcome, agenda, "why Actions" | Intro module | — | — |
| 09:20 | Core concepts: events→workflows→jobs→steps→runners | Intro + syntax (1st half) | — | — |
| 09:45 | **Demo 1:** hello-world run, logs, context dump, break debug-me live | after slide ~24 | Lab 01 | ✅ |
| 10:30 | ☕ Break | | | |
| 10:45 | Advanced syntax: events, matrix, needs/if, expressions, limits | Syntax (2nd half) | Lab 02 | |
| 12:00 | 🥪 Lunch | | | |
| 12:45 | Environments & secrets, GITHUB_TOKEN | Env & secrets module | Lab 03 | ✅ demo 2 (slide ~32) |
| 13:45 | Reusable workflows, org policies, starter templates, caching | Managing workflows | Lab 04 | ✅ demo 3 (slide ~41) — needs demo org |
| 14:45 | ☕ Break | | | |
| 15:00 | Building actions: composite/JS/Docker | Building Actions | Lab 05 | ✅ demo 4 (slide ~47) |
| 16:00 | Migration patterns + Importer (talk-heavy, good post-lab-fatigue slot) | Migration | Lab 06 (or take-home) | |
| 16:30 | Runners: hosted fleet, self-hosted live registration, ARC | Runners | Lab 07 | ✅ demo 5 (slide ~56) |
| 17:15 | CI/CD capstone kickoff — attendees continue solo/take-home | CI/CD module | Lab 08 | ✅ demo 6 (slide ~61) |
| 17:45 | Wrap-up, resources, certification pointers, feedback form | — | — | — |

**Half-day variant:** end after Lab 04; assign 05–08 as take-home with the solutions folder as the guide.

## Pre-flight checklist (day before)

- [ ] **Template repo:** confirm *Use this template* is enabled and `hello-world.yml` runs green on a fresh copy (make one yourself, end to end).
- [ ] **Your live-demo copy:** fresh instance of the template under your account; environments `staging`/`production` pre-created with yourself as reviewer.
- [ ] **Demo org** (for Lab 04/07 org demos): access to an org where you can show
  - org Actions policy screen (allowlist UI),
  - org-level secrets/variables,
  - a `.github` repo containing [`org-assets/workflow-templates/`](../org-assets/workflow-templates/) so the starter template appears in *New workflow*,
  - runner groups page.
- [ ] **Codespace warm** for the Lab 07 runner registration demo (plus a throwaway private repo, e.g. `runner-demo`).
- [ ] Actions service status: [githubstatus.com](https://www.githubstatus.com).
- [ ] Verify current action major versions still match the SHA pins in `solutions/` (quarterly maintenance — see below).

## Live-demo scripts

- **Demo 1 (logs/debugging):** run *Debug Me* on your copy. Narrate the three failures in order: workflow-level error (bad action ref — appears as an annotation, no steps run), path failure, npm script typo. Fix live via the web editor, re-running between fixes. This mirrors exactly what attendees then do in Lab 01.
- **Demo 2 (environments):** run your pre-made `deploy.yml`; show the paused run, the review dialog, the environment deployment history, then reject a deployment to show that path too.
- **Demo 3 (org):** flip a repo's Actions policy to "GitHub-owned only", show a third-party action failing to run, flip back. Then show the starter template appearing in *New workflow*.
- **Demo 4 (actions):** run the try-actions workflow; open all three `action.yml`s side by side; emphasize step duration differences (Docker's build tax).
- **Demo 5 (runner):** register a runner in the Codespace against the throwaway **private** repo, run the routed job while the terminal is visible on screen, `Ctrl+C` it, show the queued job, restart, remove. Do **not** rush this — pausing on "Listening for Jobs" while the audience watches the job arrive is the moment of the day.
- **Demo 6 (capstone preview):** run your completed pipeline once before lunch so it's green when you present it; walk the graph backward from the production approval.

## Known risks & mitigations

| Risk | Mitigation |
| --- | --- |
| Attendees on private repos hit the environments paywall | Called out in Labs 00/03; pair them with public-repo neighbors |
| Hosted runner queue delays at popular hours | Front-load Lab 01 runs; have your own completed runs to narrate |
| Org demo unavailable (no org access) | Screenshots deck as fallback; Labs mark these sections "instructor demo" so attendee flow is unaffected |
| Marketplace action pin drift (majors move on) | Quarterly: re-run `git ls-remote --tags` for each pinned action, refresh SHAs in `solutions/` + labs, re-test capstone |
| GHCR push fails: uppercase repo name | Solution workflow includes the lowercasing step — point attendees there |
| Someone registers a self-hosted runner on their public repo | The warning is in Lab 07 twice; repeat it verbally before the lab starts |
| Capstone overruns | It's designed as "start in class, finish at home"; rubric makes completion self-assessable |

## Maintenance (repo owners)

- Node versions: labs use 22.x/24.x; bump when LTS windows shift, update `app/package.json` engines + Dockerfile base + matrix references everywhere (grep for `22.x`).
- Action pins: refresh SHAs quarterly (see risk table).
- Re-run the full capstone on a fresh template copy after any change.

## After the workshop

- Share: link to this repo, the `solutions/` folder, [skills.github.com](https://skills.github.com) for follow-on self-paced courses, and the [GitHub Actions certification](https://examregistration.github.com/) as the formal next step.
- Collect feedback while people are still in the room. Two questions minimum: pace (1–5) and "which lab was most valuable?"
