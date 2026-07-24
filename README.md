# unsolved.now

A public index of real, unsolved workflow problems — curated from public discussions,
documented with linked evidence. The inverse of a product directory: demand first,
solutions later.

Live: **https://unsolved.now**

## Stack: zero-plugin Jekyll on the native GitHub Pages branch build

Decision criteria were, in order: boring/durable, data-driven, minimal build
complexity, fast. The choice:

- **Jekyll, built natively by GitHub Pages from `main`.** Pushing to `main` is the
  entire deployment pipeline — no Actions workflow, no Node toolchain, no lockfile
  that can rot. GitHub has run this exact build path for over a decade and maintains
  it; it will still build cleanly in two years untouched. It is also the only SSG that
  deploys with the repo's current Pages configuration ("deploy from branch") without
  any settings change.
- **Zero Jekyll plugins.** Meta/OG tags (`_includes/head.html`), `sitemap.xml`,
  `feed.xml` (Atom), and `robots.txt` are small hand-written Liquid templates —
  nothing to break, exact control over the SEO surface.
- **Data-driven:** every problem is one Markdown file with YAML frontmatter in
  `_problems/`; all pages render from that data. No hardcoded catalog HTML.
- **Fast:** CSS is inlined (~7&nbsp;KB), fonts are system stacks, JS is ~20 lines of
  optional progressive enhancement. The landing page is a single HTML request, well
  under 100&nbsp;KB.

## Data schema

One file per problem: `_problems/<slug>.md`. Frontmatter fields:

| Field | Required | Notes |
|---|---|---|
| `slug` | yes | Must match the filename (filename drives the URL `/problems/<slug>/`). |
| `title` | yes | The pain, phrased specifically and in the sufferer's language. |
| `who` | yes | Role/segment experiencing it. |
| `vertical` | yes | A key from `verticals` in `_config.yml`. |
| `summary` | yes | 2–4 concrete sentences. Doubles as the meta description. |
| `evidence` | yes | List, minimum 2 items: `url`, `source`, `date` (of the discussion), `note` (what it shows). All links must be independent and verified live. |
| `current_workarounds` | yes | What people do today / tools tried, as found in sources. |
| `why_unsolved` | yes | Editorial analysis; rendered under an explicit "editorial" label. |
| `signals` | no | List of directly observed, source-backed signals only. **Omit the field entirely if none.** |
| `status` | yes | `curated` for all phase-1 entries. Future: `community-validated`, … |
| `date_curated` | yes | `YYYY-MM-DD`. |

## Content curation rules

1. **Zero fabricated data.** No invented vote counts, user numbers, quotes,
   willingness-to-pay figures, testimonials, or logos. Every factual claim traces to
   a linked public source.
2. A problem qualifies only if it recurs across **≥ 2 independent sources**
   (different threads/communities/authors — not one discussion cross-posted).
3. Specific and plausibly monetizable. "Communication is hard" doesn't qualify.
4. Every evidence link is verified live (HTTP 200) before commit.
5. Analysis is labeled as analysis (`why_unsolved` renders under an explicit
   editorial flag). Signals report only what was directly observed on the page.
6. If it can't be sourced, it gets cut. Fewer excellent entries beat padded ones.

## Local development

```sh
# once: install ruby 3.3 (GitHub Pages build parity) and deps
brew install ruby@3.3
export PATH="/opt/homebrew/opt/ruby@3.3/bin:$PATH"
bundle install

# serve locally
bundle exec jekyll serve   # → http://127.0.0.1:4000
```

One-command build check: `bundle exec jekyll build`.

## Deployment

Push to `main`. GitHub Pages builds the site natively (the
`pages build and deployment` workflow appears in the Actions tab). Custom domain
`unsolved.now` is configured via `CNAME`. Verification loop after deploy:

```sh
curl -sL -o /dev/null -w "%{http_code}" https://unsolved.now/          # expect 200
curl -s https://unsolved.now/sitemap.xml | head                        # sitemap reachable
curl -s https://unsolved.now/feed.xml | head                           # feed reachable
```

## Owner TODO

Things only the repo owner can do; the site degrades gracefully without them:

- [ ] **Enable Issues on the repo** — Issues are currently disabled, so the GitHub
  Issue Form (the "Submit a problem" CTA target) 404s. Tick *Settings → General →
  Features → Issues*, then set `issues_enabled: true` in `_config.yml` and push.
  Until then, all Submit CTAs degrade to a structured `mailto:` mirroring the form.
- [ ] **Builder waitlist endpoint** — create a Formspree (or Buttondown) form and put
  its POST URL into `form_endpoint` in `_config.yml`. Until then the waitlist CTA is
  a `mailto:` link to `contact_email` (currently the owner's Gmail — change it there
  if you'd rather not expose it).
- [ ] **`www` DNS record** — `www.unsolved.now` currently doesn't resolve. Add a
  `CNAME` record `www → hrokholskyi.github.io` at your DNS provider; GitHub will
  redirect it to the apex.
- [ ] **`gh auth login` on the dev machine** — lets future sessions manage Pages
  settings/API. Everything in phase 1 worked without it (SSH push + public API).
- [ ] **Analytics (optional)** — if wanted, GoatCounter is a privacy-friendly,
  no-cookie-banner option. Deliberately not integrated with a placeholder key.

Local-dev quirk: on the original dev machine, Ruby's TLS traffic is blocked by
something network-level (curl works, `bundle install` times out), so local Jekyll
builds were impossible; verification runs against the live deployment instead
(see CLAUDE.md). On a normal network `bundle install` + `jekyll serve` work fine.
