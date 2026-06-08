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

- **Full-text search** across every submission. Type multiple words (all must
  appear) or `"a quoted phrase"` for an exact match. Results are ranked by
  number of mentions, with highlighted snippets, and the reading pane jumps to
  and highlights every hit.
- **Filter & browse** by submission type (Organisation / Named individual /
  Name withheld), "personal / parent accounts only", theme, and minimum length.
- **Themes & Frequency** — for whatever set you've filtered/searched to, see how
  many submissions mention each theme (anxiety & mental health, neurodivergence
  & disability, bullying, services, school response, funding, alternative
  education, family impact) plus the most frequent words.
- **Tagging & export** — tag/code any submission, add notes, and save quotes you
  select. Export your tags & notes, or the current result list, to CSV.
  *Tags are stored in your own browser (localStorage) — they are personal to
  each researcher and are not shared between people or devices.*

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
