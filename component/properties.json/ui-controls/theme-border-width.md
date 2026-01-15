# Theme Border Width

Displays the Theme Studio Border Width control.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Card Border",
  "id": "cardBorderWidth",
  "themeBorderWidth": {
    "default": {
      "base": {
        "top": "1",
        "right": "1",
        "bottom": "1",
        "left": "1"
      }
    }
  }
}
```
{% endtab %}

{% tab title="Group Example" %}
```json
{
  "groups": [{
    "title": "Card Styles",
    "properties": [{
      "title": "Card Border",
      "id": "cardBorderWidth",
      "themeBorderWidth": {
        "default": {
          "base": {
            "top": "1",
            "right": "1",
            "bottom": "1",
            "left": "1"
          }
        }
      }
    }]
  }]
}
```
{% endtab %}
{% endtabs %}
