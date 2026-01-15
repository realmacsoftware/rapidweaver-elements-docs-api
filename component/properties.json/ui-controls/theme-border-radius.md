# Theme Border Radius

Displays the Theme Studio Border Radius control.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Card Radius",
  "id": "cardRadius",
  "themeBorderRadius": {
    "default": {
      "base": {
        "topRight": "lg",
        "topLeft": "lg",
        "bottomRight": "lg",
        "bottomLeft": "lg"
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
      "title": "Card Radius",
      "id": "cardRadius",
      "themeBorderRadius": {
        "default": {
          "base": {
            "topRight": "lg",
            "topLeft": "lg",
            "bottomRight": "lg",
            "bottomLeft": "lg"
          }
        }
      }
    }]
  }]
}
```
{% endtab %}
{% endtabs %}
