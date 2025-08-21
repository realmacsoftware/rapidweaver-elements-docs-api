---
icon: cube
---

# Components

A component is a single item that can be added to a page in the Elements app. Each component lives in its own folder within the pack and follows a clear structure. This guide lays out how each component should be organized, what files it requires, and how each part functions together.

### Folder Structure Overview

Each component is self-contained: all templates, assets, and logic should live within a single folder. You should use a reverse domain name as the component directory name.&#x20;

```
components/
├── com.companyname.slideshow/
│   ├── info.json
│   ├── properties.json
│   ├── hooks.js
│   ├── icon.pdf
│   ├── icon-dark.pdf
│   ├── paletteIcon.pdf
│   ├── paletteIcon-dark.pdf
│   ├── templates/
│   │   ├── pageStart/
│   │   ├── pageEnd/
│   │   ├── bodyStart/
│   │   ├── bodyEnd/
│   │   ├── includes/
│   │   ├── *.html
│   │   ├── *.php
│   │   ├── *.css
│   │   └── *.js
│   └── assets/
├── com.companyname.navbar/
│   └── ...
└── shared/
    ├── assets/
    └── templates/
```

#### Component directory breakdown

*   [info.json](info.json.md) (required)

    The “manifest” file defines the component’s meta data (identifier, title, author, group, etc.).
*   [properties.json](properties.json/)

    Defines the configurable options (controls) users see when using the component.
*   [icon.pdf, icon-dark.pdf, paletteIcon.pdf, paletteIcon-dark.pdf](icons.md)

    A small icon that visually represents the component inside Elements.
*   [templates](templates/)/

    Contains HTML templates for rendering the component output. All files are processed using Elements language.

    * \*.html - The component's output. All html/php files processed, concatenated together and added to the page.
    * \*.css - All css files are processed and concatenated together. They're added to the page's css file during publish.
    * \*.js - All javascript files are processed and concatenated together. They're added to the page's js file during publish.
    * [include/](templates/includes.md) - sub-templates you can include or reuse multiple times.
    * pageStart/, pageEnd/, bodyStart/, bodyEnd/ - templates added to these folders will be injected into the page in the corresponding areas.
* [assets/](assets.md) - Contains supporting files like CSS, JavaScript, or images that should not be processed for Elements language.
*   [hooks.js](hooks.js/)

    A JavaScript file where you can define logic, data handling, or custom behavior for the component.
