# Copilot Instructions for WeChat Mini Program Plugin

This repository contains a WeChat Mini Program Plugin for live streaming features.

## Project Structure

- **`plugin/`**: The core plugin source code.
  - **`components/`**: UI components exposed by the plugin.
  - **`service/`**: API service logic.
  - **`plugin.json`**: Plugin configuration defining exposed components and pages.
- **`miniprogram/`**: A host Mini Program used for testing and demonstrating the plugin.
- **`doc/`**: Documentation files.

## Build, Test, and Lint

This project uses the WeChat DevTools ecosystem. There are no standard npm scripts for building or testing.

- **Linting**: Conforms to the rules in `.eslintrc.js` (ES6, browser/node env, WeChat globals).
- **Formatting**: Follows `.prettierrc`:
  - 2 spaces indentation
  - No semicolons (`semi: false`)
  - Single quotes (`singleQuote: true`)
  - Trailing commas (`trailingComma: "all"`)
  - Print width 120

## High-Level Architecture

The plugin provides a main component `<live-plugin>` which orchestrates sub-components like:
- `live-player-plugin`: The video player.
- `live-chat-plugin`: Chat functionality.
- `live-desc-plugin`: Live stream description.
- `live-file-plugin`: File sharing/downloads.
- `live-tabs-plugin`: Tab navigation within the live view.

These components communicate via properties and events, standard to the Mini Program component model.

## Key Conventions

### Plugin Initialization

Before using the plugin components, the host Mini Program must initialize the plugin with configuration. This is typically done in the host page's JS file:

```javascript
const plugin = requirePlugin('live-plugin')
// Must be called before plugin initialization
plugin.setApiHost('YOUR_API_HOST') 
plugin.setAccountToken('YOUR_TOKEN')
```

### Component Usage

The main entry component is `<live-plugin>`. It requires specific properties to function:

```html
<live-plugin
  classId="{{classId}}"
  liveRoomId="{{liveRoomId}}"
  identity="{{identity}}"     <!-- 1: Student, 2: TA, 3: Lecturer -->
  account="{{account}}"
  token="{{token}}"
  planId="{{planId}}"         <!-- Optional, for playback -->
/>
```

### Global Variables

The code relies on WeChat Mini Program globals which are defined in `.eslintrc.js`:
- `wx`: The main WeChat API object.
- `App`, `Page`, `Component`: Constructors for app, pages, and components.
- `requirePlugin`, `requireMiniProgram`: For plugin interactions.

### File Types

- **`.wxml`**: Structure (HTML-like).
- **`.wxss`**: Styling (CSS-like).
- **`.js`**: Logic (ES6).
- **`.json`**: Configuration.
