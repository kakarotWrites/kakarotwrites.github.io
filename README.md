# Personal portfolio

A personal portfolio and blog built with Jekyll and hosted on GitHub Pages.

The site includes:

- About, projects, writeups, and CV sections
- Markdown articles powered by Jekyll
- Responsive layouts for desktop and mobile
- A terminal-inspired theme with light and dark modes
- Optional background music
- Article images, social links, and a downloadable CV

## How it is built

The homepage is written in HTML, CSS, and JavaScript. Articles are written in Markdown and rendered by Jekyll using the shared layouts in `_layouts/`.

The main folders are:

```text
_posts/      writeups and project articles
_projects/   project source files
_layouts/    shared Jekyll layouts
assets/      images, audio, and other static files
```

## Run it locally

Install the dependencies and start Jekyll:

```bash
bundle install
bundle exec jekyll serve --livereload
```

Open [http://127.0.0.1:4000/](http://127.0.0.1:4000/) in your browser.

## Use it for your own site

1. Fork the repository.
2. Rename it to `<your-username>.github.io`.
3. Replace the text, images, articles, CV, and social links with your own content.
4. Update the site URL and author details in `_config.yml`.
5. Enable GitHub Pages from the `main` branch and the repository root.

To add an article, create a Markdown file in `_posts/` using this format:

```text
YYYY-MM-DD-title.md
```

Add Jekyll front matter at the top of the file, then write the article below it.

## License

This project is available under the [MIT License](./LICENSE).
