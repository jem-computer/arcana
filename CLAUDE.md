# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Esoterica is a Claude Code plugin marketplace - a grimoire providing esoteric tools for symbolic and archetypal reasoning in AI agents. The marketplace currently contains one plugin (Tarot) with plans for additional symbolic reasoning frameworks.

## Repository Architecture

### Marketplace Structure

This repository follows the Claude Code marketplace format:

```
.claude-plugin/
  marketplace.json      # Marketplace metadata and plugin catalog
plugins/
  tarot/               # Tarot plugin
    plugin.json        # Plugin metadata
    skills/tarot/      # Skill directory (required for plugins)
      SKILL.md         # Main skill with usage instructions
      spreads.md       # Spread patterns (Three Card, Celtic Cross, etc.)
      cards/           # 22 Major Arcana card files (00-21)
        00-the-fool.md
        ...
        21-the-world.md
```

### Key Concepts

**Marketplace**: A JSON catalog that lists available plugins and their sources. Users add the marketplace with `/plugin marketplace add jem-computer/arcana`, then install individual plugins with `/plugin install tarot@esoterica`.

**Skills**: Claude Code skills are markdown-based instruction sets that agents can invoke. The tarot skill enables agents to use archetypal reasoning by "drawing" cards and synthesizing their symbolic meanings.

**Card Files**: Each of the 22 Major Arcana cards has a dedicated markdown file containing:
- Traditional divinatory meanings (upright/reversed)
- Archetypal psychology patterns
- Symbolic correspondences (elements, astrology, mythology)
- Narrative/journey context (relationship to other cards)

**Spreads**: Structured patterns for card interpretation (Single Card, Three Card, Five Card Cross, Seven Card Horseshoe, Celtic Cross)

### Tarot Plugin Interaction Modes

1. **Simulated Draws**: Perform tarot spreads for multiple archetypal perspectives. Agents select cards using Fisher-Yates shuffle with timestamp-based seed.

2. **Question-Based Oracle**: Ask specific questions and receive relevant cards based on thematic/symbolic matching.

## Development Commands

This is a documentation-only marketplace with no build process, tests, or compilation steps.

### Marketplace Management

```bash
# Add marketplace locally for testing
/plugin marketplace add /path/to/arcana

# Install tarot plugin from local marketplace
/plugin install tarot@esoterica

# Add marketplace from GitHub (once published)
/plugin marketplace add jem-computer/arcana
```

### Git Workflow

```bash
# View status
git status

# Add and commit changes
git add .
git commit -m "feat: description of changes"

# Push to remote
git push origin main
```

## File Naming Conventions

- Card files: `cards/{number}-{card-name}.md` where number is zero-padded (00-21)
- Skill files: `SKILL.md` (uppercase, per Claude Code conventions)
- Supporting docs: lowercase with hyphens (`spreads.md`)
- Plugin metadata: `plugin.json` (in each plugin directory)
- Marketplace metadata: `marketplace.json` (in `.claude-plugin/` directory)

## Content Structure Standards

### Tarot Card Files

Each card file follows a consistent four-section structure:

1. **Traditional Divinatory Meanings**: Upright/reversed meanings, keywords
2. **Archetypal Psychology**: Core archetype, psychological patterns, shadow aspects, integration
3. **Symbolic Correspondences**: Element, astrology, numerology, colors, symbols, mythology
4. **Narrative/Journey Context**: Position in Fool's Journey, story arc, relationship to other cards, when archetype appears

### Skill File (SKILL.md)

- Front matter with `name` and `description`
- Overview and usage guidelines
- Announcement pattern for agents
- Detailed interaction modes
- Card selection methods (Fisher-Yates shuffle algorithm)
- Card reference list with quick keywords

## When Adding New Content

### Expanding the Tarot Plugin

1. **Minor Arcana**: Would add 56 cards in four suits (Wands, Cups, Swords, Pentacles). Structure as `plugins/tarot/skills/tarot/cards/minor/{suit}/{card-name}.md`

2. **Court Cards**: 16 cards (Page, Knight, Queen, King × 4 suits). These represent character archetypes rather than journey stages.

3. **New Spreads**: Add to `spreads.md` with positions, use cases, interpretation guidelines, and ASCII layout.

4. **Cross-References**: When adding cards, note relationships to existing cards in the "Narrative/Journey Context" section.

### Adding New Plugins to the Marketplace

When creating a new esoteric reasoning plugin (I Ching, Kabbalah, Alchemy, etc.):

1. Create `plugins/{plugin-name}/` directory
2. Add `plugin.json` with metadata
3. Create `plugins/{plugin-name}/skills/{plugin-name}/` directory
4. Add `SKILL.md` and supporting content files in the skills directory
5. Update `.claude-plugin/marketplace.json` to include the new plugin in the `plugins` array
6. Update README.md to document the new plugin

## Metadata Files

### Marketplace Metadata

Defined in `.claude-plugin/marketplace.json`:
- `name`: Marketplace identifier ("esoterica")
- `owner`: Marketplace maintainer info
- `metadata.description`: Brief marketplace description
- `metadata.version`: Marketplace version
- `plugins`: Array of plugin definitions with sources

### Plugin Metadata

Defined in each `plugins/{name}/plugin.json`:
- `name`: Plugin identifier (e.g., "tarot")
- `version`: Semantic versioning (current: 0.1.0)
- `description`: Brief description shown when browsing plugins
- `author`: Plugin creator info
- `license`: Software license (MIT)
