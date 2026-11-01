---
name: moli-headless-browser
description: "AI agent headless browser by lexmount/moli (22k stars). Rust-based, lightweight, structure-first design. Use when fetching web pages, extracting content, browser automation, or web scraping for AI agents. Supports CLI fetch, CDP, WebDriver Classic, and WebDriver BiDi. Installed as a prebuilt binary."
---

# Moli Headless Browser

## Quick Start

Moli is installed at `~/.local/bin/moli`. Version: 1.1.20.

```bash
export PATH="$HOME/.local/bin:$PATH"

# Fetch a page as Markdown
moli fetch --dump markdown --wait-until done https://example.com

# Fetch as semantic tree (compact, model-friendly)
moli fetch --dump semantic_tree_text --wait-selector body https://example.com

# Take a screenshot (requires --layout)
moli fetch --layout --dump screenshot https://example.com > page.png
```

## Core Commands

### fetch
Render a URL and output content, screenshot, or JS result.

**Output formats (`--dump`):**
- `markdown` - clean Markdown text
- `semantic_tree_text` - compact semantic tree, ideal for LLMs
- `html` - raw HTML
- `json` - structured data
- `screenshot` - viewport PNG (requires `--layout`)
- `screenshot_full` - full-page PNG (requires `--layout`)
- `pdf` - paginated PDF (requires `--layout`)

**Wait options:**
- `--wait-until done` - wait for page load complete
- `--wait-selector body` - wait for element selector

**Interactivity:**
```bash
# Click a button then export
moli fetch --eval 'document.querySelector("button").click()' \
  --dump markdown https://example.com
```

### serve
Start automation server for CDP / WebDriver / WebDriver BiDi.

```bash
# Basic DOM-first server
moli serve

# Enable layout, geometry, screenshots
moli serve --layout

# Also fetch images, fonts, media
moli serve --layout --resource
```

The server listens on `http://127.0.0.1:9222` by default. Playwright can connect via CDP.

## Why Moli

- **Lightweight**: ~73 MiB median RSS vs Chrome Headless ~773 MiB
- **Fast**: structure-first by default, skips layout/paint unless needed
- **Full-featured**: real JS (V8), DOM, CSS, networking, storage
- **Standalone**: Rust-built, no Chromium dependency

## Common Workflows

### Extract article content for AI reading
```bash
moli fetch --dump markdown https://news-site.com/article
```

### Scrape a list of URLs
Loop through URLs, output Markdown for each.

### Browser automation with Playwright
```bash
moli serve --layout &
# Then connect Playwright via CDP to http://127.0.0.1:9222
```

## Installation

Installed via official script to `~/.local/bin/moli`.

Update: re-run the installer script from GitHub releases.

## Limitations

- No GUI browser or persistent window
- No GPU compositor, no WebGL/Canvas high-fidelity
- `--layout` needed for screenshots and coordinate input
- Resource families (images, fonts, media) must be explicitly enabled with `--resource` or specific flags
