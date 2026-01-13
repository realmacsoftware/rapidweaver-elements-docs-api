---
description: globalEffects utility function
---

# globalEffects

Utility function for effects.

## Signature

```javascript
globalEffects(app, args = {})
```

## Parameters

| Parameter | Description |
|-----------|-------------|
| `app` | - |
| `args` | - |

## Usage

```javascript
function transformHook(rw) {
    const result = globalEffects(rw);
    return { result };
}
```
