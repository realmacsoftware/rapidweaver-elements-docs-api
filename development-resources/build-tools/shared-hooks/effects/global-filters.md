---
description: globalFilters utility function
---

# globalFilters

Utility function for effects.

## Signature

```javascript
globalFilters(app, args = {})
```

## Parameters

| Parameter | Description |
|-----------|-------------|
| `app` | - |
| `args` | - |

## Usage

```javascript
function transformHook(rw) {
    const result = globalFilters(rw);
    return { result };
}
```
