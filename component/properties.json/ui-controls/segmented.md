# Segmented

Display a segmented control.&#x20;

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Button Style",
  "id": "buttonStyle",
  "segmented": {
    "default": "solid",
    "items": [{
      "value": "solid",
      "icon": "rectangle.fill"
    }, {
      "value": "outline",
      "icon": "rectangle"
    }, {
      "value": "ghost",
      "icon": "square.dashed"
    }]
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
      "title": "Button Style",
      "id": "buttonStyle",
      "segmented": {
        "default": "solid",
        "items": [{
          "value": "solid",
          "icon": "rectangle.fill"
        }, {
          "value": "outline",
          "icon": "rectangle"
        }, {
          "value": "ghost",
          "icon": "square.dashed"
        }]
      }
    }]
  }]
}
```
{% endtab %}
{% endtabs %}

You can also use the following title key to display text instead of icons.

```json
{
  "groups": [{
    "title": "Layout",
    "properties": [{
      "title": "Content Alignment",
      "id": "contentAlignment",
      "segmented": {
        "items": [{
          "value": "text-left",
          "title": "Left"
        }, {
          "value": "text-center",
          "title": "Center",
          "default": true
        }, {
          "value": "text-right",
          "title": "Right"
        }]
      }
    }]
  }]
}
```

