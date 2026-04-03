---
description: Using CSS files in the templates directory with template directives
---

# CSS Templates

CSS files placed in the `templates/` directory are processed through the Elements template engine, allowing you to use property insertion, conditionals, and other template directives within your stylesheets. This enables dynamic, component-specific styling based on user properties.

## Overview

CSS template files provide:

* **Property insertion** - Use component properties in CSS values
* **Conditional styles** - Include or exclude CSS based on conditions
* **Dynamic selectors** - Generate class names from properties
* **Per-instance processing** - Each component instance gets its own processed CSS

## File Location

```
com.yourcompany.component/
├── templates/
│   ├── index.html
│   ├── styles.css         # Component styles
│   └── include/
│       └── ...
```

## Basic Usage

CSS files can use standard CSS syntax along with Elements template directives:

```css
.component-{{id}} {
    background-color: {{backgroundColor}};
    padding: {{spacing}}px;
}

@if(showBorder)
.component-{{id}} {
    border: {{borderWidth}}px solid {{borderColor}};
    border-radius: {{borderRadius}}px;
}
@endif
```

## Property Insertion

Insert component properties directly into CSS values:

```css
/* Using color properties */
.header {
    color: {{textColor}};
    background: {{bgColor}};
}

/* Using numeric properties */
.container {
    max-width: {{maxWidth}}px;
    padding: {{paddingTop}}px {{paddingRight}}px {{paddingBottom}}px {{paddingLeft}}px;
}

/* Using string properties */
.element {
    font-family: {{fontFamily}};
    transition-duration: {{duration}}s;
}
```

## Conditional Styles

Use `@if` directives to conditionally include CSS rules:

```css
/* Show different styles based on a property */
@if(variant == "primary")
.button {
    background: blue;
    color: white;
}
@elseif(variant == "secondary")
.button {
    background: gray;
    color: white;
}
@else
.button {
    background: transparent;
    color: blue;
}
@endif
```

## Component ID Scoping

Use the unique component `{{id}}` to scope styles to specific instances:

```css
/* Each component instance gets unique styles */
.gallery-{{id}} {
    grid-template-columns: repeat({{columns}}, 1fr);
    gap: {{gap}}px;
}

.gallery-{{id}} .item {
    aspect-ratio: {{aspectRatio}};
}
```

This is particularly useful when multiple instances of the same component exist on a page with different property values.

## Examples from Core Components

### Reveal Component (Dynamic Groups)

The Reveal component uses property insertion for dynamic group styling:

```css
.group\/{{id}}:has(>[data-rwx-droparea]) {
  max-width: 100%;
}

.group\/{{id}}:not(:has(>[data-rwx-droparea])) {
  max-width: unset;
}
```

This creates group selectors scoped to each component instance.

### Responsive Styles

Generate responsive styles based on properties:

```css
@if(responsiveEnabled)
@media (max-width: 768px) {
    .component-{{id}} {
        flex-direction: column;
        padding: {{mobilePadding}}px;
    }
}
@endif

@media (min-width: 769px) {
    .component-{{id}} {
        flex-direction: row;
        padding: {{desktopPadding}}px;
    }
}
```

## Processing Behavior

### Per-Instance Processing

CSS template files are processed **once per component instance**. If you have three instances with different properties, you'll get three sets of CSS rules:

```css
/* Instance 1 with blue background */
.card-abc123 {
    background: blue;
}

/* Instance 2 with red background */
.card-def456 {
    background: red;
}

/* Instance 3 with green background */
.card-ghi789 {
    background: green;
}
```

### Inline Styles

The processed CSS is inserted inline into the page within `<style>` tags, not as external stylesheets.

## Templates vs Assets

Choose the right location for your CSS:

### Use `templates/` CSS When:

* Styles depend on component properties
* Styles need conditional logic
* Styles are instance-specific
* You need dynamic selectors or values

**Example:**

```css
.component-{{id}} {
    color: {{userSelectedColor}};
    font-size: {{fontSize}}px;
}
```

### Use `assets/` CSS When:

