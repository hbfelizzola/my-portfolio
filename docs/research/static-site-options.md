# Static-site options for hbfelizzola.de on GitHub Pages

Research for the ticket "Which static-site options work on GitHub Pages with Experiences, Projects and three languages?" on the map "Spec the next version of hbfelizzola.de". Researched 2026-11-07 against primary sources (official docs, GitHub API, npm registry). Facts and trade-offs only; the choice belongs to the later ticket "What should the site be built with?".

Requirements being checked: Experiences (forming the Timeline) and Projects (forming the Portfolio; a Project may belong to one Experience and may get its own detail page), in English, German and Portuguese, content edited as files in the repo, no CMS, no server, one maintainer, served by GitHub Pages at hbfelizzola.de.

## Where the repo stands today

- `index.html` is one hand-written page with inline CSS, placeholder entries in "Professional & freelance" and "Personal projects", English only (`<html lang="en">`).
- Pages is **already deployed by GitHub Actions**, not from a branch: the Pages API reports `"build_type": "workflow"` and `.github/workflows/pages.yml` uploads the repo root (`path: .`) as the artifact. `README.md` still describes "Deploy from a branch", which is out of date. (Source: `gh api repos/hbfelizzola/my-portfolio/pages`; `.github/workflows/pages.yml`.)
- The same API call reports `"https_enforced": false` and certificate state `dns_changed` ("Requesting a new certificate").
- The workflow pins `actions/checkout@v5`, `configure-pages@v5`, `upload-pages-artifact@v4`, `deploy-pages@v4`. Latest releases are checkout v7.0.1, configure-pages v6.0.0, upload-pages-artifact v5.0.0, deploy-pages v5.0.1 (GitHub releases API, 2026-11-07).
- Because of that, any option below that adds a build step only changes the workflow's build step and the uploaded `path`; the Pages source setting does not need to change.

## GitHub Pages facts that constrain every option

