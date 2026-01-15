# General Structure

All properties have the same general structure using the following object keys.

<table><thead><tr><th width="156">Key</th><th width="110">Value</th><th>Notes</th></tr></thead><tbody><tr><td><code>title</code></td><td>string</td><td>See <a href="title.md">Title</a> for more information</td></tr><tr><td><code>id</code></td><td>string</td><td>See <a href="id.md">ID</a> for more information</td></tr><tr><td><code>format</code></td><td>string</td><td>See <a href="format.md">Format</a> for more information</td></tr><tr><td><code>visible</code></td><td>string</td><td>See <a href="visible.md">Visible</a> for more information</td></tr><tr><td><code>enabled</code></td><td>string</td><td>See <a href="enabled.md">Enabled</a> for more information</td></tr><tr><td><code>responsive</code></td><td>boolean</td><td>See <a href="responsive.md">Responsive</a> for more information</td></tr></tbody></table>

### Code Example

This example shows a real-world control for a hero overlay. The slider only appears when the overlay is enabled and it outputs a Tailwind class.

```json
{
  "title": "Overlay Opacity",
  "id": "overlayOpacity",
  "format": "bg-opacity-[{{value}}%]",
  "visible": "showOverlay == true",
  "enabled": "overlayStyle != 'none'",
  "responsive": false,
  "slider": {
    "default": 60,
    "min": 0,
    "max": 100,
    "round": true,
    "units": "%"
  }
}
```
