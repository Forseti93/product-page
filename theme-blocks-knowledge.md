# Shopify Theme Blocks Knowledge

Theme blocks are a modular way to build Shopify themes, introduced to enhance reusability and merchant flexibility. Unlike section blocks, which are scoped to a single section, theme blocks are defined in the `/blocks` directory and can be used across multiple sections.

## Key Concepts

### 1. Definition
- Files are stored in the `/blocks` directory (e.g., `blocks/my-block.liquid`).
- Every theme block must contain a `{% schema %}` tag.
- Blocks can be nested using `{% content_for 'blocks' %}`.

### 2. Usage in Sections
To allow theme blocks in a section, add the following to the section's schema:
```json
{
  "blocks": [
    { "type": "@theme" }
  ]
}
```
In the section's Liquid code, render the blocks using:
```liquid
{% content_for 'blocks' %}
```

### 3. Static Blocks
Blocks can be rendered statically within a section or another block:
```liquid
{% content_for 'block', type: 'block-name', id: 'unique-id' %}
```
Note: Statically rendered blocks require a `{% doc %}` tag in the block file.

### 4. CSS and JavaScript
- Use `{% stylesheet %}` and `{% javascript %}` tags for component-specific logic.
- Liquid is **not** rendered inside these tags. Use CSS variables defined in the HTML `style` attribute for dynamic values.
- Alternatively, move styles to `assets/` and link them using `{{ 'filename.css' | asset_url | stylesheet_tag }}`.

### 5. Schema Best Practices
- Use `t:` keys for localization.
- Use `settings` for customizable attributes.
- Use `presets` to make the block available in the theme editor's "Add block" menu.

## Migration Checklist (Section Blocks to Theme Blocks)
1. Extract block Liquid code to new files in `/blocks`.
2. Extract block schema to the new files.
3. Update the section schema to use `{ "type": "@theme" }`.
4. Update the section Liquid to use `{% content_for 'blocks' %}`.
5. Move shared styles to `assets/` and link them.
