# claude-marketplace

A personal [Claude Code](https://code.claude.com) plugin marketplace.

This repo is only the catalog: each plugin lives in its own repository and is
referenced from [`.claude-plugin/marketplace.json`](.claude-plugin/marketplace.json).

## Plugins

| Plugin | Version | Description |
| --- | --- | --- |
| [time-aware](https://github.com/jrosiek/claude-time-aware) | v0.1.0 | Timestamps every user prompt so Claude can track elapsed time and make time-aware decisions |

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
       "repo": "jrosiek/<plugin-name>",
       "ref": "v<version>"
     },
     "description": "What the plugin does"
   }
   ```

   Every plugin is pinned to a release tag (`ref`), so pushes to a plugin's `main` reach no one until the entry here is updated.

3. Validate:

   ```
   claude plugin validate .
   ```

4. Commit and push; users pick it up with `/plugin marketplace update jrosiek-marketplace`.

## Releasing a new plugin version

1. In the plugin repo: bump `version` in `.claude-plugin/plugin.json`, commit,
   tag `v<version>` and push the commit and the tag.
2. Here: set `ref` to the new tag, update the table above, then validate,
   commit and push.
