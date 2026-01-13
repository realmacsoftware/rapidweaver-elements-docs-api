---
description: globalBgImageFetchPriority utility function
---

# globalBgImageFetchPriority

Utility function for background.

## Signature

```javascript
globalBgImageFetchPriority(rw)
```

## Parameters

| Parameter | Description |
|-----------|-------------|
| `rw` | - |

## Usage

```javascript
function transformHook(rw) {
    const result = globalBgImageFetchPriority(rw);
    return { result };
}
```
