---
description: getAlpineTransitionAttributesDesktop utility function
---

# getAlpineTransitionAttributesDesktop

Utility function for transitions.

## Signature

```javascript
getAlpineTransitionAttributesDesktop(transitionName)
```

## Parameters

| Parameter | Description |
|-----------|-------------|
| `transitionName` | - |

## Usage

```javascript
function transformHook(rw) {
    const result = getAlpineTransitionAttributesDesktop();
    return { result };
}
```
