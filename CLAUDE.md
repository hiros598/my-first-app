# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project status

This repository is at its starting point: there is no application code, package manifest, build, lint, or test setup yet. When those are added, update this file with the real commands.

The user communicates in Japanese; respond in Japanese.

## Playwright MCP (browser verification)

`.mcp.json` registers the Playwright MCP server (`npx @playwright/mcp@0.0.82 --headless --browser chromium`), used to check pages in a headless browser.

Setup gotchas in this Codespace (Ubuntu):

- The MCP server pins its own browser build, which can differ from what `npx playwright install chromium` downloads. If navigation fails with `Browser "chrome-for-testing" is not installed`, run:
  `npx -y @playwright/mcp@0.0.82 install-browser chrome-for-testing`
- If it fails with missing system dependencies, run:
  `sudo npx -y playwright install-deps chromium`
  (the `@playwright/mcp` CLI does not accept `install-deps`).
- Snapshots are written to `.playwright-mcp/`, which is gitignored.
- `.devcontainer/devcontainer.json` reinstalls the browser and its system dependencies on Codespace rebuild (`postCreateCommand`).
- The MCP version is pinned. When upgrading, change the version in both `.mcp.json` and `.devcontainer/devcontainer.json`, then rerun the `install-browser` command above.
