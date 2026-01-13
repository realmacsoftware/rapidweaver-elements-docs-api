---
description: globalOverlayImage utility function
---

# globalOverlayImage

Utility function for effects.

## Signature

```javascript
globalOverlayImage(app, prefix)
```

## Parameters

| Parameter | Description |
|-----------|-------------|
| `app` | - |
| `prefix` | - |

## Usage

```javascript
function transformHook(rw) {
    const result = globalOverlayImage(rw);
    return { result };
}
```
