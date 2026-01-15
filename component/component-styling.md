---
description: A standardized approach to building components with Tailwind CSS
icon: paintbrush
---

# Component Styling

Elements uses Tailwind CSS for all component styling. Following this approach ensures consistency across all components—whether built-in, third-party, or custom-made—and makes it easier for users to build sites that are cohesive and simple to update.

**Your main goal should always be to make a component that feels native to Elements.**

## Why Tailwind?

Tailwind offers a utility-first approach to styling. Instead of writing custom CSS, you apply small, reusable utility classes directly to your HTML elements. This approach provides several benefits:

- **Consistency**: All components share the same styling vocabulary
- **No style leakage**: Styles applied via utility classes stay within each component's HTML structure
- **Optimized output**: Elements generates only the CSS your page actually uses, resulting in smaller, more efficient stylesheets
- **Theme integration**: Utility classes map directly to Theme Studio values

## Theme-Driven Design

In Elements, styling configurations—colors, fonts, spacing, and more—are controlled by the Theme and managed through the Theme Studio. Components inherit styles from the theme rather than dictating their own.

This means:

- Users can switch themes without breaking their site's design
- All components "just work" within any project
- Styling remains consistent across the entire site

For example, a Heading component might define its default font family as `heading` and font size as `3xl`. The component doesn't care what specific font or pixel size these represent—it only needs to know the values exist. The Theme Studio handles the actual values, allowing full customization while maintaining compatibility.

## Theme UI Controls

When designing your component, use Theme-based UI Controls wherever possible. These controls integrate directly with the Theme Studio, ensuring your component respects the user's theme settings.

| Control | Purpose |
|---------|---------|
| [Theme Border Width](properties.json/ui-controls/theme-border-width.md) | Border thickness values |
| [Theme Border Radius](properties.json/ui-controls/theme-border-radius.md) | Corner rounding values |
| [Theme Color](properties.json/ui-controls/theme-color.md) | Color palette selection |
| [Theme Font](properties.json/ui-controls/theme-font.md) | Font family selection |
| [Theme Spacing](properties.json/ui-controls/theme-spacing.md) | Margin and padding values |
| [Theme Shadow](properties.json/ui-controls/theme-shadow.md) | Box shadow styles |
| [Theme Text Style](properties.json/ui-controls/theme-text-style.md) | Text size presets |
| [Theme Typography](properties.json/ui-controls/theme-typography.md) | Typography class selection |

## Default Colors

All components need to work out of the box. Use semantic color names that map to Theme Studio values:

| Color | Usage |
|-------|-------|
| `brand` | Interactive elements like buttons and links |
| `text` | Text content |
| `surface` | Background colors |

## Generating Tailwind Classes with Format

Use the `format` key in your `properties.json` to transform property values into Tailwind utility classes. This keeps your templates clean and ensures proper class output.

```json
{
  "title": "Button Color",
  "id": "buttonColor",
  "format": "bg-{{value}}",
  "themeColor": {
    "default": {
      "name": "brand",
      "brightness": 500
    }
  }
}
```

In your template, reference the property directly:

```html
<button class="{{buttonColor}} px-4 py-2">Click Me</button>
```

This outputs:

```html
<button class="bg-brand-500 px-4 py-2">Click Me</button>
```

The `format` key works with any control type. See [Format](properties.json/general-structure/format.md) for more examples.

## Responsive Styling

Elements supports responsive styling out of the box. Theme controls can define different values for each breakpoint using the standard Tailwind breakpoint prefixes.

```json
{
  "title": "Heading Size",
  "id": "headingSize",
  "themeTextStyle": {
    "default": {
      "base": { "name": "2xl" },
      "md": { "name": "3xl" },
      "lg": { "name": "4xl" }
    }
  }
}
```

This outputs responsive classes that apply at each breakpoint:

```html
<h1 class="text-2xl md:text-3xl lg:text-4xl">...</h1>
```

Supported breakpoints follow Tailwind's defaults:

| Prefix | Minimum Width |
|--------|---------------|
| `base` | 0px (default) |
| `sm` | 640px |
| `md` | 768px |
| `lg` | 1024px |
| `xl` | 1280px |
| `2xl` | 1536px |

## Direct Application in Templates

Apply Tailwind utilities directly in your template files:

```html
<div class="flex items-center gap-4 p-6 bg-surface-50 rounded-lg shadow-md">
  <h2 class="text-xl font-heading text-text-900">{{title}}</h2>
  <p class="text-text-600">{{description}}</p>
</div>
```

This approach eliminates the need for scoped CSS—each component's styles are self-contained within its HTML structure.

---

## Custom CSS (When Necessary)

While Tailwind is the recommended approach, there are situations where custom CSS may be required. Use these techniques sparingly, as custom CSS will not be controllable from the Theme Studio.

### Using the Component ID for Scoping

You can scope CSS to a specific component instance using the `{{id}}` variable, which outputs a unique identifier for each component:

**In your CSS template file:**

```css
.{{id}} {
  /* styles scoped to this component instance */
}

.{{id}} .child-element {
  /* styles for child elements */
}
```

**In your HTML template:**

```html
<div class="{{id}} ...">
  <span class="child-element">...</span>
</div>
```

### BEM Naming Convention

If you need multiple custom classes, use BEM (Block Element Modifier) naming with a unique prefix to avoid conflicts:

```css
.mycomponent-card {
  /* block styles */
}

.mycomponent-card__title {
  /* element styles */
}

.mycomponent-card--featured {
  /* modifier styles */
}
```

### CSS Custom Properties

For values that need to be dynamic, use CSS custom properties set via inline styles:

```json
{
  "title": "Animation Duration",
  "id": "animationDuration",
  "format": "--animation-duration: {{value}}ms;",
  "slider": {
    "default": 300,
    "min": 100,
    "max": 1000
  }
}
```

```html
<div class="animated-element" style="{{animationDuration}}">...</div>
```

```css
.animated-element {
  transition: transform var(--animation-duration, 300ms) ease;
}
```

This approach lets users control CSS values through the inspector while keeping the styling logic in CSS.
