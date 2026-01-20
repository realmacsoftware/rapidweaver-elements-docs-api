# Resource

Displays a resource dropwell that accepts all file types.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Image",
  "id": "image",
  "resource": {}
}
```
{% endtab %}

{% tab title="Group Example" %}
```json
{
  "groups": [{
    "title": "Content",
    "icon": "photo",
    "properties": [{
      "title": "Image",
      "id": "image",
      "resource": {}
    }]
  }]
}
```
{% endtab %}
{% endtabs %}

## Restricting File Types

You can restrict the file types allowed in a dropwell using the `types` property.

```json
"resource": {
    "types": ["svg"]
}
```

Support for multiple file types can be added using an array:

```json
"resource": {
    "types": ["image", "svg"]
}
```

## Using Resources in Templates

### Resource Properties

When you define a resource control, you can access its properties in your template:

| Property | Description |
|----------|-------------|
| `{{resource.image}}` | The URL/path to the image |
| `{{resource.path}}` | The file path (use for non-image files like video, PDF) |
| `{{resource.width}}` | Original width in pixels (images only) |
| `{{resource.height}}` | Original height in pixels (images only) |
| `{{resource.aspect}}` | Aspect ratio, e.g. `16/9` (images only) |

### Displaying an Image

```html
<img
  src="{{photo.image}}"
  alt="{{altText}}"
  width="{{photo.width}}"
  height="{{photo.height}}"
/>
```

### Displaying a Video

For non-image resources like video files, use the `.path` property:

```html
<video controls>
  <source src="{{myVideo.path}}" type="video/mp4">
</video>
```

### Checking if a Resource Exists

Use a conditional to handle cases where no resource has been selected:

```html
@if(photo.image)
  <img src="{{photo.image}}" alt="{{altText}}" />
@else
  <p>No image selected</p>
@endif
```

## Resource Dropzones

You can enable drag-and-drop directly onto an element in the editor by adding the `rwResourceDropZone` attribute. The value should match the `id` of your resource control.

```html
<div rwResourceDropZone="photo">
  @if(photo.image)
    <img src="{{photo.image}}" alt="{{altText}}" />
  @else
    <p>Drop an image here</p>
  @endif
</div>
```

This can also be set via `hooks.js` using `rw.setRootElement()`:

```javascript
rw.setRootElement({
  as: "div",
  class: "image-wrapper",
  args: {
    rwResourceDropZone: "photo"
  }
})
```

## Complete Example

**properties.json:**

```json
{
  "groups": [{
    "title": "Image",
    "icon": "photo",
    "properties": [{
      "title": "Photo",
      "id": "photo",
      "resource": {}
    }, {
      "title": "Alt Text",
      "id": "altText",
      "text": { "default": "" }
    }]
  }]
}
```

**templates/index.html:**

```html
<div rwResourceDropZone="photo">
  @if(photo.image)
    <img
      src="{{photo.image}}"
      alt="{{altText}}"
      width="{{photo.width}}"
      height="{{photo.height}}"
    />
  @else
    <p>Drop an image here</p>
  @endif
</div>
```

