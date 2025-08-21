---
description: Component Template Folder
icon: brackets-curly
---

# Elements Language

The Elements Language (also known as the Elements API) is a lightweight yet powerful templating system built into RapidWeaver Elements. It uses \{{…\}} syntax for property insertion and offers expressive control structures like @if, all aimed at keeping your templates clean, intuitive, and logic-driven.

**Property Insertion with \{{…\}}**

Use the familiar \{{…\}} syntax to inject component or page data directly into your markup. It’s simple and intuitive. Values from properties or collections appear where needed:

```html
<h2>{{title}}</h2>
```

[**@dropzone**](dropzone.md)

A container you can drop other components into.

```html
@dropzone("extraItems")
```

[@text](text.md)

Editable text areas.

```
@text("heading")
```

[@richtext](richtext.md)

Editable styled text area.

```
@richtext("heading", default: "Hello World!")
```

[**@if**](if.md)

Control block-level rendering with clear, condition-based syntax. Elements Language uses @if, @elseif, @else, and @endif choosing when to display content based on properties.

```html
@if(condition)
  …
@elseif(otherCondition)
  …
@else
  …
@endif
```

#### [@each](each.md)

Iterate over a number of items, repeating content.

```html
@each(item in items)
  <li>{{item.title}}</li>
@endeach
```

#### [@include](include.md)

Include the content from another template file.

```html
@include("button")
```

[@portal](portal.md)

Transport content to another area of the page.

```html
@portal(pageStart)
<!-- Code here will be transported to the top of the page before the open HTML tag.-->
@endportal
```

[@template](template.md)

Define inline pieces of markup for reuse

```
@template("button")
  <button>{{label}}</button>
@endtemplate
```

Then include them

```html
@include("button", label: "Buy Now")
```

[@anchor](anchor.md)

Instruct Elements to add a linkable anchor in Elements Link Panel.

```html
<div id="@anchor("myAnchor")"></div>
```

[@raw](raw.md)

Disables template processing.

```html
@raw()
    ‹div class="text-sm text-black-600">{{message}}</div>
@endraw
```

