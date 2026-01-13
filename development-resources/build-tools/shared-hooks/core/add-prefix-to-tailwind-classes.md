---
description: Adds a prefix (like "hover:" or "group-hover:") to Tailwind classes. Handles classes that already have modifiers by inserting the prefix after the existing modifier. /
---

# addPrefixToTailwindClasses

Adds a prefix (like "hover:" or "group-hover:") to Tailwind classes. Handles classes that already have modifiers by inserting the prefix after the existing modifier. /

## Signature

```javascript
addPrefixToTailwindClasses(classString, prefix)
```

## Parameters

| Parameter | Description |
|-----------|-------------|
| `classString` | - |
| `prefix` | - |

## Usage

```javascript
function transformHook(rw) {
    const result = addPrefixToTailwindClasses();
    return { result };
}
```
