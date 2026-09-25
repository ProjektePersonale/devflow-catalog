# devflow-catalog

Remote **Marketplace** catalog for [DevFlow](https://github.com/ProjektePersonale/devflow).

`catalog.json` is a JSON array of marketplace entries (`skill` | `plugin` | `mcp`) with the same
shape as DevFlow's built-in seed. DevFlow appends it over the seed and dedupes by `type+name`
(remote wins), so entries here can update or extend the built-ins.

## Use it

DevFlow → Settings → Extensions → Marketplace, or set:

```jsonc
// ~/.devflow/settings.json
{ "marketplaceUrl": "https://raw.githubusercontent.com/ProjektePersonale/devflow-catalog/main/catalog.json" }
```

## Contribute an entry

Add an object to the array (or open a PR):

```jsonc
{
  "type": "skill",            // "skill" | "plugin" | "mcp"
  "name": "my-skill",
  "title": "My Skill",
  "description": "One line.",
  "version": "1.0.0",
  "author": "you",
  "content": "description: …\n…"                    // skill: inline markdown
  // "manifest": { "name": "…", "description": "…", "command": "…", "args": [] }   // plugin
  // "mcpConfig": { "command": "…", "args": [] }                                   // mcp (or url/headers)
}
```

Security note: plugin manifests and MCP configs execute commands on the installer's machine —
review before installing (DevFlow shows the payload before Install).
