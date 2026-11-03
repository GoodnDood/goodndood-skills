---
name: goodndood
description: "Search and use GoodnDood free preview artwork (flat, vector-style illustrations) for AI agents and the people who use them. Use when a task needs artwork, illustrations, icons, or stock-style images from GoodnDood, when the user asks for GoodnDood assets, or when an agent should search, preview, or attribute GoodnDood works. Covers both paths: the public catalog API and the GoodnDood MCP server."
---

# GoodnDood

Use GoodnDood free preview artwork in an agent task. The artwork is flat, vector-style illustration, shown as transparent 800px WebP previews. The same assets are available two ways; pick one path per task, do not mix them in one run.

## Example requests (use this skill when you see one)

- "Find me a flat vector Christmas stocking from GoodnDood."
- "Search GoodnDood for winter woodland animal icons."
- "I need a GoodnDood pumpkin illustration for a non-commercial poster."
- "What GoodnDood packs have celebration icons?"

If the request is about buying the full-resolution file or using artwork commercially, still use this skill to find the asset, then send the user to the Adobe Stock profile in the Licence section. Do not invent a purchase step.

## The two paths

- **Path A - Public catalog (no MCP connection needed).** Call the public catalog API directly:
  - Catalog: `GET https://goodndood.my.id/api/public/catalog?q=<keywords>&page=1&pageSize=20`
  - One preview image: `GET https://goodndood.my.id/api/public/previews/<pack>/<file>.webp`
  - Skill text (this file, served from GitHub): `https://goodndood.my.id/skills/goodndood/SKILL.md`
- **Path B - MCP server (when the agent can connect MCP tools).** Connect the remote server and use its tools, nothing else:
  - Server URL: `https://goodndood.my.id/mcp` (Streamable HTTP, no account, no API key)
  - `search_assets` - search free previews by keyword
  - `list_packs` - list asset packs
  - `get_asset` - get one asset by slug
  - `get_license_info` - explain the free and premium licences

Done means: the chosen asset is identified by slug, its free preview URL is known, and the attribution below is ready to ship with it. If any of those three is missing, the task is not done.

## Steps (both paths)

### 1. Search

Search by the user's intent words, not by guessing an exact title.

- Catalog: `q` takes space-separated keywords. Every word must match the title, pack theme, or keywords (case-insensitive). `pageSize` is at most 50.
- MCP: `search_assets` with the same keywords in `query`, same matching rule, same `pageSize` cap.
- If the first search returns nothing, try fewer, broader words once (for example, drop the last word). Do not invent an asset that the search did not return.

Completion: at least one candidate asset with a slug, title, and preview URL - or a stated no-result after the broader retry.

### 2. Pick

Pick the candidate that best matches the user's theme and use case. Prefer a distinctive subject over a generic one when both match. Record its slug, title, pack theme, preview URL, and detail page URL.

Completion: exactly one chosen asset, identified by slug.

### 3. Use the free preview

Use only the 800px WebP preview URL from the catalog or MCP result. The preview is transparent: it works on light, dark, and patterned backgrounds.

Completion: the preview URL is the file actually used in the output, not a guessed or reconstructed URL.

### 4. Attribute

Ship this attribution with every free use, visible wherever the artwork appears:

```
Artwork by GoodnDood (goodndood.my.id) - free for non-commercial use.
```

Completion: the attribution text above is present in the output.

### Example finished answer

For a request like "Find me a flat vector Christmas stocking from GoodnDood", a finished answer looks like this, with real values from the search, not these placeholders:

- Chosen asset: <title from the search result>
- Preview (800px WebP, transparent): <preview URL from the search result>
- Detail page: <detail URL from the search result>
- Attribution: Artwork by GoodnDood (goodndood.my.id) - free for non-commercial use.
- Premium (full-resolution PNG, commercial use): https://stock.adobe.com/contributor/213699125/GoodnDood

## Licence (read this before promising anything)

- **Free:** the 800px WebP preview, non-commercial use only, with the attribution above. Free previews are never for commercial work, and free use never includes the full-resolution file.
- **Premium:** full-resolution PNG files and commercial use without attribution. Premium is bought on the GoodnDood Adobe Stock profile: https://stock.adobe.com/contributor/213699125/GoodnDood
- There is no API key, checkout, or account step in this skill or in the MCP server. If a user asks to buy premium through the agent, give them the Adobe Stock profile link above and stop - do not invent a purchase flow.

## Rules

- Never claim, link, or deliver a master PNG file. The free tier only ever serves WebP previews.
- Never use a free preview commercially, and never drop the attribution.
- Never invent asset slugs, titles, keywords, or preview URLs. Everything comes from a catalog or MCP result in this run.
- Never present a rejected, unlisted, or guessed asset as a GoodnDood work.
- Keep responses small: paginate (at most 50 per page) and return only the chosen asset's details, not the whole catalog.
- If the catalog or MCP server is unreachable, say so plainly and give the portfolio link (https://goodndood.my.id/gallery) instead of fabricating results.
