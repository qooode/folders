# Folder import

This repository provides a specification for creating custom folder configurations that can be imported into your media organization system. With this system, you can easily share, distribute, and apply consistent folder layouts across multiple devices.

## Overview

The folder configuration system allows you to:

- Create visually appealing content organization structures
- Customize folder appearance including layouts, colors, icons, and text styles
- Group folders into categories
- Share your folder setups with the community
- Import pre-designed folder sets from URLs

This README explains how to create valid JSON configuration files that will work with the import system.

## JSON Structure

Folder configurations are defined in JSON format. A configuration file can contain a single folder object or an array of multiple folder objects.

### Basic Structure

```json
[
  {
    "id": "unique-folder-id",
    "name": "Folder Name",
    "category": "Category Name",
    "catalogIds": [],
    "displayMode": "Rows",
    "layout": "Poster",
    "backgroundColor": "#FF0000",
    "backgroundImageURL": "https://example.com/image.jpg",
    "logoURL": "https://example.com/logo.png",
    "mediaTypeFilter": "All Content",
    "iconName": "folder.fill",
    "showIcon": true,
    "nameDisplayMode": "Below Folder",
    "vignetteColor": "#000000",
    "textSize": "Large",
    "textWeight": "Bold",
    "textColor": "#FFFFFF"
  }
]
```

## Required and Optional Fields

### Required Fields

These fields must be included in every folder object:

| Field | Type | Description | Valid Values |
|-------|------|-------------|--------------|
| `name` | String | Display name of the folder | Any text |
| `catalogIds` | Array | IDs of catalogs in the folder (use empty array for imports) | `[]` |
| `displayMode` | String | How content is displayed within the folder | `"Rows"`, `"Grid"` |
| `layout` | String | Shape/dimensions of the folder | `"Poster"`, `"Landscape"`, `"Square"` |
| `iconName` | String | SF Symbol name for folder icon | Any valid SF Symbol name |
| `showIcon` | Boolean | Whether to show the folder icon | `true`, `false` |
| `nameDisplayMode` | String | Where the folder name is displayed | `"Below Folder"`, `"Inside Folder"`, `"Hidden"` |
| `mediaTypeFilter` | String | Type of media to display | `"All Content"`, `"Movies Only"`, `"TV Shows Only"` |
| `textSize` | String | Size of text inside the folder | `"Small"`, `"Medium"`, `"Large"` |
| `textWeight` | String | Weight of text inside the folder | `"Regular"`, `"Medium"`, `"Bold"` |

### Optional Fields

These fields can be omitted and will use default values:

| Field | Type | Description | Default |
|-------|------|-------------|---------|
| `id` | String | Unique identifier for the folder | Auto-generated UUID |
| `category` | String | Category name to organize folders | `"Folders"` |
| `backgroundColor` | String | Hex color code for folder background | Random color |
| `backgroundImageURL` | String | URL for custom background image | `null` |
| `logoURL` | String | URL for custom logo image | `null` |
| `vignetteColor` | String | Hex color code for vignette overlay effect | `null` |
| `textColor` | String | Hex color code for text color | System default |

### Field Details

#### `layout`
Controls the shape and dimensions of the folder:
- `"Poster"`: Portrait orientation with 2:3 ratio (240×360 points)
- `"Landscape"`: Landscape orientation with 16:9 ratio (427×240 points)
- `"Square"`: Square shape with 1:1 ratio (240×240 points)

#### `displayMode`
Controls how content is displayed within a folder:
- `"Rows"`: Content is displayed in horizontal scrolling rows
- `"Grid"`: Content is displayed in a grid layout

#### `mediaTypeFilter`
Filters the type of content shown in the folder:
- `"All Content"`: Shows both movies and TV shows
- `"Movies Only"`: Shows only movies
- `"TV Shows Only"`: Shows only TV shows

#### `nameDisplayMode`
Controls where the folder name is displayed:
- `"Below Folder"`: Name appears below the folder
- `"Inside Folder"`: Name appears inside the folder
- `"Hidden"`: Doesn't show the name at all

#### `textSize`
Controls the size of text:
- `"Small"`: 22pt
- `"Medium"`: 28pt
- `"Large"`: 34pt

#### `textWeight`
Controls the weight of text:
- `"Regular"`: Regular weight
- `"Medium"`: Medium weight
- `"Bold"`: Bold weight

#### `iconName`
Uses SF Symbols for icons. Some examples:
- `"folder.fill"`: Filled folder icon
- `"star.fill"`: Filled star icon
- `"heart.fill"`: Filled heart icon
- `"film"`: Film icon
- `"tv"`: TV icon
- `"play.rectangle.fill"`: Filled play rectangle

## Examples

### Minimal Example
```json
[
  {
    "name": "Favorites",
    "catalogIds": [],
    "displayMode": "Grid",
    "layout": "Poster",
    "iconName": "star.fill",
    "showIcon": true,
    "nameDisplayMode": "Below Folder",
    "mediaTypeFilter": "All Content",
    "textSize": "Large",
    "textWeight": "Bold"
  }
]
```

