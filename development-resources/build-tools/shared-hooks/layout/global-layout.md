---
description: globalLayout utility function
---

# globalLayout

Utility function for layout.

## Signature

```javascript
globalLayout(app, args = {})
```

## Parameters

| Parameter | Description |
|-----------|-------------|
| `app` | - |
| `args` | - |

## Usage

```javascript
function transformHook(rw) {
    const result = globalLayout(rw);
    return { result };
}
```
