# CLAUDE.md — unsolved.now conventions

A public catalog of the great **unsolved problems** of science and engineering.
Static Jekyll site, built natively by GitHub Pages from `main` (no Actions, no
plugins). Live at https://unsolved.now. Chalkboard design.

## Cardinal rule

**Zero fabricated data.** The product's credibility is the product. Never invent
dates, prize amounts, discoverers, or progress claims. Every factual claim on the
site must trace to a linked authoritative source returning HTTP 200 with real
content. Two independent references minimum per problem.

**Verify still-open.** Before adding or trusting an entry, confirm the problem is
genuinely unsolved as of now — problems fall (the 3D Kakeya conjecture fell in
2025). `date_curated` is also the "verified still open as of" date.

## Layout of the repo

- `_problems/<slug>.md` — one file per problem; schema documented in README.md.
  Filename = slug = URL (`/problems/<slug>/`).
- `_config.yml` — site config; `fields` map (key → label) drives the board sections
  and landing filter; `form_endpoint` (follow) and `submit_url` (issue form) here.
- `_layouts/problem.html` — problem page; `_layouts/default.html` +
  `_includes/head.html` — shell and per-page meta/OG; `_includes/main.css` — all
  styles, inlined; `_includes/submit_href.html` — issue-form-or-mailto CTA.
- `assets/fonts/caveat-chalk.woff2` — the one self-hosted display font, subsetted
  to latin + weight-pinned (18 KB). Regenerate with fontTools if changing weight.
- `feed.xml`, `sitemap.xml`, `robots.txt` — hand-written Liquid, no plugins.
- `.github/ISSUE_TEMPLATE/suggest-problem.yml` — the "Suggest a problem" CTA target.

The "open for N years" counters are computed from `first_posed` vs the build date
in Liquid — never hardcode them.

## Adding a problem

1. Confirm it's genuinely open and recurring in authoritative sources; pick a
   curiosity-first `title` and a precise one-sentence `statement`.
2. `curl -sL -A "Mozilla/5.0" <url>` each reference — 200 + real content at commit.
3. Create `_problems/<slug>.md` per the schema. `status: curated`,
   `date_curated: <today>`. Omit `prize`/`posed_by`/`progress` if not applicable.
4. New field? Add key → label to `fields` in `_config.yml`.
5. `bundle exec jekyll build` must pass; commit (`content: add <slug>`).

## Build & verify

```sh
export PATH="/opt/homebrew/opt/ruby@3.3/bin:$PATH"   # ruby@3.3 = Pages parity
bundle exec jekyll build                              # must pass before push
```

After push, GitHub Pages deploys automatically. Verify live:

```sh
gh run list --repo hrokholskyi/unsolved.now --limit 1   # or the public Actions API
curl -sL -o /dev/null -w "%{http_code}\n" https://unsolved.now/
curl -sL -o /dev/null -w "%{http_code}\n" https://unsolved.now/problems/<slug>/
```

Screenshots: the agent-browser CDP `captureScreenshot` hangs on this machine
(os error 35), though `eval`/navigation work. Use headless Chrome directly:
`"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new
--window-size=760,1600 --screenshot=out.png <url>`.

## Reddit note (if ever mixing in workflow-style sources)

`www.reddit.com` returns a ~8 KB bot-challenge page to curl (false 200); use
`old.reddit.com` to verify thread titles and counts.

## Conventions

- Conventional commits (`feat:`, `fix:`, `content:`, `docs:`, `chore:`); small.
- Tone: curiosity-first hooks, rigorous underneath. No hype, no jargon in titles,
  no unsourced claims.
- Performance budget: landing under ~100 KB; CSS inlined; font subsetted; JS
  optional progressive enhancement only.
