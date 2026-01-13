---
description: globalBackground utility function
---

# globalBackground

Utility function for background.

## Signature

```javascript
globalBackground(app, args = {})
```

## Parameters

| Parameter | Description |
|-----------|-------------|
| `app` | - |
| `args` | - |

## Usage

```javascript
function transformHook(rw) {
    const result = globalBackground(rw);
    return { result };
}
```
