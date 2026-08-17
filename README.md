# My Blog

A Jekyll blog hosted on GitHub Pages.

## Local development

1. Install Ruby (2.7+) and Bundler.
2. Install dependencies:
   ```
   bundle install
   ```
3. Run the local server:
   ```
   bundle exec jekyll serve
   ```
4. Visit http://localhost:4000

## Writing a new post

Add a file to `_posts/` named `YYYY-MM-DD-your-title.md`:

```markdown
---
layout: post
title:  "Your Title"
date:   2026-08-16 09:00:00 -0700
categories: general
---
Your post content here, in Markdown.
```

## Publishing

Push to the `main` branch. The GitHub Actions workflow in
`.github/workflows/jekyll.yml` builds and deploys automatically.

## Configuration

Edit `_config.yml` to set your site title, description, and social links.