### Comprehensive Example
```json
[
  {
    "id": "netflix-folder",
    "name": "Netflix",
    "category": "Streaming",
    "catalogIds": [],
    "displayMode": "Rows",
    "layout": "Landscape",
    "backgroundColor": "#E50914",
    "iconName": "play.rectangle.fill",
    "showIcon": true,
    "nameDisplayMode": "Inside Folder",
    "mediaTypeFilter": "All Content",
    "textSize": "Large",
    "textWeight": "Bold",
    "textColor": "#FFFFFF"
  },
  {
    "id": "disney-folder",
    "name": "Disney+",
    "category": "Streaming",
    "catalogIds": [],
    "displayMode": "Grid",
    "layout": "Landscape",
    "backgroundColor": "#113CCF",
    "iconName": "sparkles",
    "showIcon": true,
    "nameDisplayMode": "Inside Folder",
    "mediaTypeFilter": "All Content",
    "textSize": "Large",
    "textWeight": "Bold",
    "textColor": "#FFFFFF"
  },
  {
    "id": "action-movies",
    "name": "Action Movies",
    "category": "Genres",
    "catalogIds": [],
    "displayMode": "Grid",
    "layout": "Poster",
    "backgroundColor": "#FF3B30",
    "iconName": "flame.fill",
    "showIcon": true,
    "nameDisplayMode": "Below Folder",
    "mediaTypeFilter": "Movies Only",
    "textSize": "Medium",
    "textWeight": "Medium",
    "textColor": "#FFFFFF"
  }
]
```

### Example with Custom Images
```json
[
  {
    "name": "Netflix",
    "category": "Streaming",
    "catalogIds": [],
    "displayMode": "Rows",
    "layout": "Landscape",
    "backgroundColor": "#000000",
    "backgroundImageURL": "https://example.com/netflix-bg.jpg",
    "logoURL": "https://upload.wikimedia.org/wikipedia/commons/7/7a/Logonetflix.png",
    "iconName": "play.rectangle.fill",
    "showIcon": false,
    "nameDisplayMode": "Inside Folder",
    "mediaTypeFilter": "All Content",
    "textSize": "Large",
    "textWeight": "Bold"
  }
]
```

## Hosting Your JSON File

Your JSON file can be hosted on any service that provides a direct URL to the raw JSON content:

1. **GitHub Gist**: Create a gist and use the "Raw" link
2. **GitHub Repository**: Host in a repository and use the raw file URL
3. **Personal Website**: Host on your own web server
4. **JSON Hosting Services**: Services like JSONBin.io or similar

Make sure the URL points directly to the raw JSON content, not to an HTML page or viewer.

## Importing Folders

To import your folder configuration:

1. Go to the Settings menu in the app
2. Navigate to Folders > Import Folders
3. Enter the URL to your JSON file
4. Click "Import"

The system will download the JSON file, validate it, and add the folders to your library.

## How Import Works

When importing folder configurations:

1. The system downloads the JSON from the provided URL
2. It validates the JSON structure and required fields
3. For each folder in the JSON:
   - If a folder with the same name and category already exists, it will be updated with the new settings
   - If no matching folder exists, a new folder will be created
4. Existing catalog references are preserved when updating folders
5. New folders start with empty catalog references that you can populate later

## Troubleshooting

### Common Import Errors

| Error | Possible Cause | Solution |
|-------|----------------|----------|
| "Invalid URL format" | The URL provided is not properly formatted | Check that your URL is correct and points to a raw JSON file |
| "Invalid server response" | The server returned a non-200 status code | Ensure the file is accessible and the host is working properly |
| "Invalid JSON format" | The JSON is malformed or missing required fields | Validate your JSON structure and ensure all required fields are present |
| "keyNotFound" errors | Missing a required field | Add the missing field to your JSON objects |
| "dataCorrupted" errors | Value not valid for the field type | Check field values match the expected enum cases (exact spelling matters) |

### JSON Validation

Before importing, validate your JSON using:
- [JSONLint](https://jsonlint.com/)
- [JSON Validator](https://jsonformatter.curiousconcept.com/)

### Field Value Validation

Ensure your enum values match exactly:
- Layout: `"Poster"`, `"Landscape"`, `"Square"`
- DisplayMode: `"Rows"`, `"Grid"`
- NameDisplayMode: `"Below Folder"`, `"Inside Folder"` (not "Outside Folder"), `"Hidden"`
- MediaTypeFilter: `"All Content"`, `"Movies Only"`, `"TV Shows Only"`
- TextSize: `"Small"`, `"Medium"`, `"Large"`
- TextWeight: `"Regular"`, `"Medium"`, `"Bold"`

---

## Contributing

Feel free to contribute to this project with cool examples.
