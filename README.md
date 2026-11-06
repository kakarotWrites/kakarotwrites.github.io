# Kakarot security researcher site

This is a GitHub Pages/Jekyll site. The configured production URL is `https://kakarotwrites.github.io/`. Upload the contents of this folder to the `kakarotwrites.github.io` repository and enable **Settings → Pages → Deploy from a branch** using the repository's default branch and `/ (root)` folder.

For local development, install Ruby dependencies with `bundle install`, then run `bundle exec jekyll serve --livereload` and open `http://127.0.0.1:4000/`.

The layout includes responsive viewport settings, fluid headings, flexible navigation, and images that scale to their container for phones, tablets, laptops, and desktop displays. Jekyll changes the way pages are generated, not the browser’s rendering engine.

The optional background music is stored at [`assets/audio/theme.mp3`](./assets/audio/theme.mp3). It is off by default and only starts after the visitor presses the music button. Homepage section tabs use the original single-page navigation, so music continues while switching sections.

The site uses the original single-page experience in [`index.html`](./index.html) as its only public section interface:

- [`_posts/`](./_posts/) — organized Markdown writeup sources
- [`_projects/`](./_projects/) — organized project sources
- [`_layouts/`](./_layouts/) — shared page layout

Use the homepage hash tabs (`#about`, `#blog`, `#projects`, `#cv`) for navigation. This keeps the original visual design consistent and prevents duplicate section pages.

Before publishing, personalize the profile text, statistics, social links and CV content, then add `cv.pdf` if you want to publish a downloadable PDF.

## Publishing

1. Create a public repository named `kakarotwrites.github.io` under the `kakarotwrites` GitHub account.
2. Upload the source files from this folder to the repository root.
3. Do not upload `_site/` or `.jekyll-cache/`; they are generated locally and are ignored by Git.
4. In **Settings → Pages**, choose **Deploy from a branch**, select the default branch, and choose `/ (root)`.
5. Wait for the Pages deployment, then check the homepage, writeups, images, `sitemap.xml`, and `robots.txt`.

The site includes canonical, Open Graph, Twitter, `Person`, and `WebSite` metadata. Search engines may take time to crawl and index a new site, and no search or image result can be guaranteed. After deployment, submit `https://kakarotwrites.github.io/sitemap.xml` in Google Search Console.
