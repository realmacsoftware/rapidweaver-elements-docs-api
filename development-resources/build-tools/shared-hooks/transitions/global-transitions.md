---
description: globalTransitions utility function
---

# globalTransitions

Utility function for transitions.

## Signature

```javascript
globalTransitions(app, alwaysWantsHover = false)
```

## Parameters

| Parameter | Description |
|-----------|-------------|
| `app` | - |
| `alwaysWantsHover` | - |

## Usage

```javascript
function transformHook(rw) {
    const result = globalTransitions(rw);
    return { result };
}
```
