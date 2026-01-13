---
description: globalTransforms utility function
---

# globalTransforms

Utility function for transforms.

## Signature

```javascript
globalTransforms(app, args = {})
```

## Parameters

| Parameter | Description |
|-----------|-------------|
| `app` | - |
| `args` | - |

## Usage

```javascript
function transformHook(rw) {
    const result = globalTransforms(rw);
    return { result };
}
```
