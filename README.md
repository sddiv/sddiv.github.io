# Divyendu Thinks

Personal blog exploring the intersection of AI, technology, and human problem-solving.

Live at: https://sddiv.github.io

## Local Development

### Prerequisites

- Ruby
- Bundler (`gem install bundler`)

### Setup

```bash
bundle install
```

### Run locally

```bash
bundle exec jekyll serve
```

Site will be available at `http://localhost:4000`.

## Project Structure

```
_config.yaml    # Site configuration
_layouts/       # Page templates
_posts/         # Blog posts (Markdown)
assets/         # CSS and static assets
index.md        # Home page
about-me.html   # About page
archive.md      # Post archive
disclaimers.md  # Disclaimers page
```

## Writing Posts

Add a new Markdown file to `_posts/` with the naming convention:

```
YYYY-MM-DD-title-of-post.md
```

Include front matter at the top:

```yaml
---
layout: post
title: "Your Post Title"
date: YYYY-MM-DD
---
```

Use `<!--more-->` to define the excerpt break point.

## Built With

- [Jekyll](https://jekyllrb.com/) with the [Minimal](https://github.com/pages-themes/minimal) theme
- Hosted on [GitHub Pages](https://pages.github.com/)
