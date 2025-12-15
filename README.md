# Obsidian Metadata Tool

Automatically generate metadata for your Obsidian notes using Claude AI from Anthropic.

## Features

- Generate tags, descriptions, and titles for your notes using Claude AI
- Extract and manage existing tags from your vault
- Customize field names and prompts to match your workflow
- Add custom metadata fields
- Content truncation options to optimize API costs
- Support for multiple Claude models (Sonnet 4.5, Opus 4.5, Sonnet 3.7, Haiku 3.5)

## Installation

### Manual Installation

1. Download the latest release from the GitHub releases page
2. Extract the files to your vault's `.obsidian/plugins/obsidian-metadata-tool/` directory
3. Reload Obsidian
4. Enable the plugin in Settings → Community Plugins

### Development Installation

```bash
bun install
bun run build
```

Copy `manifest.json`, `main.js` (from `dist/`), and `styles.css` to your vault's
`.obsidian/plugins/obsidian-metadata-tool/` directory.

## Configuration

1. Open Settings → Metadata Tool
2. Add your Anthropic API key
3. Select your preferred Claude model
4. Customize field names and prompts as needed

### Settings Overview

#### API Settings

- API Key: Your Anthropic API key (get one at console.anthropic.com)
- Model: Choose from Claude Sonnet 4.5, Opus 4.5, Sonnet 3.7, or Haiku 3.5

#### Update Settings

- Update Method: Force update all fields or only update empty fields
- Truncate Content: Limit content sent to API to reduce costs
- Max Tokens: Maximum content length to send
- Truncate Method: How to truncate (beginning only, beginning + end, or headings)

#### Metadata Fields

- Tags: Extract existing tags or define custom ones
- Description: Customize summary generation
- Title: Auto-generate titles for notes
- Custom Fields: Add any additional metadata fields

## Usage

1. Open a note you want to add metadata to
2. Run the command "Generate metadata for current note" (Cmd/Ctrl + P)
3. The plugin will:
   - Analyze your note content
   - Generate appropriate tags, description, and title
   - Update the frontmatter with the generated metadata

## Example

Before:

```markdown
This is my note about gardening techniques...
```

After:

```markdown
---
tags:
  - gardening
  - techniques
  - plants
description: A comprehensive guide to various gardening techniques and best practices
title: Gardening Techniques Guide
---

This is my note about gardening techniques...
```

## Development

```bash
bun install        # Install dependencies
bun run dev        # Watch mode with auto-rebuild
bun run build      # Production build
bun run check      # Type check, lint, and format check
```

## Release

Tag and push to trigger GitHub Actions release:

```bash
git tag -a 1.0.0 -m "Release 1.0.0"
git push origin 1.0.0
```

## License

MIT
