---
name: Theme Block Settings
description: Repeatable schema settings used across different Shopify theme blocks to ensure consistency and speed up development.
category: Shopify Development
tags: [shopify, liquid, schema, settings]
---

# Theme Block Settings

This document tracks repeatable schema settings used across different Shopify theme blocks to ensure consistency and speed up development.

## Visibility & Responsiveness
Settings used to control block visibility and the threshold for responsive design changes.

### Mobile Visibility
- **ID**: `visible_on_mobile`
- **Type**: `checkbox`
- **Label**: "Visible on Mobile"
- **Default**: `false`

### Styles Breakpoint
- **ID**: `styles_breakpoint`
- **Type**: `number`
- **Label**: "Styles Breakpoint"
- **Default**: `1200`
- **Info**: "Defines the max-width for changes"

---

## Layout & Sizing
Settings used to constrain the dimensions of block content across different devices.

### Max-width (Desktop)
- **ID**: `max_width_desktop`
- **Type**: `range`
- **Min**: 200, **Max**: 1200, **Step**: 10, **Unit**: `px`
- **Label**: "Max-width (desktop)"
- **Default**: `1200`

### Max-width (Mobile)
- **ID**: `max_width_mobile`
- **Type**: `range`
- **Min**: 200, **Max**: 800, **Step**: 10, **Unit**: `px`
- **Label**: "Max-width (mobile)"
- **Default**: `800`

---

## Typography & SEO
Settings related to text structure and semantic HTML tags.

### Heading Tag
- **ID**: `heading_tag`
- **Type**: `select`
- **Label**: "Heading Tag"
- **Options**:
  - `h1`: "H1"
  - `h2`: "H2"
- **Default**: `h1`
