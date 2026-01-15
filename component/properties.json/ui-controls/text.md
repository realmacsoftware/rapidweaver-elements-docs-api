# Text

Displays a text field in the inspector.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Button Label",
  "id": "buttonLabel",
  "text": {
    "default": "Get Started",
    "subtitle": "Short call-to-action"
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
      "title": "Button Label",
      "id": "buttonLabel",
      "text": {
        "default": "Get Started",
        "subtitle": "Short call-to-action"
      }
    }]
  }]
}
```
{% endtab %}
{% endtabs %}
