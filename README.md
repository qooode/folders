# Folder Import

This guide explains how to create, share, and import folder configurations, allowing you to quickly set up folder collections with customized appearances.

## Table of Contents
- [Overview](#overview)
- [JSON Structure](#json-structure)
- [Required and Optional Fields](#required-and-optional-fields)
- [Examples](#examples)
- [Hosting Your JSON File](#hosting-your-json-file)
- [Importing Folders](#importing-folders)
- [How Import Works](#how-import-works)
- [Troubleshooting](#troubleshooting)

## Overview

The folder import feature allows you to:
- Import folders with predefined visual styles and configurations
- Share folder setups with other users
- Set up multiple folders at once
- Create themed folder collections (streaming services, genres, etc.)

When you import folders, only the folder configurations are imported - not the content inside them. You'll still need to add your own catalogs to the imported folders afterward.

## JSON Structure

The import file must be a valid JSON file with either a single folder object or an array of folder objects. Here's the basic structure:

```json
[
  {
    "id": "optional-uuid-string",
    "name": "Folder Name",
    "category": "Category Name",
    "catalogIds": [],
    "displayMode": "Rows",
    "layout": "Poster",
    // Other properties...
  },
  // More folder objects...
]
```

## Required and Optional Fields

### Required Fields
These fields MUST be included in your JSON for each folder:

| Field | Description | Possible Values |
|-------|-------------|----------------|
| `name` | Display name of the folder | Any string |
| `category` | Category group for the folder | Any string |
| `catalogIds` | Array of catalog IDs | `[]` (Empty array for imported folders) |
| `displayMode` | How content is displayed | `"Rows"` or `"Grid"` |
| `layout` | Folder shape/dimensions | `"Poster"`, `"Landscape"`, or `"Square"` |
| `mediaTypeFilter` | Type of content to show | `"All Content"`, `"Movies Only"`, or `"TV Shows Only"` |
| `iconName` | SF Symbol name for folder icon | Any valid SF Symbol name (e.g., `"folder.fill"`) |
| `showIcon` | Whether to display the icon | `true` or `false` |
| `nameDisplayMode` | Where to show the folder name | `"Inside Folder"` or `"Outside Folder"` |
| `textSize` | Size of text in the folder | `"Small"`, `"Medium"`, or `"Large"` |
| `textWeight` | Weight of text in the folder | `"Regular"`, `"Medium"`, or `"Bold"` |

### Optional Fields
These fields can be omitted from your JSON:

| Field | Description | Example |
|-------|-------------|---------|
| `id` | Unique identifier | `"550e8400-e29b-41d4-a716-446655440000"` |
| `backgroundColor` | Hex color code for background | `"#FF3B30"` |
| `backgroundImageURL` | URL to background image | `"https://example.com/bg.jpg"` |
| `logoURL` | URL to logo image | `"https://example.com/logo.png"` |
| `vignetteColor` | Hex color code for vignette effect | `"#000000"` |
| `textColor` | Hex color code for text | `"#FFFFFF"` |

## Examples

### Streaming Services Example

```json
[
  {
    "name": "Netflix",
    "category": "Streaming",
    "catalogIds": [],
    "displayMode": "Rows",
    "layout": "Landscape",
    "iconName": "play.rectangle.fill",
    "backgroundColor": "#E50914",
    "nameDisplayMode": "Inside Folder",
    "showIcon": true,
    "mediaTypeFilter": "All Content",
    "textSize": "Large",
    "textWeight": "Bold"
  },
  {
    "name": "Disney+",
    "category": "Streaming",
    "catalogIds": [],
    "displayMode": "Grid",
    "layout": "Landscape",
    "iconName": "sparkles",
    "backgroundColor": "#113CCF",
    "nameDisplayMode": "Inside Folder",
    "showIcon": true,
    "mediaTypeFilter": "All Content",
    "textSize": "Large",
    "textWeight": "Bold"
  }
]
```

### Movie Genres Example

```json
[
  {
    "name": "Action",
    "category": "Genres",
    "catalogIds": [],
    "displayMode": "Grid",
    "layout": "Poster",
    "iconName": "flame.fill",
    "backgroundColor": "#FF3B30",
    "nameDisplayMode": "Outside Folder",
    "showIcon": true,
    "mediaTypeFilter": "Movies Only",
    "textSize": "Medium",
    "textWeight": "Medium"
  },
  {
    "name": "Comedy",
    "category": "Genres",
    "catalogIds": [],
    "displayMode": "Grid",
    "layout": "Poster",
    "iconName": "face.smiling",
    "backgroundColor": "#FFCC00",
    "nameDisplayMode": "Outside Folder",
    "showIcon": true,
    "mediaTypeFilter": "Movies Only",
    "textSize": "Medium",
    "textWeight": "Medium"
  }
]
```

## Hosting Your JSON File

You'll need to host your JSON file somewhere that provides a direct URL to the raw file content. Some options include:

1. **GitHub Gist**
   - Create a gist at [gist.github.com](https://gist.github.com)
   - Click "Raw" to get the direct URL

2. **Pastebin**
   - Create a paste at [pastebin.com](https://pastebin.com)
   - After creating, click "Raw" to get the direct URL

3. **Dropbox**
   - Upload your file to Dropbox
   - Generate a shared link and modify it to start with `dl.dropboxusercontent.com` instead of `www.dropbox.com`

4. **Personal Website**
   - Upload your JSON file to your website
   - Use the direct URL to the file

Make sure the URL leads directly to the raw JSON content, not to a webpage containing the JSON.

## Importing Folders

To import folders in Strimi:

1. Navigate to **Settings > Folders**
2. Click on **Import Folders from URL**
3. Enter the URL to your hosted JSON file
4. Click **Import**

If successful, your folders will be added to your library immediately.

## How Import Works

When importing folders:

- If a folder with the same name and category already exists, it will be updated with the imported settings, but its existing catalog references will be preserved
- If it's a new folder, it will be added with empty catalogIds
- All imported folders will have their visual styles applied immediately
- After import, you'll need to add catalogs to the folders manually by editing each folder

## Troubleshooting

### Common Issues

1. **"Invalid URL format" error**
   - Make sure your URL is correct and starts with `http://` or `https://`
   - Try copying and pasting the URL into a browser to verify it works

2. **"Invalid server response" error**
   - The server returned a non-200 status code
   - Make sure your URL is publicly accessible

3. **JSON decode errors**
   - Check that your JSON is valid (use a validator like [jsonlint.com](https://jsonlint.com))
   - Verify that all required fields are included
   - Check field values match the expected format/options

4. **Missing fields error**
   - Make sure each folder object includes all required fields
   - `catalogIds` must be included (can be an empty array `[]`)

5. **No folders appeared after import**
   - Check the app logs for errors
   - Verify your JSON structure matches the examples
   - Try importing a simpler example first

### Testing Your JSON

You can validate your JSON file is correct by:
1. Using an online validator like [jsonlint.com](https://jsonlint.com)
2. Testing with a single folder first before creating a larger collection
3. Using the example templates from this guide as a starting point

## Community Sharing

Feel free to share your folder configurations with the Strimi community! Creating themed folder collections (like streaming services, movie studios, or genres) can help other users quickly set up their libraries.
