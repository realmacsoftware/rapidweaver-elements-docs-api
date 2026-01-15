# Information

Display some informational static text.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "information": {},
  "title": "Tip: Use short, action-oriented labels for buttons."
}
```
{% endtab %}

{% tab title="Group Example" %}
```json
{
  "groups": [{
    "title": "Button Settings",
    "properties": [{
      "information": {},
      "title": "Tip: Use short, action-oriented labels for buttons."
    }, {
      "title": "Button Label",
      "id": "buttonLabel",
      "text": {
        "default": "Get Started"
      }
    }]
  }]
}
```
{% endtab %}
{% endtabs %}
