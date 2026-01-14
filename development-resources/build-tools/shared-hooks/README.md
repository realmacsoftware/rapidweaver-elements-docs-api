---
description: JavaScript utility functions for hooks.source.js
---

# Shared Hooks

Call these functions in your `hooks.source.js`. No imports needed - they're automatically available.

## Animations

| Function | Description |
|----------|-------------|
| `globalAnimations()` | [Details](animations/global-animations) |
| `globalReveal()` | [Details](animations/global-reveal) |

## Background

| Function | Description |
|----------|-------------|
| `globalBackground()` | [Details](background/global-background) |
| `globalBgColor()` | [Details](background/global-bg-color) |
| `globalBgGradient()` | [Details](background/global-bg-gradient) |
| `globalBgImage()` | [Details](background/global-bg-image) |
| `globalBgImageFetchPriority()` | [Details](background/global-bg-image-fetch-priority) |
| `globalBgVideoThumbnail()` | [Details](background/global-bg-video-thumbnail) |

## Borders

| Function | Description |
|----------|-------------|
| `globalBorders()` | [Details](borders/global-borders) |
| `globalOutline()` | [Details](borders/global-outline) |

## Core

| Function | Description |
|----------|-------------|
| `addPrefixToTailwindClasses()` | [Details](core/add-prefix-to-tailwind-classes) |
| `advancedClasses()` | [Details](core/advanced-classes) |
| `classnames()` | [Details](core/classnames) |
| `getHoverPrefix()` | [Details](core/get-hover-prefix) |
| `globalHTMLTag()` | [Details](core/global-html-tag) |
| `injectPrefixOnDarkModeColors()` | [Details](core/inject-prefix-on-dark-mode-colors) |

## Effects

| Function | Description |
|----------|-------------|
| `bgPosition()` | [Details](effects/bg-position) |
| `globalEffects()` | [Details](effects/global-effects) |
| `globalFilters()` | [Details](effects/global-filters) |
| `globalOverlay()` | [Details](effects/global-overlay) |
| `globalOverlayColor()` | [Details](effects/global-overlay-color) |
| `globalOverlayGradient()` | [Details](effects/global-overlay-gradient) |
| `globalOverlayImage()` | [Details](effects/global-overlay-image) |

## Interactive

| Function | Description |
|----------|-------------|
| `globalFilter()` | [Details](interactive/global-filter) |
| `globalLink()` | [Details](interactive/global-link) |

## Layout

| Function | Description |
|----------|-------------|
| `getHiddenClasses()` | [Details](layout/get-hidden-classes) |
| `globalActAsGridOrFlexItem()` | [Details](layout/global-act-as-grid-or-flex-item) |
| `globalLayout()` | [Details](layout/global-layout) |

## Navigation

| Function | Description |
|----------|-------------|
| `globalMenuItem()` | [Details](navigation/global-menu-item) |
| `globalNavItems()` | [Details](navigation/global-nav-items) |
| `globalNavTitle()` | [Details](navigation/global-nav-title) |

## Sizing

| Function | Description |
|----------|-------------|
| `aspectRatioClasses()` | [Details](sizing/aspect-ratio-classes) |
| `globalSizing()` | [Details](sizing/global-sizing) |
| `globalSizingContainer()` | [Details](sizing/global-sizing-container) |
| `objectClasses()` | [Details](sizing/object-classes) |

## Spacing

| Function | Description |
|----------|-------------|
| `globalSpacing()` | [Details](spacing/global-spacing) |
| `globalSpacingMargin()` | [Details](spacing/global-spacing-margin) |
| `globalSpacingPadding()` | [Details](spacing/global-spacing-padding) |

## Transforms

| Function | Description |
|----------|-------------|
| `globalTransforms()` | [Details](transforms/global-transforms) |

## Transitions

| Function | Description |
|----------|-------------|
| `aControlWantsHover()` | [Details](transitions/a-control-wants-hover) |
| `getAlpineTransitionAttributesDesktop()` | [Details](transitions/get-alpine-transition-attributes-desktop) |
| `getAlpineTransitionAttributesMobile()` | [Details](transitions/get-alpine-transition-attributes-mobile) |
| `globalTransitions()` | [Details](transitions/global-transitions) |

## Typography

| Function | Description |
|----------|-------------|
| `globalButtonFontAndTextStyles()` | [Details](typography/global-button-font-and-text-styles) |
| `globalHeadingColor()` | [Details](typography/global-heading-color) |
| `globalHeadingTextColor()` | [Details](typography/global-heading-text-color) |
| `globalInputFontAndTextStyles()` | [Details](typography/global-input-font-and-text-styles) |
| `globalTextFontsAndTextStyles()` | [Details](typography/global-text-fonts-and-text-styles) |

## Quick Usage

```javascript
function transformHook(rw) {
    const classes = classnames()
        .add(globalSpacing(rw))
        .add(globalBackground(rw))
        .toString();

    return { classes };
}

exports.transformHook = transformHook;
```
