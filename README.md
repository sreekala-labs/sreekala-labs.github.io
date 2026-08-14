# sreekala-labs.github.io

Source for my field notes site — a dated, topic-tagged log of what I'm
studying. Built as a plain Jekyll site (no theme, no build step required
locally) and published automatically by GitHub Pages on every push.

**Live at:** https://sreekala-labs.github.io

## Add a new entry

1. Copy `_drafts/template.md` into `_posts/`
2. Rename it `YYYY-MM-DD-short-slug.md` (this date sets the publish date
   and the URL)
3. Fill in `title`, `topic`, `summary` in the front matter
4. Write the entry in Markdown below the front matter
5. Commit and push — no local Jekyll install needed, GitHub Pages builds
   it for you

```bash
cp _drafts/template.md "_posts/$(date +%F)-my-topic.md"
# edit the file
git add _posts/
git commit -m "Add entry: my topic"
git push
```

## Structure

```
_config.yml       site settings
_layouts/         default.html (shell), post.html (entry page)
_posts/           published entries — one file per entry
_drafts/          template.md lives here so it never publishes
assets/css/       style.css — the whole design system
index.html        homepage: entries grouped by month, filterable by topic
about.md          bio / contact
```

## First-time setup

This repo must be named exactly `sreekala-labs.github.io` for GitHub
Pages to serve it at the root domain. In repo Settings → Pages, set
Source to "Deploy from a branch," branch `main` (or `master`), folder
`/ (root)`. No further configuration needed — Jekyll builds are automatic.
