# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Chrome extension that opens GitHub-hosted Jupyter notebooks directly in Google Colab. When clicked on a GitHub page containing a `.ipynb` file, it redirects to `https://colab.research.google.com/github/` or `/gist/` with the appropriate parameters.

## Development Commands

### Build TypeScript
```bash
npx tsc
```

There are no specific build, lint, or test commands defined in package.json. The project uses TypeScript compilation directly.

## Architecture

The extension consists of two main TypeScript files:

1. **service_worker.ts** - Background service worker that:
   - Listens for extension icon clicks
   - Calls `githubToColabUrl()` to convert the current URL
   - Opens a new tab with the Colab URL or shows a help popup for unsupported pages

2. **parse.ts** - URL parsing logic:
   - `githubToColabUrl()` - Converts GitHub notebook URLs to Colab URLs
   - Supports both regular GitHub repos and Gists
   - Contains branch name extraction logic (currently has a bug with `encoeeURIComponent` typo on line 53)

The extension uses Manifest v3 and requires TypeScript compilation before use. Both `.ts` files need to be compiled to `.js` for the extension to function.