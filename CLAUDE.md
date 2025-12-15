# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Obsidian plugin for generating metadata using the Anthropic Claude API. The project root serves as both the development environment and a test Obsidian vault.

## Development Commands

### Setup

```bash
bun install
./setup-vault.sh  # Sets up the test vault (optional, already configured)
```

### Build and Development

```bash
bun run dev     # Watch mode with auto-rebuild
bun run build   # Production build (runs check first)
```

### Code Quality

```bash
bun run check         # Run all checks (typecheck + lint + format check)
bun run typecheck     # TypeScript type checking only
bun run lint          # ESLint and markdownlint
bun run lint:fix      # Auto-fix linting issues
bun run format        # Format code with Prettier
bun run format:check  # Check formatting without changes
```

### Versioning

```bash
bun run version  # Update manifest.json and versions.json from package.json version
```

## Architecture

### Build System

- **Build script**: [build.ts](build.ts) uses Bun's native bundler
- **Entry point**: [src/main.ts](src/main.ts)
- **Output**: `dist/main.js` (CommonJS format)
- **Externals**: `obsidian` and `electron` are marked as external dependencies
- Watch mode available via `--watch` flag

### Plugin Structure

- **Main class**: `MetadataToolPlugin` extends Obsidian's `Plugin` class
- **Settings**: Type-safe settings interface in [src/settings.ts](src/settings.ts)
- **Settings tab**: `MetadataToolSettingTab` provides comprehensive UI in [src/settingsTab.ts](src/settingsTab.ts)
- **Metadata generation**: Claude AI integration in [src/metadata.ts](src/metadata.ts)
- **Utilities**: API calls and helper functions in [src/utils.ts](src/utils.ts)

### Configuration Files

- **[manifest.json](manifest.json)**: Obsidian plugin metadata (update before publishing)
- **[versions.json](versions.json)**: Maps plugin versions to minimum Obsidian versions
- **[tsconfig.json](tsconfig.json)**: TypeScript compiler options (noEmit mode, strict checking)
- **[eslint.config.js](eslint.config.js)**: Flat config format with TypeScript support

### Version Management

The [version-bump.ts](version-bump.ts) script syncs versions across files:

- Reads version from `package.json`
- Updates `manifest.json` version field
- Updates `versions.json` with new version and minimum Obsidian version

## Release Process

Tag and push to trigger GitHub Actions release:

```bash
git tag -a 1.0.0 -m "Release 1.0.0"
git push origin 1.0.0
```

## TypeScript Configuration

- Target: ES2022
- Module resolution: bundler (Bun-style)
- Strict mode enabled
- No emit (bundler handles output)

## Test Vault

This project root is configured as an Obsidian vault for testing:

- Plugin files are symlinked from `.obsidian/plugins/obsidian-metadata-tool/` to build output
- Sample notes are provided for testing metadata generation
- Open this folder as a vault in Obsidian to test the plugin
- Changes rebuild automatically in watch mode (`bun run dev`)
- Reload Obsidian (Cmd/Ctrl + R) to see changes

See [DEVELOPMENT.md](DEVELOPMENT.md) for detailed development workflow.
