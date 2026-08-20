# Agent Instructions — Gino Pack's Blog

This is a Jekyll blog hosted on GitHub Pages. Read this fully before making changes — several
choices below were made deliberately after hitting real build failures, and reverting them will
reintroduce bugs that were already solved.

## Stack & build

- **Static site generator:** Jekyll, theme = `minima`
- **Ruby dependency management:** `Gemfile` uses the `github-pages` gem (NOT a direct `jekyll` +
  `minima` dependency). This pins Minima to **version 2.5.x** — see "Known constraints" below.
- **Deploy method:** GitHub Actions (`.github/workflows/jekyll.yml`), building via
  `bundle exec jekyll build`. Pages source in repo Settings is set to "GitHub Actions."
- **Repo base path:** the site is NOT at the root of `username.github.io` — check `baseurl` and
  `url` in `_config.yml` match the actual repo name before assuming asset/link paths.

## Known constraints — do not "fix" these without reading this first

1. **Do not upgrade to Minima 3.0.** We deliberately stayed on the `github-pages` gem (Minima
   2.5.x) rather than pulling `minima` and `jekyll` directly, after weighing the trade-off:
   losing GitHub's centrally-tested dependency pinning wasn't worth gaining `minima.skin` and
   `minima.social_links`. Do NOT use `minima.skin:` or `minima.social_links:` in `_config.yml` —
   they silently no-op on 2.5.x. Social icons and dark mode are implemented manually instead (see
   below).
2. **`_includes/custom-head.html` does not work.** Minima 2.5.1 has a known bug where this
   standard theme hook is broken. Any `<head>` injection must go through a full
   `_includes/header.html` override instead (already in place — see below).
3. **`theme:` values for the other GitHub-Pages-bundled themes need the `jekyll-theme-` prefix**
   (e.g. `jekyll-theme-slate`, not `slate`) — a bare theme name will fail the build with
   "theme could not be found."
4. **`repository:` must be set in `_config.yml`** (e.g. `repository: ginopack/blog`) — without
   it, `jekyll-seo-tag` throws a fatal "No repo name found" error when building via Actions
   (the official Pages build action sets this automatically; our custom workflow does not).
5. **Plugin whitelist** only matters if we ever revert to the legacy "Deploy from a branch"
   build. Since we're on Actions now, any Jekyll plugin works, not just GitHub's whitelisted set.

## Custom theme overrides in place

All of these intentionally override Minima's built-in files. They were hand-written by
reconstructing Minima 2.5's actual markup, not auto-generated — if something looks structurally
off after a Minima gem update, compare against the upstream `jekyll/minima` repo (`2.5-stable`
branch) before assuming the override is wrong.

| File | Purpose |
|---|---|
| `_includes/header.html` | Full header override. Includes the dark mode toggle button + both its inline scripts (theme read on load, click handler). Do not move the toggle logic into `custom-head.html` — that hook is broken (see constraint #2). |
| `_includes/footer.html` | Adds a copyright line (`&copy; {{ site.time | date: "%Y" }} ...`) below Minima's default footer content. |
| `assets/main.scss` | All custom CSS/Sass lives here: color variable overrides, dark mode (`prefers-color-scheme` + manual `.theme-dark`/`.theme-light` toggle classes on `<html>`), nav spacing, 3-column post grid, video embed responsive wrapper, category badges (see "Not currently adopted" below). |

## Content conventions

- **Posts:** `_posts/YYYY-MM-DD-title.md`, front matter needs `layout: post`, `title`, `date`,
  `categories` (space-separated or YAML array — both work).
- **`future: true` is set in `_config.yml`.** Posts with a timestamp later than the actual build
  time will still publish immediately rather than silently disappearing until that time passes.
- **Pages:** `about.md`, `posts.md`, `categories.md`, `speaking-engagements.md` at repo root, all
  `layout: page`. Nav order is controlled explicitly via `header_pages:` in `_config.yml` — new
  top-level pages won't appear in the header nav unless added to that list.
- **Speaking engagements** use two Jekyll data files, not hardcoded HTML:
  `_data/speaking_upcoming.yml` and `_data/speaking_past.yml`. Add new entries at the top of the
  relevant list; move an entry from upcoming to past (adding `date` and `media_url`) once it's
  happened.
- **Social icons** (homepage + wherever else needed) use plain `<img>` tags pointing at the
  `simple-icons` CDN (`https://cdn.jsdelivr.net/npm/simple-icons@v13/icons/{name}.svg`) rather
  than Minima's `social_links` config, since that config key doesn't work on 2.5.x. This is also
  just simpler to extend — adding a new platform is one `<a><img></a>` block, no config schema to
  match.
- **Video embeds:** wrap YouTube/Vimeo iframes in `<div class="video-wrapper">...</div>` — the
  CSS in `main.scss` handles responsive 16:9 scaling.
- **Images:** live under `assets/` (e.g. `assets/profile.png`, `assets/certifications/*.png`).
  Always reference them with the `relative_url` Liquid filter, e.g.
  `{{ '/assets/profile.png' | relative_url }}` — a plain `/assets/...` path will break because of
  the non-root `baseurl`.

## Not currently adopted (built but rejected/deferred — don't reintroduce silently)

- `_layouts/post.html` override to show category badges on individual posts — was drafted but the
  user explicitly said "not interested in that for now." Don't add this back without being asked.

## Style/tone conventions for new content

- Site focus: **Business Central, the Microsoft 365 ecosystem, and AI** — keep new page copy and
  post categories aligned to these three pillars where relevant.
- Homepage (`index.md`) tone: warm/first-person ("Hey, I'm Gino"), not corporate. Keep this
  consistent if editing homepage copy.
- Color accent (`$brand-color` in `main.scss`) is currently a blue (`#0a66c2`, LinkedIn-blue-ish)
  — check current value before assuming it's Minima's default.

## Before making structural changes

- Check whether a change requires a Minima 3.0 feature — if so, flag it explicitly rather than
  silently pulling in a newer theme version, since that reopens the dependency-pinning trade-off
  described above.
- After any `_config.yml` or `assets/main.scss` change, verify the change actually reached the
  compiled output by checking `https://ginopack.github.io/blog/assets/main.css` directly (Ctrl+F
  for the expected rule) rather than trusting a hard-refresh alone — this repo has had at least
  one incident of an edit not fully landing in a commit.