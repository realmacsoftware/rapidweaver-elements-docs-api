---
description: injectPrefixOnDarkModeColors utility function
---

# injectPrefixOnDarkModeColors

Utility function for core.

## Signature

```javascript
injectPrefixOnDarkModeColors(prefix, classes)
```

## Parameters

| Parameter | Description |
|-----------|-------------|
| `prefix` | - |
| `classes` | - |

## Usage

```javascript
function transformHook(rw) {
    const result = injectPrefixOnDarkModeColors();
    return { result };
}
```
