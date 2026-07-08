---
description: Organize reusable template partials in the include directory
---

# Include Directory

The `templates/include/` directory is where you store reusable template partials that can be included in other template files using the `@include()` directive. This promotes code reuse, improves maintainability, and helps organize complex components.

## Overview

Include files allow you to:
- Break complex templates into smaller, manageable pieces
- Reuse common markup across multiple templates
- Keep your main templates clean and focused
- Organize related functionality into logical groups

## Directory Location

```
com.yourcompany.component/
├── templates/
│   ├── index.html
│   └── include/              # Include directory
│       ├── header.html
│       ├── footer.html
│       ├── icon.html
│       └── card.html
```

## How It Works

Include files are referenced using the `@include()` directive from any template file:

```html
<!-- templates/index.html -->
<div class="component">
    @include("header")
    
    <main>
        @dropzone("content", title: "Content")
    </main>
    
    @include("footer")
</div>
```

The include filename is specified **without the `.html` extension** and is relative to the `templates/include/` directory.

## Creating Include Files

Include files are standard HTML template files that can use the full [Elements Language](../language/README.md) syntax:

```html
<!-- templates/include/header.html -->
<header class="{{classes.header}}">
    <h1>{{title}}</h1>
    @if(showSubtitle)
        <p class="subtitle">{{subtitle}}</p>
    @endif
</header>
```

Include files have access to:
- All component properties from `properties.json`
- Data passed from `hooks.js` via `rw.setProps()`
- Built-in properties like `id`, `edit`, `preview`
- Parameters passed from the `@include()` call

## Passing Parameters

You can pass additional parameters to includes:

```html
<!-- templates/index.html -->
@include("button", label: "Click Me", style: "primary")
@include("button", label: "Cancel", style: "secondary")
```

```html
<!-- templates/include/button.html -->
<button class="btn btn-{{style}}">
    {{label}}
</button>
```

Parameters override properties with the same name within the include's scope.

## Conditional Includes

Use `@includeIf()` to conditionally include a template:

```html
@includeIf(showHeader, template: "header")

<div class="content">
    @dropzone("main", title: "Main Content")
</div>

@includeIf(showFooter, template: "footer")
```

See the [`@include` directive documentation](../language/include.md) for complete syntax details.

## Examples from Core Components

### Gallery Component

The Gallery component uses 10+ include files to organize different media types and UI elements:

```
templates/include/
├── alpine.html              # Alpine.js bindings
├── closeButton.html         # Lightbox close button
├── indicators.html          # Gallery indicators
├── lightbox.html           # Lightbox wrapper
├── lightboxMedia.html      # Media in lightbox
├── mp4.html                # MP4 video element
├── navButtons.html         # Navigation buttons
├── thumbnail.html          # Gallery thumbnail
├── vimeo.html              # Vimeo embed
└── youtube.html            # YouTube embed
```

Usage in `templates/index.html`:

```html
<div class="{{classes.wrapper}}" x-data>
    @each(image in resources)
        @include("thumbnail")
    @endeach
</div>
@includeIf(includeLightbox, template: "lightbox")
```

### Navbar Component

The Navbar component organizes desktop and mobile variations:

```
templates/include/
├── desktop_folder.html
├── desktop_item.html
├── desktop_submenu.html
├── desktop_submenu_indicator.html
├── desktop_submenu_menu.html
├── mobile_folder.html
├── mobile_item.html
├── mobile_submenu.html
├── mobile_submenu_indicator.html
├── mobile_submenu_menu.html
├── logo.html
└── title.html
```

Usage pattern:

```html
<!-- Desktop navigation -->
<nav class="desktop-nav">
    @include("logo")
    @each(item in menuItems)
        @if(item.isFolder)
            @include("desktop_folder")
        @else
            @include("desktop_item")
        @endif
    @endeach
</nav>

<!-- Mobile navigation -->
<nav class="mobile-nav">
    @include("logo")
    @each(item in menuItems)
        @if(item.isFolder)
            @include("mobile_folder")
        @else
            @include("mobile_item")
        @endif
    @endeach
</nav>
```

### Container Component

The Container component uses includes for different background types:

```
templates/include/
├── color.html          # Solid color background
├── gradient.html       # Gradient background
├── image.html          # Image background
├── mp4.html            # MP4 video background
├── overlay.html        # Background overlay
├── video.html          # Video wrapper
├── vimeo.html          # Vimeo background
└── youtube.html        # YouTube background
```

