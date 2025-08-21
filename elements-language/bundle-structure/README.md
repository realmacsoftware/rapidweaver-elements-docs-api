---
icon: box
---

# Element Pack

### What Is an Element Pack?

An Element Pack is a folder-based “plugin” format for sharing and distributing addons for Elements.

* Development Use Only: An Element Pack ends with a `.elementsdevpack` extension. This format is strictly for development environments and should not be sold or shared in this form.
* Distributable Version: To share your packs with others you'll use the Elements Store. Distributable packs are non-editable, pre-processed, optimised and encrypted to protect your code. You can [learn more about distributing your addons here](../../elements-marketplace/distribution.md).

### What Can You Include?

Your Element Pack can bundle together different types of add-ons, such as any combination of the following:

* Components – Reusable, structured elements
* Resources – Assets like images or other files
* Templates – Pre-built sections consisting of multiple components
* Themes – Predefined visual styles
* Projects – (Planned for future support)

Note: Element Packs must follow the macOS “bundle” structure. Templates, Resources, and Themes are created within Elements whereas Components are typically built outside of Elements using an editor like VS Code.

### Folder Structure Overview

Here’s how a typical `.elementsdevpack` bundle is organized:

```
MyElementPack.elementsdevpack/
├── info.json
├── components/
│   ├── com.companyname.slideshow/
│   ├── com.companyname.navbar/
│   └── shared/
│       ├── assets/
│       └── templates/
└── themes/
    ├── com.companyname.themes.architect/
    └── com.companyname.themes.solar/
```

#### Folder Breakdown:

* Root folder (MyElementPack.elementsdevpack)
  * [info.json](info.json.md) - \[required] the main configuration file for the pack
  * components - contains folders for each custom component
  * themes - contains folders for each custom theme

