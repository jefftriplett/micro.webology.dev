# micro.webology.dev

The source for [micro.webology.dev](https://micro.webology.dev), my microblog.

From December 2023 to October 2026, this blog was hosted on [Micro.blog](https://micro.blog/webology). This repo is a copy of that blog, converted to a [Hugo](https://gohugo.io) site and hosted on GitHub Pages.

## What came over from Micro.blog

- All 272 posts, from Micro.blog's Git archive, as Markdown in `content/posts/`.
- The same URLs for every post, so old links keep working.
- Micro.blog's old short URLs (such as `/2024/07/01/weeknotes-for-week.html`), as redirects to the posts.
- The same feeds at `/feed.xml` and `/feed.json`, with the same item IDs, so feed readers do not show old posts again.
- The [Outpost](https://github.com/zrwvat/theme-outpost) theme and the [Meta tags](https://github.com/microdotblog/plugin-metatags) plugin, as they were used on Micro.blog.

Micro.blog-only features, such as replies, webmentions, and Micropub posting, did not come over.

## Layout

- `content/posts/YYYY/MM/DD/slug.md` - posts
- `content/about.md`, `content/archive.md` - pages
- `static/uploads/` - images
- `themes/outpost/`, `themes/plugin-metatags/` - unmodified copies from Micro.blog (see each `SOURCE` file)
- `layouts/` - overrides for the theme, the archive page, and the feeds
- `hugo.toml` - site config

## Running locally

```shell
hugo server
```
