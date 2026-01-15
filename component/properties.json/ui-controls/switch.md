# Switch

Displays a switch, similar to a checkbox in functionality.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Show Icon",
  "id": "showIcon",
  "responsive": false,
  "switch": {
    "default": true
  }
}
```
{% endtab %}

{% tab title="Group Example" %}
```json
{
  "groups": [{
    "title": "Button",
    "properties": [{
      "title": "Show Icon",
      "id": "showIcon",
      "responsive": false,
      "switch": {
        "default": true
      }
    }]
  }]
}
```
{% endtab %}
{% endtabs %}

The following example returns a true or false value. Note that `responsive` should be `false`.

```json
{
  "groups": [{
    "title": "Content",
    "properties": [{
      "title": "Show Badge",
      "id": "showBadge",
      "responsive": false,
      "switch": {
        "default": false
      }
    }]
  }]
}
```

The following example returns a string value instead of true or false. Note that `responsive` should be `false`.

```json
{
  "groups": [{
    "title": "Pricing",
    "properties": [{
      "title": "Price Label",
      "id": "priceLabel",
      "responsive": false,
      "switch": {
        "trueValue": "From $99",
        "falseValue": "From $129",
        "default": true
      }
    }]
  }]
}
```

To display this value in a template file, use `{{priceLabel}}`.

### Responsive

When using a switch responsively, trueValue and falseValue should be set to a Tailwind class name. You'll then receive a list of Tailwind classes within your template, prefixed for each breakpoint as necessary.

```json
{
  "groups": [{
    "title": "Layout",
    "properties": [{
      "title": "Show Description",
      "id": "showDescription",
      "responsive": true,
      "switch": {
        "trueValue": "block",
        "falseValue": "hidden",
        "default": {
          "base": false,
          "md": true
        }
      }
    }]
  }]
}
```

### Template

In the Template file you can do the following to display different html based on the value.

```html
@if(showDescription)
    <div class="p-sm text-lg text-center text-primary-500">I'm True!</div>
@else
    <div class="p-sm text-lg text-center text-primary-500">I'm False!</div>
@endif
```
