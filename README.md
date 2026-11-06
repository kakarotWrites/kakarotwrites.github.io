# Rifat Al Jubayer — Personal Website

The source for [kakarotwrites.github.io](https://kakarotwrites.github.io/), a responsive Jekyll site for Rifat Al Jubayer's cybersecurity research, software projects, writeups, and CV.

## What is included

- Single-page portfolio navigation for About, Writeups, Projects, and CV
- Markdown-based security writeups and project articles
- Responsive layouts for desktop, tablet, and mobile screens
- Terminal-inspired dark theme with optional light theme
- Optional background music with browser-safe playback controls
- Profile image, downloadable CV, favicon, and social links
- SEO metadata, canonical URLs, Open Graph, Twitter cards, JSON-LD, sitemap, and robots.txt

## Project structure

```text
.
├── _config.yml              # Jekyll and site configuration
├── _layouts/                # Shared layouts for Markdown pages
├── _posts/                  # Writeups and project articles
├── _projects/               # Project source material
├── assets/
│   ├── audio/               # Optional background music
│   └── images/              # Profile, favicon, and article images
├── index.html               # Main portfolio page
├── Rifat_Al_Jubayer.pdf     # Downloadable CV
├── robots.txt               # Crawler instructions
└── Gemfile                 # Ruby/Jekyll dependencies
```

The homepage is the primary public interface. Hash routes such as `#about`, `#blog`, `#projects`, and `#cv` switch sections without creating duplicate section pages. Articles are written in Markdown and published through Jekyll.

## Local development

Requirements:

- Ruby
- Bundler
- Jekyll

Install dependencies and start the development server:

```bash
bundle install
bundle exec jekyll serve --livereload
```

Open [http://127.0.0.1:4000/](http://127.0.0.1:4000/) in a browser.

Build the site without starting a server:

```bash
bundle exec jekyll build
```

Generated files are written to `_site/`. They are not required in the repository and are excluded by `.gitignore`.

## Adding a writeup

Create a Markdown file in `_posts/` using Jekyll's date-based filename format:

```text
YYYY-MM-DD-short-title.md
```

Example front matter:

```yaml
---
layout: post
title: "A clear title"
date: 2026-12-01
categories: [writeups]
tags: [web security, research]
description: "A short description for article previews and search metadata."
---
```

Use the `project` tag for project articles. Vulnerability severity labels are reserved for security findings and should not be used for projects.

## Deployment

This site is configured as a GitHub Pages user site at:

```text
https://kakarotwrites.github.io/
```

To deploy:

1. Push the source files to the `main` branch of `kakarotWrites/kakarotwrites.github.io`.
2. Open **Settings → Pages**.
3. Select **Deploy from a branch**.
4. Choose `main` and `/ (root)`.
5. Wait for the Pages deployment to complete.

Do not commit `_site/` or `.jekyll-cache/`; GitHub Pages builds the site from the source files.

## SEO

The site publishes:

- Canonical URLs
- Open Graph and Twitter metadata
- `Person` and `WebSite` structured data
- Profile image metadata
- `sitemap.xml`
- `robots.txt`

Search engines control when pages are crawled and which title or description they display. After deployment, submit the sitemap in Google Search Console:

```text
https://kakarotwrites.github.io/sitemap.xml
```

## License

The site content, images, CV, and research writeups belong to Rifat Al Jubayer. Contact the author before reusing personal content or published evidence.
