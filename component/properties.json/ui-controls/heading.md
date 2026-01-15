# Heading

Displays a heading in the inspector interface.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Typography",
  "heading": {}
}
```
{% endtab %}

{% tab title="Group Example" %}
```json
{
  "groups": [{
    "title": "Text Styles",
    "properties": [{
      "title": "Typography",
      "heading": {}
    }, {
      "title": "Text Style",
      "id": "textStyle",
      "themeTextStyle": {
        "default": {
          "base": {
            "name": "lg"
          }
        }
      }
    }]
  }]
}
```
{% endtab %}
{% endtabs %}
