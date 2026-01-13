---
description: globalOverlay utility function
---

# globalOverlay

Utility function for effects.

## Signature

```javascript
globalOverlay(app, isContainer = false)
```

## Parameters

| Parameter | Description |
|-----------|-------------|
| `app` | - |
| `isContainer` | - |

## Usage

```javascript
function transformHook(rw) {
    const result = globalOverlay(rw);
    return { result };
}
```
