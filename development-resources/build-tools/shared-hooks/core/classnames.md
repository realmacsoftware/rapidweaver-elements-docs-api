---
description: A function to manage CSS class names with optional modifiers. /
---

# classnames

A function to manage CSS class names with optional modifiers. /

## Signature

```javascript
classnames(initialClasses = "")
```

## Parameters

| Parameter | Description |
|-----------|-------------|
| `initialClasses` | - |

## Usage

```javascript
function transformHook(rw) {
    const result = classnames();
    return { result };
}
```
