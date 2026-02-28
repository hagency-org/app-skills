# Deep Search

Version: 1.0.0
Author: hagency

## Overview

The `deep_search` tool performs comprehensive web research by combining web search with parallel page content fetching. It searches the web for a given query, fetches the full content of the top results, and saves everything to a local research directory for later reference.

## Usage

Call `deep_search` with a query string. The tool will:

1. Search the web using DuckDuckGo (or optionally Brave, You.com, or Perplexity if API keys are set)
2. Fetch and extract content from the top result pages in parallel
3. Save each page as a markdown file under `./research/<query-slug>/`
4. Return an index of results with inline previews

### Parameters

- **query** (required, string): The search query to research.
- **max_results** (optional, integer, default: 8): Number of search results to fetch and crawl (1-10).
- **search_engine** (optional, string): Preferred search engine. Options: `duckduckgo`, `brave`, `you`, `perplexity`. Defaults to auto-detection based on available API keys.

### Example

```json
{
  "query": "Rust async runtime comparison 2025",
  "max_results": 5,
  "search_engine": "duckduckgo"
}
```

### Output

The tool returns a JSON object:

```json
{
  "output": "<formatted search results with inline previews>",
  "success": true
}
```

### Saved Files

Results are saved to `./research/<query-slug>/`:

- `_search_results.md` -- raw search results index
- `01_<domain>.md` -- full page content from first result
- `02_<domain>.md` -- full page content from second result
- etc.

Use `read_file` on any saved file to access the full page content for detailed analysis and synthesis.

### Environment Variables (Optional)

- `BRAVE_API_KEY` -- enables Brave Search (free tier: 2k queries/month)
- `YDC_API_KEY` -- enables You.com search
- `PERPLEXITY_API_KEY` -- enables Perplexity Sonar (AI-synthesized, most expensive)

Without any API keys, DuckDuckGo HTML search is used (free, no key required).