* Styles are static and don't change
* Styles are shared across all instances
* You want better caching and performance
* Styles are large frameworks or libraries

**Example:**

```css
/* Static base styles */
.component-base {
    display: flex;
    align-items: center;
}
```

### Combining Both

A common pattern is to use both:

```
components/
├── assets/
│   └── base.css          # Static styles for all instances
└── templates/
    └── dynamic.css       # Property-based styles per instance
```

## Best Practices

### Scope with Component ID

Always scope your CSS to prevent conflicts:

```css
/* Good - scoped to this instance */
.component-{{id}} .header {
    color: {{headerColor}};
}

/* Risky - could conflict with other components */
.header {
    color: {{headerColor}};
}
```

### Keep Templates CSS Minimal

Only include CSS that actually needs property insertion:

```css
/* Good - needs property value */
.component-{{id}} {
    background: {{bgColor}};
}

/* Better in assets/ - static value */
.component-{{id}} {
    display: flex;
    align-items: center;
}
```

### Use CSS Custom Properties

For complex styling systems, consider using CSS custom properties:

```css
.component-{{id}} {
    --primary-color: {{primaryColor}};
    --spacing: {{spacing}}px;
    --border-radius: {{borderRadius}}px;
}

.component-{{id}} .header {
    color: var(--primary-color);
    padding: var(--spacing);
    border-radius: var(--border-radius);
}
```

This keeps the template processing minimal while allowing CSS to handle the styling logic.

### Avoid Heavy Computation

Don't use template CSS for complex calculations. Do that in `hooks.js`:

```javascript
// hooks.js
const transformHook = (rw) => {
    const calculatedWidth = rw.props.baseWidth * rw.props.multiplier;
    rw.setProps({
        computedWidth: calculatedWidth
    });
};
```

```css
/* templates/styles.css */
.component-{{id}} {
    width: {{computedWidth}}px;
}
```

### Consider Performance

Remember that each component instance generates CSS. For components that might appear many times:

```css
/* This works but generates a lot of CSS for 50 instances */
.item-{{id}} {
    background: {{itemColor}};
}

/* Consider using inline styles in HTML instead */
```

In your HTML template:

```html
<div class="item" style="background: {{itemColor}}">
```

## Limitations

### No @import

CSS `@import` statements won't work in template CSS files as they're processed as inline styles:

```css
/* This won't work */
@import url('external-styles.css');

/* Put imports in assets/ instead */
```

### Limited Preprocessor Support

Template CSS files don't support Sass, Less, or other preprocessors. Use the Elements template language for logic instead.

### Browser Compatibility

Generated CSS still needs to be valid CSS. Template directives don't add vendor prefixes or polyfills:

```css
/* You still need to handle browser compatibility */
.component {
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
}
```

## Common Patterns

### Theme Integration

Integrate with theme colors:

```css
.component-{{id}} {
    color: {{themeColors.primary}};
    background: {{themeColors.surface}};
}
```

Set up in `hooks.js`:

```javascript
rw.setProps({
    themeColors: rw.theme.colors
});
```

### Utility Classes

Generate utility classes based on properties:

```css
@if(showUtilities)
.text-{{customColorName}} {
    color: {{customColor}};
}

.bg-{{customColorName}} {
    background-color: {{customColor}};
}
@endif
```

### Animation Properties

Dynamic animations based on user settings:

```css
.component-{{id}} .animated {
    animation-duration: {{duration}}s;
    animation-timing-function: {{easing}};
    animation-delay: {{delay}}s;
}

@if(animation == "fade")
.component-{{id}} .animated {
    animation-name: fadeIn;
}
@elseif(animation == "slide")
.component-{{id}} .animated {
    animation-name: slideIn;
}
@endif
```

## Related Documentation

* [Elements Language](../language/) - Template syntax reference
* [Templates Overview](./) - Understanding templates
* [Assets](../assets.md) - Static CSS files
* [Hooks.js](../hooks.js/) - Computing values for CSS
* [Properties](../properties.json/) - Defining CSS properties
