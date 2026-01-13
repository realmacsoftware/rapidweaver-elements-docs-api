---
description: globalHTMLTag utility function
---

# globalHTMLTag

Utility function for core.

## Signature

```javascript
globalHTMLTag(app, fallback = "div")
```

## Parameters

| Parameter | Description |
|-----------|-------------|
| `app` | - |
| `fallback` | - |

## Usage

```javascript
function transformHook(rw) {
    const result = globalHTMLTag(rw);
    return { result };
}
```
