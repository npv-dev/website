# NPV website

Source of **https://npv.co.nz**, the public website of NPV Development Limited.
It is a small static site built with [Hugo](https://gohugo.io/): no theme, no
JavaScript, no external fonts, images or scripts, no cookies and no analytics.

## Layout

| Path | What it holds |
|---|---|
| `content/` | The pages, as Markdown (`_index.md`, `contact.md`, `privacy.md`) |
| `layouts/` | The page templates |
| `static/` | `style.css`, `favicon.svg` and `_headers` (the security headers) |
| `hugo.toml` | Site settings and the company details shown in the footer |
| `wrangler.toml` | Cloudflare Workers deploy config: static assets only |
| `.hugo-version` | The pinned Hugo version |

## Build and preview locally

The site is built with **Hugo 0.167.0** (the standard edition is enough). The
version is written in `.hugo-version`, in `hugo.toml` and here; keep the three
in step when it changes.

    hugo server                  # live preview on http://localhost:1313
    hugo --minify                # build into public/ (not committed)

## Deploy

Cloudflare Workers Builds builds and deploys this repository to a Workers static
assets project. The settings are:

| Setting | Value |
|---|---|
| Root directory | `/` (the repository root) |
| Build command | `hugo --minify` |
| Deploy command | `npx wrangler deploy` |
| Build variable | `HUGO_VERSION` = `0.167.0` |

No credential is stored in this repository or in GitHub: Cloudflare's GitHub app
is installed on this one repository, and nothing else is needed. Never commit an
API token, a key or any other secret.

The security headers (a strict Content-Security-Policy, `X-Frame-Options` and
others) live in `static/_headers` and apply to every response, because the
Worker has no script of its own.

## Changing the site

Open a pull request against `main`. Merging to `main` publishes the site, so the
site owner's merge is the review. Keep the site free of cookies, analytics,
tracking and third-party assets: the privacy page promises exactly that.
