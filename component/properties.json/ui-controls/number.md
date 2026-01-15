# Number

Displays a number field with a stepper.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Max Items",
  "id": "maxItems",
  "number": {
    "default": 6,
    "subtitle": "Number of cards to show"
  }
}
```
{% endtab %}

{% tab title="Group Example" %}
```json
{
  "groups": [{
    "title": "Collection Settings",
    "properties": [{
      "title": "Max Items",
      "id": "maxItems",
      "number": {
        "default": 6,
        "subtitle": "Number of cards to show"
      }
    }]
  }]
}
```
{% endtab %}
{% endtabs %}
