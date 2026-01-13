---
description: globalBgColor utility function
---

# globalBgColor

Utility function for background.

## Signature

```javascript
globalBgColor(app, args = {})
```

## Parameters

| Parameter | Description |
|-----------|-------------|
| `app` | - |
| `args` | - |

## Usage

```javascript
function transformHook(rw) {
    const result = globalBgColor(rw);
    return { result };
}
```
