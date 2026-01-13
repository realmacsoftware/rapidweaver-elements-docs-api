---
description: globalOverlayColor utility function
---

# globalOverlayColor

Utility function for effects.

## Signature

```javascript
globalOverlayColor(app, prefix)
```

## Parameters

| Parameter | Description |
|-----------|-------------|
| `app` | - |
| `prefix` | - |

## Usage

```javascript
function transformHook(rw) {
    const result = globalOverlayColor(rw);
    return { result };
}
```
