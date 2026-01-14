---
description: Display content based on dynamic conditions
---

# @if

Conditional statements in Elements allow you to control when content is displayed based on certain conditions. Using `@if`, `@elseif`, and `@else`, you can define different outcomes depending on the values of variables. This is useful for showing or hiding content based on user settings, mode (edit or preview), or other dynamic conditions.

## Syntax

```html
@if(condition)
    <!-- Content shown when condition is true -->
@endif
```

With else if and else branches:

```html
@if(condition)
    <!-- Content for first condition -->
@elseif(otherCondition)
    <!-- Content for second condition -->
@else
    <!-- Fallback content -->
@endif
```

## Block-Level Conditionals

### Basic If Statement

Display content when a switch or boolean property is true:

```html
@if(showSubtitle)
    <p class="subtitle">{{subtitle}}</p>
@endif
```

### If Not Statement

Use the `!` operator to check if something is false:

```html
@if(!edit)
    We're in preview mode or the site is Published.
@endif
```

### Multiple Conditions with Else If

Chain multiple conditions before falling back to else:

```html
@if(edit)
    We're in edit mode
@elseif(preview)
    And now in preview
@elseif(showAlternate)
    The alternate option is enabled
@else
    Default content
@endif
```

### Edit/Preview Mode Detection

Elements provides built-in `edit` and `preview` variables:

```html
@if(edit)
    Visible in Edit mode (inside Elements)
@elseif(preview)
    Visible in local preview (in Safari).
@else
    Visible when Published.
@endif
```

## Inline Conditionals

Conditionals can also be used inline within HTML attributes. This is particularly useful for dynamic class names and attribute values.

### Dynamic Class Names

Apply classes conditionally based on properties:

```html
<div class="slide @if(image::isFirst) slide-active @else slide-hidden @endif">
    <img src="{{image.src}}" />
</div>
```

### Multiple Conditional Classes

Chain multiple inline conditions for complex class logic:

```html
<li class="item @if(page.isTopLevel) top-level @elseif(page.isSecondLevel) sub-menu @elseif(page.isThirdLevel) third-level @endif">
    {{page.title}}
</li>
```

### Conditional Attributes

Add or remove attributes based on conditions:

```html
<a 
    href="{{page.url}}"
    @if(page.openInNewWindow)
    target="_blank"
    @endif
>
    {{page.title}}
</a>
```

### Conditional Image Attributes

Apply different behaviors based on settings:

```html
<img
    src="{{image.src}}"
    alt="{{image.alt}}"
    @if(imageProtection)
    oncontextmenu="return false"
    ondragstart="return false"
    @endif
    @if(imageLazyLoading)
    loading="lazy"
    @endif
    @if(wantsFetchPriority)
    fetchpriority="{{imageFetchPriority}}"
    @endif
/>
```

### Conditional Visibility Styles

Hide elements in preview/published mode:

```html
<div 
    @if(!edit)
    style="display: none"
    @endif
    class="modal-backdrop"
>
    <!-- Modal content -->
</div>
```

## Nested Conditionals

Conditionals can be nested for complex logic:

```html
@if(page.hasPages)
    <ul>
        @each(subPage in page.pages)
            @if(subPage.isVisible)
                <li>{{subPage.title}}</li>
            @endif
        @endeach
    </ul>
@endif
```

## Combining with @each

Use conditionals within loops for filtered rendering:

```html
@each(page in pages)
    @if(page.isFolder)
        @include("folder_template")
    @else
        @include("link_template")
    @endif
@endeach
```

## Common Patterns

### Fallback Content

Show a placeholder when no content exists:

```html
@if(!hasImage)
    <img src="{{sharedAssetPath}}/images/placeholder.png" alt="Placeholder" />
@else
    <img src="{{image.src}}" alt="{{image.alt}}" />
@endif
```

### Feature Toggles

Enable or disable component features:

```html
@if(showIcon)
    <span class="icon">
        @include("icon")
    </span>
@endif
```

### Conditional Includes

For conditional template includes, consider using [@includeIf](include.md#conditional-includes) for cleaner syntax:

```html
@includeIf(wantsLightbox, template: "lightbox")
```

## Best Practices

1. **Keep conditions simple** - For complex logic like string comparisons, use the [hooks file](../hooks.js/README.md) to compute boolean values and pass them to the template.

2. **Use meaningful property names** - Boolean properties should have clear names like `showIcon`, `enableLazyLoading`, or `hasImage`.

3. **Prefer @includeIf for conditional includes** - Instead of wrapping `@include` in `@if`, use `@includeIf` for cleaner templates.

4. **Only non-responsive controls work in conditionals** - Responsive controls cannot be used directly in `@if` statements.

## Related

- [@includeIf](include.md#conditional-includes) - Conditional template includes
- [Hooks File](../hooks.js/README.md) - For complex conditional logic
