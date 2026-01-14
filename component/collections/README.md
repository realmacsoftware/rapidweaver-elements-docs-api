---
description: Create flexible datasets for your components
icon: rectangle-history
---

# Collections

Collections provide a flexible way to create repeatable datasets for your components. They allow users to add, edit, and manage multiple items of structured data—perfect for features like audio playlists, image galleries, FAQ sections, pricing tables, and any content that follows a repeated pattern.

## Overview

Collections appear in the Elements inspector as a dedicated panel where users can add, remove, and reorder items. Each item in a collection has its own set of properties that you define.

## Directory Structure

To add collections to your component, create a `collections` folder at the root of your component directory. Each collection requires its own subfolder containing two files:

```
com.yourcompany.component/
├── collections/
│   └── {collection-name}/
│       ├── info.json
│       └── properties.json
├── templates/
│   └── index.html
├── hooks.js
├── info.json
└── properties.json
```

## Creating a Collection

### Step 1: Create the Collection Folder

Create a folder inside `collections/` with the name of your collection. Use lowercase with hyphens for multi-word names:

```
collections/
├── tracks/
├── features/
├── pricing-tiers/
└── team-members/
```

### Step 2: Define info.json

The `info.json` file identifies your collection to RapidWeaver:

```json
{
    "identifier": "com.yourcompany.component.collections.features",
    "title": "Features"
}
```

| Property | Required | Description |
|----------|----------|-------------|
| `identifier` | Yes | Unique identifier using reverse domain notation |
| `title` | Yes | Display name shown in the Elements interface |

### Step 3: Define properties.json

The `properties.json` file describes the fields for each item in your collection. It uses the same format as component properties:

```json
{
    "groups": [
        {
            "title": "Feature",
            "properties": [
                {
                    "title": "Title",
                    "property": "title",
                    "responsive": false,
                    "text": {
                        "default": ""
                    }
                },
                {
                    "title": "Description",
                    "property": "description",
                    "responsive": false,
                    "textArea": {
                        "default": ""
                    }
                },
                {
                    "title": "Icon",
                    "property": "icon",
                    "responsive": false,
                    "resource": {}
                }
            ]
        }
    ]
}
```

All UI controls available to components are also available within collections. See the [properties.json documentation](../properties.json/README.md) for the complete reference.

## Real-World Examples

### Tags Collection

A simple collection for filtering tags used in Grid, Flex, and Container components:

**collections/tags/info.json**
```json
{
    "identifier": "com.realmacsoftware.grid.collections.tags",
    "title": "Tags"
}
```

**collections/tags/properties.json**
```json
{
    "groups": [
        {
            "title": "Tag",
            "properties": [
                {
                    "title": "Title",
                    "property": "title",
                    "responsive": false,
                    "text": {
                        "default": ""
                    }
                }
            ]
        }
    ]
}
```

### Audio Tracks Collection

A more complex collection for an audio playlist with multiple fields:

**collections/tracks/info.json**
```json
{
    "identifier": "com.realmacsoftware.audioPlaylist.collections.tracks",
    "title": "Tracks"
}
```

**collections/tracks/properties.json**
```json
{
    "groups": [
        {
            "title": "Track",
            "properties": [
                {
                    "title": "Title",
                    "property": "title",
                    "responsive": false,
                    "text": { "default": "" }
                },
                {
                    "title": "Artist",
                    "property": "artist",
                    "responsive": false,
                    "text": { "default": "" }
                },
                {
                    "title": "Artwork",
                    "property": "coverImage",
                    "responsive": false,
                    "resource": {}
                },
                {
                    "title": "Audio Source",
                    "property": "audioSource",
                    "responsive": false,
                    "resource": {}
                }
            ]
        }
    ]
}
```

## Next Steps

Once you've created your collection structure, you need to:

1. **[Add the collection to properties.json](collections-in-properties.json.md)** - Make the collection appear in the component inspector
2. **[Access data in templates](accessing-data-in-templates.md)** - Display collection items in your HTML
3. **[Manipulate data in hooks.js](data-collections-in-hooks.js.md)** - Process collection data before rendering

## Best Practices

1. **Use descriptive identifiers** - Follow the pattern `com.company.component.collections.name` for clear organization.

2. **Keep properties focused** - Only include fields that users need for each collection item.

3. **Set appropriate defaults** - Provide sensible defaults to give users a starting point.

4. **Mark properties as non-responsive** - Collection properties typically don't need responsive values, so set `"responsive": false`.

5. **Group related properties** - Use property groups to organize complex collection items.
