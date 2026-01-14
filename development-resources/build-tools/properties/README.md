---
description: Reusable value definitions for controls
---

# Properties

Use these in your controls with `"use": "Name"` to get pre-defined option lists.

| use | Description | Default |
|-----|-------------|---------|
| `BackgroundType` | [View details](background-type) | - |
| `ButtonSize` | [View details](button-size) | `md` |
| `ContainerWidths` | [View details](container-widths) | `full` |
| `ContainerHeights` | [View details](container-heights) | `full` |
| `FontWeight` | [View details](font-weight) | `400` |
| `GradientDirection` | [View details](gradient-direction) | `bg-gradient-to-b` |
| `LetterSpacing` | [View details](letter-spacing) | `normal` |
| `LineHeight` | [View details](line-height) | `normal` |
| `RevealAnimations` | [View details](reveal-animations) | `fade` |
| `Slider` | [View details](slider) | - |
| `TextAlign` | [View details](text-align) | `text-left` |
| `TransformOrigins` | [View details](transform-origins) | `center` |
| `TransitionNames` | [View details](transition-names) | `dim` |

## Usage

```json
{
  "title": "Weight",
  "id": "fontWeight",
  "select": {
    "use": "FontWeight"
  }
}
```

The property's `items` and `default` will be merged into your control definition.
