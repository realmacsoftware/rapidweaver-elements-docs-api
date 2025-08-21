---
icon: sliders-simple
---

# Properties

Component properties (User Interface controls) are defined in the `properties.json` file. [Browse the UI Control docs](ui-controls/) for a full list of available controls and code samples.

An example `properties.json` file that creates a single group named "Slider Example" with one slider control.

```
{
    "groups": [{
        "title": "Slider Example",
        "properties": [{
            "title": "Contrast",
            "id": "contrast",
            "format": "{{value}}%",
            "slider": {
                "default": 50,
                "min": 0,
                "max": 100,
                "units": "%",
                "round": true
            }
        }]
    }]
}

```
