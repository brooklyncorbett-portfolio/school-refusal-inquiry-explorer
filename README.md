# School Refusal Inquiry — Submission Explorer

A self-contained web app for searching and doing preliminary analysis of the
public submissions to the Australian Senate inquiry **"The national trend of
school refusal and related matters"** (Senate Education and Employment
References Committee).

It is aimed at researchers reading the **parent / individual** submissions in
particular, but covers all 151 published submissions with extractable text.

## What's in this folder

| File | What it is |
|------|------------|
| `index.html` | The entire app — HTML, CSS and JavaScript in one file. No build step, no dependencies. |
| `data.json`  | The dataset: full text + metadata for every submission (~3 MB). |
| `README.md`  | This file. |

That's it. The two files (`index.html` + `data.json`) **are** the website.

## Features

- **Search & Browse** — opens on **Parent submissions** (the 78 name-withheld
  lived-experience accounts); one click shows **All submissions**. Full-text
  search (multiple words = all must appear, or `"a quoted phrase"`), ranked with
  highlighted snippets; the reading pane jumps to and highlights every hit.
  Extra filters: theme, minimum length, reading status, and auto-detected
  **context** (condition e.g. autism/ADHD/anxiety, state, school type, school
  stage).
- **What parents want** — auto-extracted recommendation/request sentences
  ("…should…", "…need to…", "…recommend…") across the current set, filterable
  and exportable. A fast way to see what parents are asking the inquiry to change.
- **Word in context (KWIC)** — type any word or phrase and get every mention
  with its surrounding text, in a table you can export. The quick way to pull
  quotes for a given term (e.g. *suspension*, *wait list*, *NDIS*).
- **Themes & Frequency** — a **Parents vs organisations** comparison (share of
  each group mentioning each theme), plus per-set theme coverage and most
  frequent words.
- **Tagging, reviewing & export** — tag/code submissions, add notes, save
  selected quotes, and mark submissions **reviewed** (with initials) to divide
  reading across the team. Export tags, the recommendation list, the
  concordance, or the current result list to CSV.
  *Tags and review status are stored in each person's own browser
  (localStorage) — they persist on that device but are **not shared** between
  people. Use CSV export to combine the team's work.*

## Running it locally

Any static file server works. From inside this `app` folder:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

(Opening `index.html` directly with `file://` will **not** work — browsers block
`fetch()` of `data.json` from the file system. Use a local server, or host it.)

## Hosting it online (so colleagues can just visit a URL)

The app is fully static, so any static host works for free. Easiest options:

1. **Netlify Drop** (no account needed to try): go to
   <https://app.netlify.com/drop> and drag this whole `app` folder onto the
   page. You'll get a live URL in seconds. Create a free account to keep it.
2. **Cloudflare Pages / GitHub Pages / Vercel** — point them at this folder
   (or a repo containing it). No build command; output directory is this folder.

### A note on the data (please read before hosting publicly)

Every submission here was **published by the committee** on aph.gov.au, so it is
already public. "Name withheld" submitters asked for their *name* to be withheld
— and it is (shown as "Name Withheld"). However, some submission *text* may still
contain personal detail. Re-publishing already-public documents is normally fine,
but if this is for a formal research project you may want to (a) host it behind a
login / share privately rather than fully open, and (b) check it against your
project's ethics approval. The app works identically whether hosted publicly or
privately.

## Refreshing / rebuilding the dataset

The dataset was built by the scripts in the parent folder
(`../scrape_list.py`, `../download_extract.py`, `../build_data.py`). To rebuild
(e.g. if new submissions are published), re-run them in that order; the last one
regenerates `data.json`.
