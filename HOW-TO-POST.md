# How to post on the site

Everything is a small text file. Add one on GitHub (**Add file → Create new file**), click **Commit changes**, and the site updates in about a minute. New items appear on **Latest** automatically.

---

## New note (blog post)

Folder: `_posts/`
File name: `YEAR-MONTH-DAY-short-title.md`, for example `_posts/2026-11-04-sql-joins.md`

~~~markdown
---
title: SQL joins explained with one example
summary: One sentence that shows on the Latest and Notes pages.
tags: [sql]
---

Write the post here in Markdown.

## A heading

- a list
- of points

```sql
SELECT 1;
```
~~~

Tags are lowercase, one word each (use a dash for two words, like `looker-studio`). Each tag becomes a filter button on the Notes page.

---

## New project

Folder: `_projects/`
File name: `short-name.md`, for example `_projects/sales-forecast.md`

```markdown
---
title: Sales Forecast Dashboard
date: 2026-11-10
summary: One or two sentences: the business question and what you found.
metric_name: forecast_error
metric: 4.8%
trend: up
tags: [tableau, sql]
repo: https://github.com/juliocezarcarneiro/sales-forecast
live: https://link-to-dashboard
live_label: dashboard
---
```

- `trend` colours the metric: `up` is green, `down` is red, `wip` is amber (use it with `metric: in progress`).
- Add `featured: true` to show the project on the home page under Featured projects.
- `metric_name`, `metric`, `trend`, `live`, `live_label` and `featured` are optional. Delete the lines you don't need.

---

## New free book or resource

Folder: `_resources/`
File name: `short-name.md`, for example `_resources/storytelling-guide.md`

```markdown
---
title: Book title
author: Author Name
date: 2026-11-12
type: book
link: https://where-to-read-it-free
summary: One sentence on why it's worth reading.
tags: [sql, beginner]
---
```

`type` can be `book`, `course`, `tool` or anything else. Only add resources that are free and legal to read online.

---

## Other pages

- **About:** edit `about.html`
- **Home page intro:** edit `index.html` (top part only)
- **Menu, name and links:** edit `_config.yml` (`links:` section) and `_layouts/default.html`
- **Colours and fonts:** edit `assets/style.css`
- **Resume:** replace `resume-julio-carneiro.pdf` with a new file of the same name
