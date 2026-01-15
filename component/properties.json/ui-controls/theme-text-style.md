# Theme Text Style

Displays the Theme Studio Text Style control.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Heading Size",
  "id": "headingTextStyle",
  "themeTextStyle": {
    "default": {
      "base": {
        "name": "3xl"
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
    "title": "Typography",
    "properties": [{
      "title": "Heading Size",
      "id": "headingTextStyle",
      "themeTextStyle": {
        "default": {
          "base": {
            "name": "3xl"
          }
        }
      }
    }]
  }]
}
```
{% endtab %}
{% endtabs %}
