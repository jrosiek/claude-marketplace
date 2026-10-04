# claude-marketplace

A personal [Claude Code](https://code.claude.com) plugin marketplace.

This repo is only the catalog: each plugin lives in its own repository and is
referenced from [`.claude-plugin/marketplace.json`](.claude-plugin/marketplace.json).

No plugins are published yet.

## Install

Add the marketplace in Claude Code:

```
/plugin marketplace add jrosiek/claude-marketplace
```

Then browse and install plugins:

```
/plugin install <plugin-name>@jrosiek-marketplace
```

## Adding a plugin

1. Create the plugin in its own repo (e.g. `jrosiek/<plugin-name>`) with a
   `.claude-plugin/plugin.json` manifest at its root.
2. Register it in `.claude-plugin/marketplace.json`:

   ```json
   {
     "name": "<plugin-name>",
     "source": {
       "source": "github",
       "repo": "jrosiek/<plugin-name>"
     },
     "description": "What the plugin does"
   }
   ```

   Optionally pin a version with `"ref": "<tag-or-branch>"` or `"sha": "<commit>"`
   inside `source`. For non-GitHub hosts use `"source": "url"` with
   `"url": "https://…/<plugin-name>.git"`.

3. Validate:

   ```
   claude plugin validate .
   ```

4. Commit and push; users pick it up with `/plugin marketplace update jrosiek-marketplace`.
