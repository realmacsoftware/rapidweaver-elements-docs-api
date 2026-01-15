# Divider

Display a divider between content.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "divider": {}
}
```
{% endtab %}

{% tab title="Group Example" %}
```json
{
  "groups": [{
    "title": "Card Settings",
    "properties": [{
      "title": "Content",
      "heading": {}
    }, {
      "title": "Title",
      "id": "cardTitle",
      "text": {
        "default": "New arrivals"
      }
    }, {
      "divider": {}
    }, {
      "title": "Button",
      "heading": {}
    }, {
      "title": "Button Label",
      "id": "buttonLabel",
      "text": {
        "default": "Shop now"
      }
    }]
  }]
}
```
{% endtab %}
{% endtabs %}
