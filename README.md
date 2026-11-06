# Rifat Al Jubayer — Jekyll Portfolio

This repository contains the source for [kakarotwrites.github.io](https://kakarotwrites.github.io/), a responsive Jekyll portfolio for cybersecurity research, software projects, technical writeups, and a CV. It can also be forked and adapted as a starting point for your own GitHub Pages portfolio.

## What this project is

The site combines a terminal-inspired single-page homepage with Markdown-powered articles. It is designed for developers, security researchers, and technical writers who want a fast personal site that is easy to edit, responsive on phones, and deployable directly from GitHub.

The included profile, CV, social links, statistics, images, and research content belong to the original author. Replace them before publishing a fork.

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

## Use this as your own site

1. Fork this repository, or use **Use this template** if enabled.
2. Rename the repository to `<your-username>.github.io` for a GitHub Pages user site.
3. Replace the personal content in [`index.html`](./index.html), [`_posts/`](./_posts/), [`_projects/`](./_projects/), and [`Rifat_Al_Jubayer.pdf`](./Rifat_Al_Jubayer.pdf).
4. Replace the profile image, article images, social URLs, and favicon in [`assets/images/`](./assets/images/).
5. Update `url`, `author`, `description`, and `image` in [`_config.yml`](./_config.yml).
6. Update the canonical, Open Graph, and structured-data URLs in [`index.html`](./index.html) if your URL differs.
7. Enable GitHub Pages from the `main` branch and `/ (root)` directory.

For a project repository rather than a user site, set `baseurl` in [`_config.yml`](./_config.yml) to `/<repository-name>` and keep links generated with Jekyll's `relative_url` filter.

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
