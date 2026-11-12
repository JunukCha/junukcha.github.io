# Agent guide for junukcha.github.io

This repo is edited from more than one machine (laptop and mini PC), by people and by agents.

## Always start with `git pull`

Before reading or changing anything, run:

```bash
git pull --ff-only origin master
```

- Do this at the start of every task, even if you pulled recently.
- If it fails (local changes or diverged history), stop and tell the user. Do not force-push, reset, or discard changes on your own.
- Pull again right before you push.

## Build and deploy

- Do not build the site locally or with Docker.
- Commit and push to `master` directly. GitHub Actions builds and deploys the site.

## Project pages

Each paper's project page uses the same four places (see OpenFS as the example):

| What | Where |
| --- | --- |
| Page HTML | `_layouts/<name>.html` |
| Permalink stub | `_pages/project-<name>.md` (`layout: <name>`, `permalink: /project/<name>/`) |
| Images and videos | `media/projects/<name>/` |
| Projects list card | `_projects/<n>-<name>.md` (`redirect: /project/<name>/`) |
| Publication link | `website = {/project/<name>/}` in `_bibliography/papers.bib` |
