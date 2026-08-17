---
layout: post
title:  "Here is another!"
date:   2026-08-16 10:00:00 -0700
categories: Testing
---

This post exists purely to stress-test the blog's **Markdown rendering** and *typography* before I start writing real content.

## Headings

### A smaller heading
#### An even smaller heading

## Text formatting

Here's a sentence with **bold text**, *italic text*, ***bold italic text***, ~~strikethrough~~, and `inline code`.

You can also mix them: this is **bold with `inline code` inside it**.

## Lists

An unordered list:

- First item
- Second item
  - Nested item one
  - Nested item two
- Third item

An ordered list:

1. Preheat the oven
2. Mix the ingredients
3. Bake for 25 minutes
   1. Check at the 20 minute mark
   2. Rotate the pan if needed

A task list:

- [x] Set up the repository
- [x] Fix the baseurl config
- [ ] Write a real first post
- [ ] Customize the theme

## Blockquotes

> Simplicity is the ultimate sophistication.
>
> — Often attributed to Leonardo da Vinci

Nested blockquotes:

> This is the outer quote.
>
> > This is a nested quote inside it.

## Code blocks

Inline code looks like `this`. A fenced code block with syntax highlighting:

```python
def fibonacci(n):
    a, b = 0, 1
    for _ in range(n):
        a, b = b, a + b
    return a

print(fibonacci(10))
```

```bash
bundle exec jekyll serve --livereload
```

## Links and images

Here's a [link to the Jekyll docs](https://jekyllrb.com/docs/), and here's a bare URL: <https://github.com>.

Here's an example image (swap the path for a real one in `/assets`):

![A placeholder alt description](/assets/example-image.jpg)

## Tables

| Feature       | Supported | Notes                     |
|---------------|:---------:|----------------------------|
| Headings      |    ✅     | H1–H6                      |
| Tables        |    ✅     | GitHub-flavored Markdown   |
| Footnotes     |    ✅     | See below                  |
| Emoji shortcodes | ⚠️     | Depends on theme/plugin    |

## Horizontal rule

Above this line is one section, below is another.

---

## Footnotes

Here's a sentence with a footnote.[^1] And another one.[^2]

[^1]: This is the first footnote's content.
[^2]: This is the second footnote's content, and it can span multiple sentences if needed.

## Definition-style list (via HTML)

<dl>
  <dt>Jekyll</dt>
  <dd>A static site generator written in Ruby.</dd>
  <dt>Front matter</dt>
  <dd>The YAML block at the top of a post that sets its layout, title, and date.</dd>
</dl>

## Wrap-up

If all of the above rendered with proper spacing, list indentation, code highlighting, and table borders, the layout is working as expected. Time to delete this post and write something real.
