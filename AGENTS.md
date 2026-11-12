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
| Navbar entry | the `project_pages` list in `_includes/project_navbar.html` |

Order the `_projects` cards newest paper first (`importance: 1` is the newest).

## CV PDFs (Overleaf, via Claude in Chrome)

The CV source lives in the private repo `JunukCha/CV` (English `resume.tex` + `cv/`, Korean `resume_ko.tex` + `cv_ko/`).
Keep the English CV, the Korean CV and `_pages/cv.md` in agreement. The PDFs are built in Overleaf and copied here as
`assets/pdf/CV.pdf` (English) and `assets/pdf/CV_kor.pdf` (Korean).

Use Claude in Chrome for Overleaf: the user is signed in there. The built-in browser is not signed in to Overleaf.

1. Commit and push the `.tex` changes to `JunukCha/CV`.
2. Open the Overleaf project named **CV** (`https://www.overleaf.com/project`), open the GitHub integration and click
   **Pull GitHub changes into Overleaf**. Wait for "No new commits in GitHub since last merge." Never click **Push Overleaf changes to GitHub**.
3. English: the main document is `resume.tex`. Click **Recompile**, then the **Download PDF** button in the PDF toolbar.
4. Korean: Overleaf compiles only the main document (the compile API ignores `rootDoc_id`). Set the main document to `resume_ko.tex`
   (Menu → Main document, or `POST /project/<id>/settings` with `{"rootDocId": "<resume_ko.tex doc id>"}` and the `X-Csrf-Token` from
   `meta[name="ol-csrfToken"]`), reload, **Recompile**, then **Download PDF**.
5. Set the main document back to `resume.tex`.
6. Download with the toolbar button, one at a time. Chrome blocks repeated script-triggered downloads.
   Files land in `~/Downloads` as `CV.pdf`, `CV (1).pdf`, and so on. Open each one and check its language and content before using it.
7. Copy the English PDF to `assets/pdf/CV.pdf` and the Korean PDF to `assets/pdf/CV_kor.pdf`. On the laptop, also copy them to
   `OneDrive\바탕 화면\준욱\CV.pdf` and `CV_kor.pdf`. Delete the downloaded copies, then commit and push here.
