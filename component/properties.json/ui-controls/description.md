# Description

Displays a static paragraph of descriptive text. Use it for longer explanatory notes that relate to the controls around it; for short callout-style tips, use the [Information](information.md) control instead.

Like the other display controls, `description` takes no options — the text comes from the property's `title` and no `id` is needed.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Each column item controls the matching CSV column by position (1st item → 1st column).",
  "description": {}
}
```
{% endtab %}

{% tab title="Group Example" %}
```json
{
  "groups": [{
    "title": "Columns",
    "properties": [{
      "title": "Each column item controls the matching CSV column by position (1st item → 1st column).",
      "description": {}
    }, {
      "title": "Sortable",
      "id": "columnSortable",
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

### Value

Display controls don't store a value and can't be referenced in templates.
