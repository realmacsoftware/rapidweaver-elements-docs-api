# Text Area

Displays a multiline text area in the inspector.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Description",
  "id": "cardDescription",
  "textArea": {
    "size": 5,
    "default": "Add a short paragraph that explains the feature."
  }
}
```
{% endtab %}

{% tab title="Group Example" %}
```json
{
  "groups": [{
    "title": "Card Content",
    "properties": [{
      "title": "Description",
      "id": "cardDescription",
      "textArea": {
        "size": 5,
        "default": "Add a short paragraph that explains the feature."
      }
    }]
  }]
}
```
{% endtab %}
{% endtabs %}
