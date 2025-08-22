---
description: Include content from another template file
---

# @includeIf

Rather than wrapping your `@include` statement inside an `@if` statement, you can use the `@includeIf` helper:

```atom
// Instead of doing this:
@if(myVariable)
  @include("myTemplate")
@endif

// You can do this:
@includeIf(myVariable, template:"myTemplate")

// You can also negate the property
@includeIf(!myVariable, template:"myTemplate")
```
