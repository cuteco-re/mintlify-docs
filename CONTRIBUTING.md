# Contributing to pom Documentation

This guide explains how to add, edit, and format documentation pages for pom. The docs site is built with [Mintlify](https://mintlify.com) and uses MDX (Markdown + JSX components).

---

## Quick Reference

| Task | What to do |
|------|-----------|
| Add a new page | Create a `.mdx` file, add it to `docs.json` navigation |
| Add a new category | Add a new `group` object to `docs.json` navigation, create folder |
| Edit existing page | Edit the `.mdx` file directly |
| Add images | Place in `assets/`, reference as `/assets/filename.png` |
| Preview locally | Run `mintlify dev` (requires Node.js + `npm i -g mintlify`) |

---

## File Structure

```
docs/
├── docs.json              ← Mintlify config (navigation, theme, metadata)
├── assets/                ← Static images (logo, screenshots)
├── getting-started.mdx    ← Top-level pages
├── category-name/         ← Category folders
│   └── page-name.mdx     ← Individual pages
└── CONTRIBUTING.md        ← This file
```

---

## Adding a New Page

### 1. Create the MDX file

Create a new `.mdx` file in the appropriate folder. Every page **must** start with frontmatter:

```mdx
---
title: "Page Title"
description: "A brief description of what this page covers."
icon: "icon-name"
---

Your content here...
```

- **title**: Displayed in the sidebar and page header
- **description**: Shown below the title and used for SEO
- **icon**: A [Lucide icon](https://lucide.dev/icons) name (e.g., `shield`, `settings`, `music`)

### 2. Add to navigation

Open `docs.json` and add your page path (without `.mdx` extension) to the appropriate group:

```json
{
  "group": "Category Name",
  "pages": [
    "category/existing-page",
    "category/your-new-page"
  ]
}
```

---

## Adding a New Category

### 1. Create a folder

```
mkdir docs/your-category
```

### 2. Add a navigation group in `docs.json`

```json
{
  "group": "Your Category",
  "pages": [
    "your-category/first-page",
    "your-category/second-page"
  ]
}
```

You can also nest sub-groups with icons:

```json
{
  "group": "Your Category",
  "pages": [
    {
      "group": "Sub-Group",
      "icon": "folder",
      "pages": [
        "your-category/sub/page-one",
        "your-category/sub/page-two"
      ]
    }
  ]
}
```

---

## MDX Components

### Callout Boxes

Use these to highlight important information:

```mdx
<Info>
  Informational context the user should know.
</Info>

<Tip>
  A helpful best-practice suggestion.
</Tip>

<Warning>
  A destructive or irreversible action warning.
</Warning>
```

### Code Groups (Tabbed Examples)

Show command syntax alongside a real example:

````mdx
<CodeGroup>

```bash Syntax
,command <required> [optional]
```

```bash Example
,command @user some reason
```

</CodeGroup>
````

### Step-by-Step Guides

```mdx
<Steps>
  <Step title="First step">
    Description of what to do.
  </Step>
  <Step title="Second step">
    Description of what to do next.
  </Step>
</Steps>
```

### Collapsible Sections

```mdx
<AccordionGroup>
  <Accordion title="Section Title">
    Content that is hidden by default and expands on click.
  </Accordion>
</AccordionGroup>
```

### Card Grids (Link to other pages)

```mdx
<CardGroup cols={2}>
  <Card title="Card Title" icon="icon-name" href="/path/to/page">
    Short description of what this links to.
  </Card>
</CardGroup>
```

### Tables

Standard Markdown tables work:

```mdx
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `member`  | User mention | Yes | The member to target |
| `reason`  | Text | No | Reason for the action |
```

---

## Content Style Guide

### Tone
- Write in second person ("you can", "your server")
- Be direct and concise but thorough
- Assume the reader is a server admin, not a developer

### Page Structure
1. **Overview paragraph** (2-4 sentences explaining the feature conceptually)
2. **Setup / Getting Started** section if applicable
3. **Commands** with CodeGroup syntax + example tabs
4. **Parameters** in a table or list
5. **Tips / Warnings** where relevant
6. **Related pages** linked at the bottom or inline

### Command Documentation Format
Every command should include:
- What it does (1-2 sentences)
- Syntax with `<required>` and `[optional]` parameter notation
- A realistic example
- Parameter descriptions if not self-evident
- Required permissions (if any)
- Aliases (if any)

### Formatting Rules
- Use `,` as the prefix in all examples (it's the default)
- Wrap command names in backticks: `,ban`
- Use `<angle brackets>` for required parameters
- Use `[square brackets]` for optional parameters
- Internal links use paths without extensions: `[welcome messages](/configuration/welcome)`
- External links open in new tabs automatically

---

## Previewing Locally

```bash
npm install -g mintlify
cd docs/
mintlify dev
```

This starts a local server at `http://localhost:3000` with hot reload.

---

## Deployment

Docs are auto-deployed by Mintlify when changes are pushed to the connected GitHub repository. No manual build step is required.