Usage with conditionals. Template `@if` accepts a single condition only, so compute the background-type booleans in `hooks.js` and use `@includeIf` for the branch. See [Combining Conditions](../language/if.md#combining-conditions).

```javascript
// hooks.js
exports.transformHook = (rw) => {
    const { backgroundType } = rw.props;
    rw.setProps({
        bgIsColor: backgroundType === "color",
        bgIsGradient: backgroundType === "gradient",
        bgIsImage: backgroundType === "image",
        bgIsVideo: backgroundType === "video",
    });
};
```

```html
<div class="container">
    @includeIf(bgIsColor, template: "color")
    @includeIf(bgIsGradient, template: "gradient")
    @includeIf(bgIsImage, template: "image")
    @includeIf(bgIsVideo, template: "video")

    @if(hasOverlay)
        @include("overlay")
    @endif
</div>
```

### Accordion Component

Simple icon inclusion with fallback:

```html
<!-- templates/index.html -->
<span class="{{classes.icon}}" aria-hidden="true">
    @include("icon")
</span>
```

```html
<!-- templates/include/icon.html -->
@includeIf(!hasAnIcon, template: "chevron")

@if(hasAnIcon)
    {{icon}}
@endif
```

```html
<!-- templates/include/chevron.html -->
<svg><!-- Default chevron icon --></svg>
```

## Organization Strategies

### By Feature

Group related includes by feature or functionality:

```
templates/include/
├── navigation/
│   ├── menu.html
│   ├── submenu.html
│   └── breadcrumb.html
├── cards/
│   ├── product-card.html
│   ├── blog-card.html
│   └── team-card.html
└── media/
    ├── image.html
    ├── video.html
    └── gallery.html
```

### By Component Part

Organize by component sections:

```
templates/include/
├── header.html
├── body.html
├── footer.html
├── sidebar.html
└── actions.html
```

### By Variation

Create variations of similar elements:

```
templates/include/
├── button-primary.html
├── button-secondary.html
├── button-outline.html
└── button-ghost.html
```

## Best Practices

### Keep Includes Focused

Each include should have a single, clear purpose:

**Good:**
```
templates/include/
├── avatar.html         # Just the avatar
├── username.html       # Just the username
└── bio.html           # Just the bio
```

**Less ideal:**
```
templates/include/
└── user-profile.html  # Everything mixed together
```

### Use Descriptive Names

Choose names that clearly indicate the include's purpose:

```
✓ product-card.html
✓ navigation-item.html
✓ social-share-buttons.html

✗ comp1.html
✗ thing.html
✗ misc.html
```

### Pass Explicit Parameters

When reusing includes with different values, pass parameters explicitly:

```html
@include("card", 
    title: item.title,
    image: item.thumbnail,
    link: item.url
)
```

This makes the template more readable and maintainable.

### Avoid Deep Nesting

While includes can include other includes, avoid deep nesting chains:

```html
<!-- Avoid this pattern -->
<!-- index.html includes section.html -->
<!-- section.html includes card.html -->
<!-- card.html includes button.html -->
<!-- button.html includes icon.html -->
```

Too many levels make the template flow hard to follow.

### Document Complex Includes

Add comments for includes that expect specific parameters:

```html
<!-- templates/include/video-player.html -->
<!-- Parameters:
     - videoUrl: The video source URL
     - posterImage: Thumbnail image URL
     - autoplay: Boolean for autoplay (optional)
-->
<video src="{{videoUrl}}" poster="{{posterImage}}" @if(autoplay)autoplay@endif>
</video>
```

## Include vs Inline Template

Choose between includes and inline templates based on your needs:

### Use Includes When:
- The template is reused across multiple files
- You want to keep files organized in separate files
- The template is complex and benefits from separation

### Use Inline Templates When:
- The template is only used once in a single file
- You want to keep related code together
- The template is simple and short

```html
<!-- Inline template example -->
@template("listItem")
    <li>{{title}}</li>
@endtemplate

<ul>
    @each(item in items)
        @include("listItem", title: item.title)
    @endeach
</ul>
```

See the [`@template` directive documentation](../language/template.md) for inline templates.

## Related Documentation

- [`@include` Directive](../language/include.md) - Complete `@include` syntax
- [`@includeIf` Directive](../language/include.md#conditional-includes) - Conditional includes
- [`@template` Directive](../language/template.md) - Inline templates
- [Elements Language](../language/README.md) - Template syntax reference
- [index.html](index.html.md) - Main template file
