# CLAUDE.md — unsolved.now conventions

Curated index of real, unsolved workflow problems. Static Jekyll site, built natively
by GitHub Pages from `main` (no Actions, no plugins). Live at https://unsolved.now.

## Cardinal rule

**Zero fabricated data.** The product's entire value is verified evidence. Never
invent vote counts, user numbers, quotes, dates, testimonials, or engagement figures.
Every factual claim on the site must trace to a linked public source that returns
HTTP 200. Editorial opinion is allowed only in `why_unsolved`, which renders under an
explicit "editorial analysis" label.

## Layout of the repo

- `_problems/<slug>.md` — one file per problem; schema documented in README.md.
  Filename = slug = URL (`/problems/<slug>/`).
- `_config.yml` — site config; `verticals` map (key → label) drives the landing
  filter; `form_endpoint` (waitlist) and `submit_url` (issue form) live here.
- `_layouts/problem.html` — problem page; `_layouts/default.html` + `_includes/head.html`
  — shell and per-page meta/OG; `_includes/main.css` — all styles, inlined.
- `feed.xml`, `sitemap.xml`, `robots.txt` — hand-written Liquid, no plugins.
- `.github/ISSUE_TEMPLATE/submit-problem.yml` — the "Submit a problem" CTA target.

## Adding a problem

1. Verify it meets the bar: recurring in ≥2 independent live sources, specific,
   plausibly monetizable (curation rules in README.md).
2. `curl -sL -o /dev/null -w "%{http_code}" -A "Mozilla/5.0" <url>` each evidence
   link — must be 200 at commit time.
3. Create `_problems/<slug>.md` following the schema. Omit `signals` entirely if
   there are none. `status: curated`, `date_curated: <today>`.
4. If it's a new vertical, add the key → label to `verticals` in `_config.yml`.
5. Build locally, then commit (`content: add <slug>` conventional style).

## Build & verify

```sh
export PATH="/opt/homebrew/opt/ruby@3.3/bin:$PATH"   # ruby@3.3 = Pages parity
bundle exec jekyll build                              # must pass before push
```

After push, GitHub Pages deploys automatically. Verify live (repo is public, so the
workflow status is visible unauthenticated):

```sh
curl -s "https://api.github.com/repos/hrokholskyi/unsolved.now/actions/runs?per_page=1" \
  | python3 -c "import json,sys; r=json.load(sys.stdin)['workflow_runs'][0]; print(r['status'], r['conclusion'])"
curl -sL -o /dev/null -w "%{http_code}\n" https://unsolved.now/
curl -sL -o /dev/null -w "%{http_code}\n" https://unsolved.now/problems/<new-slug>/
```

Note: `gh` CLI is not authenticated on this machine (owner TODO); use SSH git +
the public REST API as above.

## Conventions

- Conventional commits (`feat:`, `fix:`, `content:`, `docs:`, `chore:`); small and
  reviewable.
- Tone everywhere: precise, evidence-first, builder-facing. No hype, no
  marketing superlatives, no implying validation machinery that doesn't exist yet
  (phase 1 = curated only).
- Performance budget: landing page under ~100 KB transferred excluding images; CSS
  stays inlined; JS remains optional progressive enhancement.
