---
description: Using JavaScript files in the templates directory with template directives
---

# JavaScript Templates

JavaScript files placed in the `templates/` directory are processed through the Elements template engine, allowing you to inject component properties, conditionals, and dynamic values directly into your JavaScript code. This enables you to create interactive components with configuration driven by user properties.

## Overview

JavaScript template files provide:
- **Property insertion** - Use component properties in JavaScript code
- **Conditional code** - Include or exclude JavaScript based on conditions
- **Per-instance configuration** - Each component instance gets its own configuration
- **Portal injection** - Place scripts in specific page locations using `@portal`

## File Location

```
com.yourcompany.component/
├── templates/
│   ├── index.html
│   ├── script.js         # Component JavaScript
│   └── include/
│       └── ...
```

## Basic Usage

JavaScript files can use standard JavaScript syntax along with Elements template directives:

```javascript
// Initialize component with properties
const component = document.getElementById('component-{{id}}');
component.setAttribute('data-color', '{{color}}');
component.setAttribute('data-enabled', '{{enabled}}');

@if(autoStart)
// Auto-start functionality
component.classList.add('active');
@endif
```

## Property Insertion

Insert component properties directly into JavaScript values:

```javascript
// String values
const componentId = '{{id}}';
const title = '{{title}}';
const description = '{{description}}';

// Numeric values
const duration = {{duration}};
const delay = {{delay}};
const maxItems = {{maxItems}};

// Boolean values (be careful with JSON format)
const isEnabled = {{enabled}};  // true or false
const autoPlay = {{autoPlay}};

// Object properties
const settings = {
    color: '{{color}}',
    size: {{size}},
    animated: {{animated}}
};
```

## Portal Injection

A common pattern is to use `@portal` to inject JavaScript into specific page locations, typically `bodyEnd`:

```javascript
@portal(bodyEnd, includeOnce: true, id: "my-component-lib")
<script>
    // This script is included only once per page
    window.MyComponent = {
        init: function(id, options) {
            // Component initialization logic
        }
    };
</script>
@endportal
```

Then in your HTML template:

```html
<div id="component-{{id}}" data-component="myComponent">
    <!-- Component markup -->
</div>

<script>
    MyComponent.init('{{id}}', {
        color: '{{color}}',
        autoStart: {{autoStart}}
    });
</script>
```

See the [`@portal` documentation](../language/portal.md) for more details.

## Examples from Core Components

### Accordion Component (Alpine.js)

The Accordion uses a portal to define Alpine.js component logic once:

```javascript
@portal(bodyEnd, includeOnce: true, id: "com.realmacsoftware.accordion.alpine")
<script>
    document.addEventListener("alpine:init", () => {
        Alpine.data("accordion", (id, options = {}) => ({
            open: options.openOnLoad || false,
            id,
            options,
            init() {
                this.$watch("open", (value) => {
                    if (value && this.options.groupId) {
                        this.$dispatch("close-accordions-in-group", {
                            groupId: this.options.groupId,
                            id: this.id,
                        });
                    }
                });
            },

            details: {
                ["@close-accordions-in-group.window"](e) {
                    const { groupId, id } = e.detail;
                    if (groupId == this.options.groupId && id != this.id) {
                        this.open = false;
                    }
                },
                [":data-open"]() {
                    return this.open.toString();
                },
            },

            summary: {
                ["@click"]() {
                    this.open = !this.open;
                },
            },

            content: {
                ["x-show"]() {
                    return this.open;
                },
            },
        }));
    });
</script>
@endportal
```

Each accordion instance then uses this component with its own properties:

```html
<div x-data="accordion('{{id}}', { openOnLoad: {{openOnLoad}}, groupId: '{{groupId}}' })">
    <!-- Accordion markup -->
</div>
```

### Gallery Component (Image Lightbox)

The Gallery component includes lightbox functionality:

```javascript
@portal(bodyEnd, includeOnce: true, id: "gallery-lightbox-script")
<script>
    class Lightbox {
        constructor(galleryId, options) {
            this.galleryId = galleryId;
            this.options = options;
            this.init();
        }
        
        init() {
            // Lightbox initialization
        }
    }
    
    window.Lightbox = Lightbox;
</script>
@endportal
```

## Conditional JavaScript

Use `@if` directives to conditionally include code:

```javascript
const component = document.getElementById('{{id}}');

@if(enableLogging)
console.log('Component {{id}} initialized with:', {
    color: '{{color}}',
    size: {{size}}
});
@endif

@if(trackAnalytics)
// Send analytics event
analytics.track('component_loaded', {
    componentType: '{{componentType}}',
    componentId: '{{id}}'
});
@endif

@if(animation == "fade")
component.classList.add('fade-animation');
@elseif(animation == "slide")
component.classList.add('slide-animation');
@else
component.classList.add('no-animation');
@endif
```

## Processing Behavior

### Per-Instance Processing

JavaScript template files are processed **once per component instance**. Each instance gets its own `<script>` tag with processed code:

```javascript
// Instance 1
const comp1 = document.getElementById('component-abc123');
comp1.config = { color: 'blue' };

// Instance 2
const comp2 = document.getElementById('component-def456');
comp2.config = { color: 'red' };
```