| Fact | Source |
|---|---|
| Pages is static hosting: it "takes HTML, CSS, and JavaScript files straight from a repository ... optionally runs the files through a build process". No server code, so no `Accept-Language` negotiation or server-side redirects. | [What is GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages) |
| Two publishing sources: deploy from a branch (Jekyll build, or none with `.nojekyll`) or GitHub Actions. A custom workflow is the route for "a build process other than Jekyll". | [Configuring a publishing source](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site) |
| Custom workflow: `configure-pages`, `upload-pages-artifact`, `deploy-pages`; deploy job needs `pages: write` and `id-token: write`; artifact is a gzip'd tar under 10 GB with no symlinks or hard links. | [Using custom workflows](https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages) |
| With a custom Actions workflow, "any existing `CNAME` file is ignored and is not required". The custom domain lives in repo Settings > Pages. Enforce HTTPS is optional and can take up to 24 hours to become available. | [Managing a custom domain](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site) |
| Limits: published site up to 1 GB, soft 100 GB/month bandwidth, deployments time out after 10 minutes; the 10 builds/hour soft limit does not apply to custom Actions workflows. | [GitHub Pages limits](https://docs.github.com/en/pages/getting-started-with-github-pages/github-pages-limits) |
| Branch publishing uses Jekyll 3.10.0 (`github-pages` gem 232) with a fixed plugin allow-list; no i18n plugin is on it. "GitHub Pages cannot build sites using unsupported plugins." | [versions.json](https://pages.github.com/versions.json), [About Pages and Jekyll](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll) |
| The `ubuntu-24.04` runner ships Node.js 22.23.4 and Ruby 3.2.3, so a Node or Ruby build needs no extra install step. | [runner-images Ubuntu2404-Readme](https://github.com/actions/runner-images/blob/main/images/ubuntu/Ubuntu2404-Readme.md) |

### Three languages on a static host (applies to all options)

- Google recommends distinct URLs per language; subdirectories (`/de/`) are "easy to set up" and low maintenance; URL parameters (`?loc=de`) are not recommended. Google advises: "Avoid automatically redirecting" users between language versions. ([Managing multi-regional sites](https://developers.google.com/search/docs/specialty/international/managing-multi-regional-sites))
- `hreflang` alternates (HTML `<link>` tags, HTTP headers, or sitemap are "equivalent from Google's perspective") must be reciprocal, otherwise "the tags will be ignored"; `x-default` covers unmatched languages. ([Localized versions](https://developers.google.com/search/docs/specialty/international/localized-versions))
- Since Pages cannot negotiate, the root `/` either holds one language's content (e.g. English at `/`, German at `/de/`, Portuguese at `/pt/`) or is a static redirect page (meta refresh or JS) to a prefixed default. Eleventy's guide notes content negotiation "Requires some server configuration" ([Eleventy i18n guide](https://www.11ty.dev/docs/i18n/)); Astro and Hugo emit an HTML redirect page in static builds (see below).
- No option translates text for you. Every option needs the UI strings (section labels, "Contact", dates) and each Experience/Project's text written three times; options differ in where those copies live and how missing ones are caught.

### Rendering in the browser vs. at build time

Google renders JavaScript via a render queue that "can take longer" than a few seconds, and still recommends pre-rendering because "not all bots can run JavaScript". ([JavaScript SEO basics](https://developers.google.com/search/docs/crawling-indexing/javascript/javascript-seo-basics)) This matters for the "data file" options below: rendering in the browser leaves the HTML empty for link previews and non-JS crawlers; rendering at build time does not.

## Options

Current stable versions (GitHub releases API / npm registry, 2026-11-07): Eleventy 3.1.8 (Node >= 18), Astro 7.4.7 (Node >= 22.23.4), Hugo 0.169.0, Jekyll 4.4.1 (Pages' built-in is 3.10.0).

### A. Hand-written HTML (status quo)

- **Data**: none; each Experience and Project is markup in the page. A Project's data appears wherever it is shown (Portfolio list, its Experience on the Timeline, its detail page) and in each of three languages.
- **i18n**: three hand-maintained copies (`/index.html`, `/de/index.html`, `/pt/index.html`). Switcher and `hreflang` links are written by hand on every page.
- **Detail pages**: one hand-written file per Project per language (projects x 3 files), sharing no layout; CSS is duplicated unless moved to a shared stylesheet.
- **Deploy**: works today, no change.
- **Upkeep**: zero tooling, nothing to update. Cost grows with content: adding one Project with a detail page touches about 6 files (3 lists + 3 detail pages) plus Experience entries; consistency between languages is checked by eye.

### B1. Plain HTML + data file, rendered in the browser

- **Data**: one JSON file (e.g. `experiences.json`, `projects.json`), with per-language fields or one file per language; `fetch()` + a small script builds the DOM.
- **i18n**: one HTML shell per language, or one shell reading the language from the path. Switcher can be generated from the data.
- **Detail pages**: either a single `project.html?id=...` (query parameter URLs, which Google does not recommend for language and which cannot carry their own static `<title>`/Open Graph tags) or one shell file per Project anyway.
- **Deploy**: works today with the existing workflow, no build step.
- **Upkeep**: no dependencies. Content is invisible to non-JS crawlers and link-preview bots; this bears on the map's open "SEO and social sharing" item.

### B2. Plain HTML + data file, rendered at build time by a small script

- **Data**: JSON (or YAML via one dependency) in the repo; a short Node script (`node:fs` + template literals, no framework) writes `/`, `/de/`, `/pt/`, and one page per Project per language into an output folder.
- **i18n**: whatever the script does: language folders, switcher and `hreflang` links derived from the same list. UI strings live in a small dictionary per language.
- **Detail pages**: a loop over Projects x languages.
- **Deploy**: add `run: node build.mjs` before `upload-pages-artifact` and point `path:` at the output folder; Node 22 is already on the runner.
- **Upkeep**: no third-party code if it stays dependency-free, but the developer owns every feature (escaping, slugs, sitemap, missing-translation checks, dev server/watch). The script grows as the spec grows.

### C. Eleventy (11ty) 3.1.8

- **Data**: global data in `_data/` as JSON or JavaScript out of the box; YAML needs `addDataExtension` plus the `yaml` package ([Global data](https://www.11ty.dev/docs/data-global/), [Custom data formats](https://www.11ty.dev/docs/data-custom/)). Experiences/Projects can also be Markdown files with front matter. No schema validation built in; a Project-to-Experience link is a field you resolve in templates.
- **i18n**: bundled i18n plugin (since v2.0) adds `locale_url` and `locale_links` filters and `page.lang`; the plugin "does not localize that content's strings", so UI strings need your own dictionary or a library ([i18n plugin](https://www.11ty.dev/docs/plugins/i18n/)). The guide recommends one folder per locale with a directory data file setting `lang` ([i18n guide](https://www.11ty.dev/docs/i18n/)). The `locale_links` loop is the documented switcher pattern.
- **Detail pages**: pagination with `size: 1` and a `permalink` creates one page per data item ([Pages from data](https://www.11ty.dev/docs/pages-from-data/)). Paginating over Projects x languages at once is not documented; the documented tools are one paginated template per language folder or reshaping data with the `before` callback ([Pagination](https://www.11ty.dev/docs/pagination/)).
- **Deploy**: Eleventy's GitHub Pages tutorial uses an Actions workflow; with a custom domain, "remove the `--pathprefix` parameter entirely" ([Deployment](https://www.11ty.dev/docs/deployment/)).
- **Upkeep**: one npm dependency (`@11ty/eleventy`) plus a lockfile; templates in Nunjucks/Liquid/JS; output is plain HTML with no client JS unless added. The existing page's markup and CSS can be moved into a layout nearly as is.

### D. Astro 7.4.7

- **Data**: content collections in `src/content.config.ts`; `glob()` reads directories of Markdown, MDX, Markdoc, JSON, YAML or TOML, `file()` reads many entries from one JSON/YAML/TOML file. Zod schemas validate every entry at build time and generate TypeScript types; `reference()` links an entry to another collection (e.g. a Project's Experience) ([Content collections](https://docs.astro.build/en/guides/content-collections/)).
- **i18n**: built-in routing config (`locales`, `defaultLocale`, `routing.prefixDefaultLocale`, `redirectToDefaultLocale`, `fallback`), helpers `getRelativeLocaleUrl()` / `getAbsoluteLocaleUrl()`, and `Astro.currentLocale` on static pages. `Astro.preferredLocale` (browser language) is for on-demand rendered pages, so not available on Pages. UI string translation is not part of it ([Internationalization](https://docs.astro.build/en/guides/internationalization/)).
- **Detail pages**: `getStaticPaths()` + `getCollection()` in e.g. `src/pages/[lang]/projects/[id].astro`, producing one static page per Project per language ([Content collections](https://docs.astro.build/en/guides/content-collections/), [Routing](https://docs.astro.build/en/guides/routing/)).
- **Deploy**: official `withastro/action@v6` (latest v6.1.4) then `actions/deploy-pages@v5`; for a custom domain add `public/CNAME`, set `site` to the domain and remove `base` ([Deploy to GitHub Pages](https://docs.astro.build/en/guides/deploy/github/)). Static redirects are emitted as meta-refresh HTML ([Routing](https://docs.astro.build/en/guides/routing/)).
- **Upkeep**: npm project with a larger dependency tree, Node >= 22.23.4 (npm `engines`), major versions roughly yearly (now at 7). Ships zero client JS by default; components (`.astro`) are HTML-like. Schema validation catches a missing German title or a broken Experience reference at build time.

### E. Hugo 0.169.0

- **Data**: `data/` directory (JSON, TOML, YAML, XML; not CSV) merged into `site.Data` and shared across languages ([Data sources](https://gohugo.io/content-management/data-sources/)); or Experiences/Projects as content files (Markdown with front matter), which is Hugo's native unit for pages and translations. Content adapters (`_content.gotmpl`, per language or with `EnableAllLanguages`) create pages from data with `AddPage` ([Content adapters](https://gohugo.io/content-management/content-adapters/)).
- **i18n**: the most complete built-in support of the candidates. `languages` config, translation by filename (`about.de.md`) or by per-language `contentDir`, `translationKey` linking, string tables in `i18n/de.yaml` used via `T` with fallback to the default language and `--printI18nWarnings` for gaps ([Multilingual](https://gohugo.io/content-management/multilingual/)). `.Translations` returns the other-language versions of the current page, the documented switcher ([Translations](https://gohugo.io/methods/page/translations/)). With `defaultContentLanguageInSubdir = true`, the root redirects to the default language unless `disableDefaultLanguageRedirect` is set ([Configuration](https://gohugo.io/configuration/all/)).
- **Detail pages**: each Project content file (or `AddPage` call) is a page per language.
- **Deploy**: official workflow pins Hugo 0.169.0 and Dart Sass, builds `hugo build --gc --minify`, takes `--baseURL` from `configure-pages`, uploads `./public` ([Host on GitHub Pages](https://gohugo.io/host-and-deploy/host-on-github-pages/)). Custom domain via Pages settings (CNAME file ignored under Actions, per GitHub above).
- **Upkeep**: single binary, no `node_modules`; upgrades are a version bump in the workflow, but Hugo is pre-1.0 and its docs show recent config/feature churn (e.g. the newer "sites matrix" for adapters). Go templates are the least HTML-like syntax of the candidates.

### F. Jekyll (GitHub Pages' built-in generator)

- **Data/detail pages**: collections with `output: true` give one page per document ([Collections](https://jekyllrb.com/docs/collections/)); `_data/` for YAML/JSON.
- **i18n**: no i18n plugin on Pages' allow-list, so three languages on branch publishing means hand-rolled language folders and lookups; a plugin such as jekyll-polyglot needs an Actions build (and then Jekyll has no Pages-specific advantage).
- **Deploy**: branch publishing runs Jekyll 3.10.0, older than current Jekyll 4.4.1 (released 2025-01-29).
- **Upkeep**: Ruby toolchain locally. Included for completeness; it is the only generator Pages builds without a workflow, which this repo no longer relies on.

## Comparison

| | Data for Experiences/Projects | 3 languages + switcher | Detail page per Project | Pages deploy (custom domain) | Solo upkeep |
|---|---|---|---|---|---|
| A. Hand-written HTML | None; copy per place and language | Manual copies, manual switcher/`hreflang` | Hand-written file per Project x 3 | Works now | No tooling; content edits multiply x3+ |
| B1. Data file, browser-rendered | JSON | Manual shells; switcher from data | Query-param shell or per-Project shells | Works now | No deps; content not in HTML (SEO/previews) |
| B2. Data file, build script | JSON (YAML with 1 dep) | Whatever you write | Loop you write | Add `run:` step, change `path` | No deps; you own all features |
| C. Eleventy 3.1.8 | JSON/JS `_data`, YAML via 1 dep, or Markdown; no schema | i18n plugin: `locale_url`, `locale_links`; strings DIY | Pagination `size: 1`; per-language templates | Actions workflow, no path prefix | 1 npm dep; templates close to current HTML |
| D. Astro 7.4.7 | Collections from MD/JSON/YAML/TOML, Zod-validated, `reference()` | Built-in routing + URL helpers; strings DIY | `getStaticPaths()` | `withastro/action`, `public/CNAME` | Larger npm tree, Node >= 22.23.4, yearly majors |
| E. Hugo 0.169.0 | `data/` or content files; content adapters | Most built-in: translations, `T` string tables, `.Translations` | Native (content file = page) | Official workflow pins binary | Single binary; Go templates; pre-1.0 churn |
| F. Jekyll | Collections, `_data` | No plugin on Pages; DIY | Collections `output: true` | Branch (3.10.0) or Actions | Ruby; i18n needs Actions anyway |

## Trade-offs worth carrying into "What should the site be built with?"

- **Content multiplication vs. tooling**: every option stores three languages of text; A and B1 also multiply structure (markup and links) per language and per place a Project appears. B2 through E write structure once.
- **Where a missing translation is caught**: Astro (schema), Hugo (`--printI18nWarnings`, missing-translation placeholders) and Eleventy (`errorMode` for missing localized pages) give build-time signals; A, B1 and B2 rely on review unless B2 adds checks.
- **Project belongs to one Experience**: Astro models it directly (`reference()`, validated); in Eleventy, Hugo and B2 it is an ID field resolved in templates.
- **Dependency footprint**: none (A, B1, B2) < Hugo binary < Eleventy (one package) < Astro.
- **Downloadable CV** (open map item): options with a structured data store (B2, C, D, E) can render a CV page from the same Experience data; A cannot without duplication.
- **Root URL**: all options face the same choice (default language at `/` vs. redirect page), since Pages cannot negotiate language.
