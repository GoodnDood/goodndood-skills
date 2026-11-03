# GoodnDood Skills

Public home of the GoodnDood skill for AI agents.

Repository: https://github.com/GoodnDood/goodndood-skills

## Install (one command)

Run this in your project folder. It needs Node.js, which you already have if you run Claude Code or Codex:

```bash
npx skills@latest add GoodnDood/goodndood-skills --skill goodndood -y
```

For every project on your machine instead of one folder, use the global form:

```bash
npx skills@latest add GoodnDood/goodndood-skills --skill goodndood -g -y
```

This command was verified against this repository: it installs the `goodndood` skill and reports "Installed 1 skill".

## Check that it worked

After the command finishes, your project folder should contain this file:

```
.agents/skills/goodndood/SKILL.md
```

Then start a new agent session so it picks up the new skill, and ask it for GoodnDood artwork by theme or keyword.

## How to use it

You do not need to learn any commands. After installing, just talk to your agent in plain words. The agent searches the GoodnDood catalog, picks one matching preview, and shows it to you with attribution.

### What to say to your agent

Copy one of these, or write your own in the same style:

- "Find me a flat vector Christmas stocking from GoodnDood."
- "Search GoodnDood for winter woodland animal icons."
- "I need a GoodnDood pumpkin illustration for a non-commercial poster."
- "What GoodnDood packs have celebration icons?"

### What happens, step by step

1. You ask for artwork in plain words.
2. Your agent searches the GoodnDood catalog by those words.
3. Your agent shows you the best matching preview: a transparent 800px WebP image you can use on light, dark, or patterned backgrounds.
4. Every free use carries this attribution, visible wherever the artwork appears:

```
Artwork by GoodnDood (goodndood.my.id) - free for non-commercial use.
```

### What you get, and what you do not get

- Free: the 800px WebP preview, for non-commercial use, with attribution. That is all the Skill and the MCP server can deliver.
- Premium: the full-resolution PNG file, and commercial use without attribution. Premium is bought on the [GoodnDood Adobe Stock profile](https://stock.adobe.com/contributor/213699125/GoodnDood). No agent, Skill, or MCP tool can sell or deliver the premium file. If an agent offers you one, it is inventing it.

### Skill or MCP, which one do I need?

You need only one. The Skill is for agents that read skill files. The MCP server is for agents that connect to MCP tools. Both search the same catalog and return the same free previews. If you are not sure, use the MCP server: it needs no install.

## If the skill is not found

1. Restart your agent session first. A session started before the install will not see the new skill.
2. Run the same install command again. It overwrites the old copy, so re-running it is also how you update.
3. Check that the folder is named `goodndood` and contains `SKILL.md`, at the path above.

## No terminal? No Node.js?

Use the MCP server instead. It needs no install at all, just this snippet pasted into your agent config:

```json
{
  "mcpServers": {
    "goodndood": {
      "url": "https://goodndood.my.id/mcp"
    }
  }
}
```

Or ask your agent to read the Skill directly at https://goodndood.my.id/skills/goodndood/SKILL.md

## Manual fallback, only if the command fails

```bash
git clone https://github.com/GoodnDood/goodndood-skills.git
cp -r goodndood-skills/skills/goodndood .agents/skills/goodndood
```

## Two ways to use GoodnDood

1. **Skill (this repo):** follow the procedure in `SKILL.md` - search the public catalog, pick a free preview, use it with attribution.
2. **MCP server:** connect `https://goodndood.my.id/mcp` (Streamable HTTP, no account, no API key) and use its four free tools: `search_assets`, `list_packs`, `get_asset`, `get_license_info`.

Both paths serve the same free artwork: 800px WebP previews for non-commercial use with attribution to GoodnDood. Full-resolution PNG files and commercial use without attribution are premium, bought on the [GoodnDood Adobe Stock profile](https://stock.adobe.com/contributor/213699125/GoodnDood).

## Source of truth

This repository is the single source of truth for the Skill. The GoodnDood website does not store a source copy of `SKILL.md`; it serves this file by proxying GitHub with an edge cache, so updating this repo updates the website automatically.
