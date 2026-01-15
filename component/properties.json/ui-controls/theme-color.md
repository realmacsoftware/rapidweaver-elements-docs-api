# Theme Color

Displays the Theme Studio Color control.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Button Color",
  "id": "buttonColor",
  "format": "bg-{{value}}",
  "themeColor": {
    "default": {
      "name": "brand",
      "brightness": 500
    }
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
      "title": "Button Color",
      "id": "buttonColor",
      "format": "bg-{{value}}",
      "themeColor": {
        "default": {
          "name": "brand",
          "brightness": 500
        }
      }
    }]
  }]
}
```
{% endtab %}
{% endtabs %}

For consistency and integration with the Theme Studio in RapidWeaver Elements, use the `themeColor` attribute to specify all color options for your elements. This ensures that the color settings are centrally managed and adaptable to theme changes.

**Usage of `themeColor`:**

* **default**: Sets the initial or fallback color and brightness. In this case, the default color is brand with a brightness value of 500.

**Output Example:** [The `format` key](../general-structure/format.md) controls the output format of the `buttonColor` property. In your template files, referencing `{{buttonColor}}` with the example configuration above would output: `bg-brand-500`.

### Setting Light and Dark mode colours

```json
"themeColor": {
  "default": {
    "name": "surface",
    "brightness": 800,
    "darkName": "surface",
    "darkBrightness": 50
  }
}
```

