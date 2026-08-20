# Installing the Product Leadership Skills plugin

This repository is packaged as a single Claude Code plugin (`product-leadership-skills`) containing all seven skills listed in [skills/README.md](skills/README.md). Installing the plugin makes every skill available in any project without copying files into `.claude/skills/`.

## Install

In Claude Code, run:

```
/plugin marketplace add AndyMelnykov/product_leadership_skills
/plugin install product-leadership-skills@product-leadership-skills
```

(The first argument to `marketplace add` can also be a full git URL or a local path to this repo, e.g. `/plugin marketplace add /path/to/product_leadership_skills`.)

Restart Claude Code (or run `/plugin` to check status) if the skills don't show up immediately.

## Verify

Run `/plugin` and confirm `product-leadership-skills` is listed as installed and enabled, or ask Claude to list its available skills — you should see `synthesize-research`, `user-research`, `write-feature-spec`, `stakeholder-alignment-brief`, `prep-competency-review`, `build-dashboard`, and `data-visualization`.

## Update

When this repo changes, refresh the marketplace and reinstall:

```
/plugin marketplace update product-leadership-skills
/plugin install product-leadership-skills@product-leadership-skills
```

## Uninstall

```
/plugin uninstall product-leadership-skills@product-leadership-skills
```

## Layout reference

```
.claude-plugin/
  plugin.json        # plugin manifest (name, description, version)
  marketplace.json    # lets this repo be added directly via /plugin marketplace add
skills/
  README.md           # competency-model mapping for each skill
  <skill-name>/SKILL.md
```
