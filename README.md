# hbfelizzola.de

Personal portfolio of Humberto Felizzola. A single static page (`index.html`) with no build step, served by GitHub Pages at https://hbfelizzola.de.

## Editing

Change `index.html` and push to `main`. GitHub Pages republishes within a minute or two.

## Hosting setup

- Repo **Settings → Pages**: Source "Deploy from a branch", branch `main`, folder `/ (root)`. Custom domain `hbfelizzola.de` (also stored in `CNAME`), then **Enforce HTTPS**.
- GoDaddy DNS for hbfelizzola.de:

| Type  | Name | Value                 |
|-------|------|-----------------------|
| A     | @    | 185.199.108.153       |
| A     | @    | 185.199.109.153       |
| A     | @    | 185.199.110.153       |
| A     | @    | 185.199.111.153       |
| CNAME | www  | hbfelizzola.github.io |
