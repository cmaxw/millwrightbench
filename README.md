# millwrightbench.com

The Millwright site. Hugo, hand-rolled layouts, one stylesheet, zero
JavaScript, no npm.

## Requirements

Hugo **0.125 or newer** (standard edition — the extended build is not needed,
since there is no SCSS). Built and verified against 0.148.2. That is the only
dependency: no npm, no `package.json`, no theme.

```
brew install hugo          # macOS
sudo pacman -S hugo        # Arch
# or grab a binary: https://github.com/gohugoio/hugo/releases
```

## Run locally

```
hugo server -D             # http://localhost:1313, -D includes drafts
```

## Build

```
hugo --gc --minify         # output lands in public/
```

## Add a Writing post

Create `content/writing/some-slug.md`:

```yaml
---
title: "Post title"
description: "150–160 character summary. Used for the meta description, the
  Open Graph description, the listing page, and the Article JSON-LD."
date: 2026-08-22
lastmod: 2026-08-22
topics: ["ai-policy", "legislation"]
draft: false
---
```

Notes:

- Start the body at `##`. The `<h1>` is generated from `title`, and every page
  gets exactly one.
- `topics` is the site's single flat taxonomy. Taxonomy listing pages are
  disabled at launch (`disableKinds` in `hugo.toml`); the values are there for
  JSON-LD keywords and for turning listing pages on later.
- `description` is not optional. It carries the meta description, the OG
  description, and the summary shown on `/writing/`.
- RSS is emitted for `/writing/` only, at `/writing/index.xml`. It is enabled
  by the `outputs` key in `content/writing/_index.md`, not site-wide.

## Standard page front matter

`content/{build,policy,speaking,about,contact}/_index.md`:

```yaml
---
title: "Policy"
description: "150–160 characters. Meta description and og:description."
layout: "standard"
draft: false
---
```

## Editing the other pages

Each page is one markdown file under `content/`. The five standard pages carry
`layout: "standard"` in their front matter — leave that key alone (see
[Layouts](#layouts) for why). Placeholder copy is marked
with `<!-- TODO: replace -->` followed by a `[PLACEHOLDER — …]` block, and the
headings are already in the shape the finished argument should take. Replace
section by section; delete the TODO comment as you go.

To find everything still unwritten:

```
grep -rn "PLACEHOLDER" content/ layouts/ static/
```

Two files carry copy outside the markdown body:

- `content/_index.md` — the home page's two-path fork lives in front matter
  `params` (headings, blurbs, link labels), because the two paths need
  different markup. The body of the file is the positioning statement.
- `layouts/partials/footer.html` — the affiliations line.

## Page-by-page rules worth not breaking

- **`/policy/` is not a services page.** No engagement types, no pricing, no
  "how we work", no booking CTA. It ends with a plain line offering to talk and
  an email address. `layouts/_default/standard.html` emits the CTA partial for
  `build` and `speaking` only; leave Policy out of that list.
- **`/build/` is a services page.** CTA expected and present.
- **Top End Devs is a separate business.** It is linked from `/about/` and
  named in `llms.txt`. It does not get branding, content, or nav space here.
- The home fork's two paths are asymmetric on purpose: build ends in a button,
  policy ends in a plain link. They should not look like two products in a
  catalog.

## Layouts

```
layouts/
├── index.html              Home — the two-path fork
├── 404.html
├── sitemap.xml             Sitemap (see below)
├── _default/
│   ├── baseof.html         Shell: head, header, main, footer
│   ├── standard.html       Standard page (Build, Policy, Speaking, About, Contact)
│   ├── single.html         A Writing post
│   └── list.html           The Writing index
└── partials/
    ├── head.html           Meta, OG, Twitter card, canonical, stylesheet, RSS link
    ├── header.html         Nav
    ├── footer.html         Contact, affiliations, copyright
    ├── schema.html         JSON-LD
    └── cta.html            The "book a call" block
```

### Why the standard-page layout is called `standard`, not `page`

The five standard pages live at `content/<section>/_index.md`, which makes Hugo
treat them as **section** pages, not single pages — so they never reach
`_default/single.html`. Their front matter sets `layout: "standard"` to route
them to `_default/standard.html`.

That layout deliberately is **not** named `page.html`. `page`, `section`,
`list`, `home`, `term`, and `taxonomy` are reserved kind names in Hugo's
template lookup, so a section page can never resolve a layout called "page" —
it silently falls through to `_default/list.html` and renders as the Writing
index instead, with no build error. (Verified against Hugo 0.148.) Rename that
file and the five standard pages break quietly.

So: `standard.html` serves the five standard pages, `single.html` serves
Writing posts (the only true single pages), and `list.html` serves `/writing/`.

### Why there is a hand-written `sitemap.xml`

Hugo's built-in sitemap template ranges over the home page's `.Pages`, which is
just the top-level sections. Once `[outputs]` is customised in `hugo.toml` — as
it is here, to scope RSS to `/writing/` — that drops the home page and every
Writing post from the sitemap, again with no build error.
`layouts/sitemap.xml` ranges over `site.Pages` instead, so everything is
listed. Check `public/sitemap.xml` after any change to `[outputs]`.

## Structured data

`layouts/partials/schema.html` emits one JSON-LD block per page kind:

| Page | Type |
|---|---|
| Home | `ProfessionalService` |
| `/about/` | `Person` — the canonical `@id` |
| `/writing/*` | `Article`, `author` referencing that `Person` `@id` |

The `Person` block pulls `sameAs` from `params.social` in `hugo.toml`. Those
URLs are placeholders (`REPLACE-ME`) — fill them in before launch, or drop the
entries you do not want.

Validate after editing: https://validator.schema.org/

## Before launch

Search for `REPLACE-ME` and fix:

- `params.bookingURL` in `hugo.toml`
- `params.social` in `hugo.toml` (LinkedIn, GitHub)
- the calendar embed in `content/contact/_index.md`

Also confirm `chuck@millwrightbench.com` is receiving mail — it appears in the
footer, on `/policy/`, on `/about/`, and in `llms.txt`.

## Deploy — Cloudflare Pages

1. Push this repo to GitHub.
2. Cloudflare dashboard → Workers & Pages → Create → Pages → connect the repo.
3. Build settings:
   - Framework preset: **Hugo**
   - Build command: `hugo --gc --minify`
   - Build output directory: `public`
   - Environment variable: `HUGO_VERSION` = the version you build with locally
     (`hugo version`). Pin it — Cloudflare's default Hugo is old.
4. Add `millwrightbench.com` under Custom domains. Cloudflare issues the TLS
   certificate.

Netlify is equivalent: same build command, same output directory, and
`HUGO_VERSION` set in `netlify.toml` or the UI.

## Non-goals

No CMS, no npm or `package.json`, no CSS framework, no JS framework, no
comment system, no newsletter signup, no cookie banner, no client-side
analytics. The site targets a sub-1s load and 100 across Lighthouse; every one
of those additions costs some of that, and the speed is itself part of the
pitch. The only defensible exception is the calendar provider's embed script on
`/contact/` — and if the provider offers a plain booking link, use the link.
