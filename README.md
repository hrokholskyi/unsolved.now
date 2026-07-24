# unsolved.now

A public catalog of the great **unsolved problems** of science and engineering —
how long each has been open, why it resists, what progress has been made, and what
falls when it's solved. Every date, prize, and progress claim is cited to an
authoritative source.

Live: **https://unsolved.now**

## Stack: zero-plugin Jekyll on the native GitHub Pages branch build

Decision criteria, in order: boring/durable, data-driven, minimal build complexity,
fast. The choice:

- **Jekyll, built natively by GitHub Pages from `main`.** Pushing to `main` is the
  entire deploy pipeline — no Actions workflow, no Node toolchain, no lockfile that
  can rot. GitHub has run this exact path for a decade and maintains it; it will
  still build cleanly in two years untouched.
- **Zero Jekyll plugins.** Meta/OG tags, `sitemap.xml`, `feed.xml` (Atom), and
  `robots.txt` are small hand-written Liquid templates — nothing to break, exact
  control over the SEO surface.
- **Data-driven:** every problem is one Markdown file with YAML frontmatter in
  `_problems/`; all pages render from that data. No hardcoded catalog HTML.
- **Fast:** CSS is inlined (~9 KB); one self-hosted, subsetted chalk font
  (Caveat, 18 KB woff2, latin-only, weight-pinned) used sparingly for display;
  JS is ~20 lines of optional progressive enhancement.

## Design

Chalkboard: the universal image of an unsolved problem is a blackboard covered in
half-finished equations. Dark board (`#1B2521`), chalk-white serif body, a
handwritten display face (Caveat) reserved for the emotional beats — the big
"open for N years" counters and the timeline years — and a single warm chalk-yellow
accent. Fully functional without JavaScript; keyboard-navigable; respects reduced
motion.

## Data schema

One file per problem: `_problems/<slug>.md`. Frontmatter fields:

| Field | Required | Notes |
|---|---|---|
| `slug` | yes | Must match the filename (drives the URL `/problems/<slug>/`). |
| `name` | yes | Short proper name ("The Riemann Hypothesis"). Shown as the eyebrow and in rows. |
| `title` | yes | Curiosity-first, plain-language hook — what we *don't* know. |
| `field` | yes | A key from `fields` in `_config.yml`. |
| `statement` | yes | One precise sentence of the actual open question. |
| `first_posed` | yes | Year (integer). Drives the "open for N years" counter. |
| `posed_by` | no | Who posed it / where it originates. |
| `prize` | no | Real, verified prize (e.g. "Clay Millennium Prize — $1,000,000"). Omit if none. |
| `summary` | yes | 3–5 accessible sentences. Doubles as the meta description. |
| `why_it_matters` | yes | 2–3 sentences of concrete stakes. |
| `progress` | no | List of `"YEAR — milestone"` strings, real and dated. |
| `references` | yes | List, min 2: `url`, `source`, `note`. Independent, authoritative, verified live. |
| `status` | yes | `curated`. |
| `date_curated` | yes | `YYYY-MM-DD`; also the "verified still open as of" date. |

The "open for N years" counters are computed at build time from `first_posed` and
the build date — they stay current on every rebuild with no manual edits.

## Content curation rules

1. **Zero fabricated data.** Every date, name, prize, and progress claim traces to
   a linked authoritative source, verified live (HTTP 200 + real content) at
   curation time.
2. **Must be genuinely open.** Each entry is checked for recent resolutions before
   inclusion (problems *do* fall — the 3D Kakeya conjecture fell in 2025). The
   `date_curated` doubles as "verified still unsolved as of".
3. **Curiosity-first, precision underneath.** Titles are plain-language hooks;
   the `statement` and details are exact. No jargon in the hook, no hand-waving in
   the body.
4. **Authoritative sources only** — Clay Institute, arXiv, Nature/Science, CERN,
   NASA, Nobel, university/institute pages, Quanta for recent progress. Wikipedia
   allowed as at most one of the two links.
5. If it can't be sourced or might already be solved, it's cut.

## Local development

```sh
brew install ruby@3.3
export PATH="/opt/homebrew/opt/ruby@3.3/bin:$PATH"
bundle install
bundle exec jekyll serve   # → http://127.0.0.1:4000
```

One-command build check: `bundle exec jekyll build`.

## Deployment

Push to `main`. GitHub Pages builds natively (the `pages build and deployment`
workflow appears in the Actions tab). Custom domain `unsolved.now` via `CNAME`.
Verify live after deploy:

```sh
curl -sL -o /dev/null -w "%{http_code}" https://unsolved.now/
curl -s https://unsolved.now/sitemap.xml | head
curl -s https://unsolved.now/feed.xml | head
```

## Owner TODO

- [ ] **Follow-the-board endpoint** — create a Buttondown/Formspree form and put its
  POST URL into `form_endpoint` in `_config.yml`. Until then the follow CTA is a
  `mailto:` to `contact_email` (currently the owner's Gmail — change it there if
  you'd rather not expose it).
- [ ] **Analytics (optional)** — GoatCounter is a privacy-friendly, no-cookie-banner
  option. Deliberately not integrated with a placeholder key.

Everything else (GitHub Issues for suggestions, `gh` auth, `www` DNS, Ruby TLS) is
resolved and verified.

## History

The first iteration cataloged unsolved *workflow* problems (a demand-discovery
index). That version is preserved on the `workflow-catalog` branch. The `main`
site pivoted to the great open problems of science and engineering.
