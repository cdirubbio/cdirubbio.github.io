# Chris DiRubbo's Dev Blog

Personal blog built with Jekyll and hosted on GitHub Pages.

## Local Development

```bash
# Install dependencies
bundle install

# Run locally
bundle exec jekyll serve

# Visit http://localhost:4000
```

## Writing Posts

Create new posts in `_posts/` with the format: `YYYY-MM-DD-title.md`

```markdown
---
layout: post
title: "Your Post Title"
date: 2025-03-02 12:00:00 -0800
tags: [tag1, tag2]
---

Your content here...
```

## Deployment

Push to `main` branch and GitHub Pages will automatically build and deploy.

## Customization

- Edit `_config.yml` for site settings
- Modify `assets/css/style.css` for styling
- Update `about.md` with your info
