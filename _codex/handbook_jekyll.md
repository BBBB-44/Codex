---
---

# Intro

**Jekyll** is a static site generator that turns simple text files (like Markdown) into a complete website. It’s tightly integrated with GitHub, which means you can use it with GitHub Pages to build blogs, documentation sites, or portfolios without needing a backend server.  

Instead of writing raw HTML for every page, you use templates, layouts, and data files—Jekyll assembles everything into a fast, static site.  

GitHub Pages supports Jekyll out of the box, so no extra setup is needed for basic use.

---

# Front Matter

Every post requires **YAML front matter** (e.g., `layout: post`) to be processed.

The front matter must be the first thing in the file and must take the form of valid YAML set between triple-dashed lines.

## Example

```yaml
---
layout: post
title: Blogging Like a Hacker
---
````

## Minimal front matter (most common)
Just use this:
---
---
It’s the smallest possible “activation switch.”

Using front matter allows you to specify configuration in pages and posts for your site. You can define things like:

* Default layout
* Custom titles
* Specific date/time for posts

Often, you’ll find yourself repeating configuration options (like layouts, categories, or authors). Instead of duplicating this in every file, Jekyll lets you define **site-wide defaults**.

---

# Site-Wide Defaults

You can configure defaults in the `_config.yml` file using the `defaults` key.

This key holds an array of scope/value pairs that define default settings for files.

## Example

```yaml
defaults:
  -
    scope:
      path: "" # applies to all files
    values:
      layout: "default"
```

---

# How to Create a Dynamic File Listing

Even though Jekyll is “static,” it can generate dynamic-looking content using templates and data.

---

## Option A: Using Posts

Jekyll post listings are created by iterating over `site.posts` using Liquid templating.

### Requirements

* Posts must be in a `_posts/` folder
* File names must follow: `YYYY-MM-DD-title.md`

### Basic Post Listing

Add this to your `index.html`:

```liquid
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      <span>{{ post.date | date: "%Y-%m-%d" }}</span>
    </li>
  {% endfor %}
</ul>
```

---

## Option B: Using a Custom Collection

### Step 1: Add to `_config.yml`

```yaml
collections:
  projects:   <!-- notice how you dont need to write the "_" appearing in the folder name -->
    output: true
```

### Step 2: Create files in `_projects/` # must start with "_" 

```yaml
---
title: My Project
---
Project description here.
```

### Step 3: Display the collection

```liquid
<ul>
  {% for project in site.projects %}
    <li>{{ project.title }}</li>
  {% endfor %}
</ul>
```
