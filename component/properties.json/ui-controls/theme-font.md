# Theme Font

Displays the Theme Studio Font control.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Headline Font",
  "id": "headlineFont",
  "themeFont": {
    "default": {
      "base": { "name": "heading" },
      "sm": { "name": "heading" },
      "md": { "name": "display" }
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
      "title": "Headline Font",
      "id": "headlineFont",
      "themeFont": {
        "default": {
          "base": { "name": "heading" },
          "sm": { "name": "heading" },
          "md": { "name": "display" }
        }
      }
    }]
  }]
}
```
{% endtab %}
{% endtabs %}

For effective theme integration in RapidWeaver Elements, it is recommended to use the `themeFont` attribute to define all font family settings for your elements. This approach ensures that font preferences are coordinated with the overall theme settings, providing a consistent user experience.

Here’s a structured example for defining a font property:

**Output Example:** In your template files, referencing `{{headlineFont}}` with the example configuration above would output: `font-heading sm:font-heading md:font-display`.
