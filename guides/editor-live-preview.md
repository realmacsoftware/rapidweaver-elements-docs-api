---
description: Run Three.js and other ES modules live on the editing canvas
---

# Editor Live Preview

Page JavaScript — Alpine factories, `<script>` tags, pack `bodyEnd` loaders — does not execute on the editing canvas. The canvas is a React document that sanitizes HTML and never runs those scripts. Use the **live-preview contract** when a component needs a real animation (Three.js, or any other ES module) to play while the user edits.

The editor hosts a special tag, `rwlivepreview`. It dynamically imports a module you provide, calls `mount`, and owns disposal when the node is removed or the module changes. Inspector tweaks update the `props` attribute; the host calls `update` instead of remounting.

## The Module Contract

A live-preview module is an ES module that exports `mount`:

```js
import * as THREE from 'three'; // resolved via the editor import map

export function mount(el, props) {
    // el: empty host div owned by the module; props: parsed JSON object
    return {
        update(nextProps) {},      // optional — called on property changes; if absent, host disposes + remounts
        setVisible(isVisible) {},  // optional — host calls via IntersectionObserver; pause rAF here
        dispose() {}               // called on unmount/remount; cancel rAF, renderer.dispose()
    };
}
```

- `el` is an empty `div`. The module owns everything inside it.
- `props` is the decoded JSON object from the tag's `props` attribute.
- `update` is optional. Implement it for colour/speed tweaks so the scene does not flicker. If you omit it, the host disposes and remounts on every property change.
- `setVisible` is optional. Pause `requestAnimationFrame` when `isVisible` is false. Browsers cap WebGL contexts; pausing off-screen scenes keeps a page of several Three.js components from exhausting that cap.
- `dispose` must cancel animation frames, disconnect observers, and call `renderer.dispose()` (and `forceContextLoss()` for Three.js).

The editor wraps every call in try/catch. A broken module logs a warning and leaves the host empty — it must not take the canvas down.

## Dev Pack Components

Emit the tag in edit mode only. Encode props with `encodeURIComponent(JSON.stringify(...))` so quotes survive the HTML attribute.

```javascript
// hooks.source.js
rw.setProps({
    isEdit: rw.project.mode === "edit",
    assetPath: rw.component.assetPath,
    livePreviewProps: encodeURIComponent(JSON.stringify(config)),
});
```

```html
@if(isEdit)
<rwlivepreview module="{{assetPath}}/editor-preview.module.js" props="{{livePreviewProps}}" class="absolute inset-0 w-full h-full"></rwlivepreview>
@endif
```

Put the module at `assets/page/editor-preview.module.js` (the only supported component-asset subfolder). Import Three.js with the bare specifier `three` — the editor import map resolves it to a single shared copy. Do not import the pack-vendored Three.js file from this module; published pages cannot reach editor URLs, and this file is editor-only.

The published path stays as it is today: Alpine (or your own script) plus a pack-level Three.js loader. The live-preview module is not shipped into the visitor page unless you also reference it from a non-edit template.

Attribute names are lowercase (`module`, `props`, `class`). The tag name must be alphanumeric with no hyphens: `rwlivepreview`.

## Custom Components

Custom components have no URL-addressable asset root. Omit the `module` attribute. The host takes the component's JavaScript area (already delivered to the editor) and imports it as a Blob ES module.

Guard the export so the published page never sees `export`:

```
@if(isEdit)
import * as THREE from 'three';

export function mount(el, props) {
    const renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
    el.appendChild(renderer.domElement);
    // …
    return {
        update(next) {},
        setVisible(visible) {},
        dispose() {
            renderer.dispose();
            renderer.forceContextLoss();
        }
    };
}
@endif
@if(!isEdit)
/* published-page script (Alpine etc.) */
@endif
```

Template:

```html
@if(isEdit)
<rwlivepreview props="{{livePreviewProps}}" class="absolute inset-0 w-full h-full"></rwlivepreview>
@endif
```

The host rewrites the bare specifier `three` to the editor's vendored module before creating the Blob. Other libraries are not rewritten; vendor them yourself or use a `module` URL from a Dev Pack.

## Shared Three.js

The editor serves Three.js r165 at `/assets/vendor/three/three.module.min.js` and maps the specifier `three` to that URL. URL-loaded pack modules resolve the specifier through the import map. Blob-loaded custom-component modules have the specifier rewritten to the same absolute URL. Either path shares one module instance.

## Limitations

- Ordinary page scripts still do not run on the canvas. Alpine, GSAP, and pack `bodyEnd` loaders remain preview/publish-only.
- Editor UI-dev mode (`localhost:8080`) serves `/assets/vendor/...` from Vite, but pack-asset module URLs (`/<uuid>/<absolute-path>`) hit Vite and 404. Use a normal editor session to test Dev Pack live previews.
- Do not mount more live WebGL scenes than you need. Implement `setVisible` and dispose promptly.

## Related Documentation

* [Designing the Edit-Mode Experience](edit-mode-experience.md)
* [Integrating JavaScript Libraries](integrating-javascript-libraries.md)
* [Interactive Components with Alpine.js](interactive-components-with-alpine.md)
* [Assets](../component/assets.md)