### Inline Scripts

Processed JavaScript is inserted inline into the page within `<script>` tags, not as external files.

## Templates vs Assets

Choose the right location for your JavaScript:

### Use `templates/` JavaScript When:

- Code needs component property values
- Code is instance-specific
- Code needs conditional logic
- Configuration varies per instance

**Example:**
```javascript
const instance = new Component('{{id}}', {
    color: '{{userColor}}',
    speed: {{userSpeed}},
    enabled: {{enabled}}
});
```

### Use `assets/` JavaScript When:

- Code is static library code
- Code is shared across all instances
- Code is a large framework (Alpine.js, GSAP, etc.)
- You want better caching and performance

**Example:**
```javascript
// Reusable component class
class Component {
    constructor(id, options) {
        this.id = id;
        this.options = options;
    }
    // Component methods...
}
```

### Combining Both

A common pattern is to define classes in `assets/` and instantiate them in `templates/`:

```
components/
├── assets/
│   └── component-class.js    # Static class definition
└── templates/
    └── init.js               # Per-instance initialization
```

## Best Practices

### Use includeOnce for Libraries

When defining reusable functions or classes, use `includeOnce`:

```javascript
@portal(bodyEnd, includeOnce: true, id: "my-component-lib")
<script>
    // Define once for the entire page
    class MyComponent {
        // Class definition
    }
    window.MyComponent = MyComponent;
</script>
@endportal
```

### Avoid Inline Event Handlers

Instead of inline handlers in HTML:

```html
<!-- Avoid -->
<button onclick="handleClick('{{id}}', {{someValue}})">
```

Use proper event listeners in JavaScript:

```javascript
document.getElementById('button-{{id}}').addEventListener('click', function() {
    handleClick('{{id}}', {{someValue}});
});
```

### Escape String Values

Be careful with user-provided strings that might contain quotes:

```javascript
// Unsafe
const title = '{{title}}';  // Breaks if title contains '

// Better - use JSON encoding in hooks.js
const title = {{titleJSON}};
```

In `hooks.js`:
```javascript
rw.setProps({
    titleJSON: JSON.stringify(rw.props.title)
});
```

### Minimize Template JavaScript

Keep template JavaScript minimal and focused on configuration:

```javascript
// Good - just configuration
new MyComponent('{{id}}', {
    color: '{{color}}',
    size: {{size}}
});

// Better in assets/ - complex logic
class MyComponent {
    constructor(id, options) {
        // Complex implementation
    }
}
```

### Use Proper Scope

Avoid polluting global scope:

```javascript
// Avoid
function myFunction() {
    // Global function
}

// Better - use IIFE
(function() {
    const component = document.getElementById('{{id}}');
    // Component-specific code
})();

// Or use modern modules
{
    const component = document.getElementById('{{id}}');
    // Block-scoped code
}
```

### Handle Timing

Ensure DOM is ready before accessing elements:

```javascript
@if(edit)
// In edit mode, run immediately
const component = document.getElementById('{{id}}');
component.init();
@else
// In published mode, wait for DOM
document.addEventListener('DOMContentLoaded', function() {
    const component = document.getElementById('{{id}}');
    component.init();
});
@endif
```

## Common Patterns

### Alpine.js Integration

Define Alpine components with property-based configuration:

```javascript
@portal(bodyEnd, includeOnce: true, id: "my-alpine-component")
<script>
    document.addEventListener("alpine:init", () => {
        Alpine.data("myComponent", (id, config) => ({
            id,
            config,
            // Component state and methods
            init() {
                // Initialization
            }
        }));
    });
</script>
@endportal
```

```html
<div x-data="myComponent('{{id}}', {
    color: '{{color}}',
    autoStart: {{autoStart}}
})">
    <!-- Component markup -->
</div>
```

### GSAP Animations

Configure GSAP animations with user properties:

```javascript
@if(enableAnimation)
gsap.to('#component-{{id}}', {
    duration: {{duration}},
    opacity: {{targetOpacity}},
    x: {{translateX}},
    ease: '{{easing}}'
});
@endif
```

### Data Attributes

Set data attributes for JavaScript access:

```javascript
const element = document.getElementById('{{id}}');
element.dataset.componentId = '{{id}}';
element.dataset.variant = '{{variant}}';
element.dataset.enabled = '{{enabled}}';

// Later access
const variant = element.dataset.variant;
```

## Limitations

### No ES Modules

Template JavaScript doesn't support ES module syntax:

```javascript
// This won't work in template files
import { something } from './module.js';
export default MyComponent;

// Use traditional scripts or put modules in assets/
```

### Limited Preprocessing

Template JavaScript files don't support TypeScript, Babel, or other preprocessors. Use the Elements template language for logic.

### Execution Context

Template JavaScript runs in the page context, not in a controlled environment. Ensure code is safe and handles errors appropriately.

## Related Documentation

- [Elements Language](../language/README.md) - Template syntax reference
- [`@portal` Directive](../language/portal.md) - Injecting scripts to page locations
- [Templates Overview](README.md) - Understanding templates
- [Assets](../assets.md) - Static JavaScript files
- [Hooks.js](../hooks.js/README.md) - Preparing data for JavaScript
