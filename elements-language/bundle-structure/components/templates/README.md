---
description: Component Template Folder
icon: brackets-curly
---

# Templates

Template files in RapidWeaver Elements house all the HTML, CSS, JavaScript, and other assets your component needs to work seamlessly. All template files are dynamically processed by Elements, allowing for property replacements (think handlebars-style), perform iterations, and more. This enables you to build highly flexible and reusable components.

{% hint style="info" %}
Any files that don't contain Elements template language should be store in the [assets](../assets.md) directory
{% endhint %}

### Templates Directory Structure

The structure of the templates directory is important and denotes in which area the contained files will be inserted into the page. Any files placed at the root of the templates directory will be processed and added for each instance of the component on the page.

The templates directory may also contain the following sub directories

* **headStart** - Placed at the top of head
* **headEnd** - Placed at the end of head
* **bodyStart** - Placed at the top of body
* **bodyEnd** - Placed at the bottom of body
* **include** - Files can be included from other template files using an [@include](include.md) statement
* [**backend**](../backend.md) - Additional supporting files deployed to the server

### Supported Template File Types

* **html** - contains HTML content
* **js** - contains javascript
* **css** - CSS styles
* **php** - files containing PHP
