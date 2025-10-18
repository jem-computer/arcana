# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Arcana is a Claude Code plugin that provides Major Arcana tarot archetypes for symbolic and archetypal reasoning in AI agents. This is a documentation-only plugin (no executable code) that extends Claude agents with archetypal reasoning capabilities.

## Repository Architecture

### Plugin Structure

This repository follows the Claude Code plugin format:

```
.claude-plugin/
  plugin.json          # Plugin metadata (name, version, description)
skills/
  tarot/
    SKILL.md          # Main skill with usage instructions
    spreads.md        # Spread patterns (Three Card, Celtic Cross, etc.)
    cards/            # 22 Major Arcana card files (00-21)
      00-the-fool.md
      ...
      21-the-world.md
```

### Key Concepts

**Skills**: Claude Code skills are markdown-based instruction sets that agents can invoke. The tarot skill enables agents to use archetypal reasoning by "drawing" cards and synthesizing their symbolic meanings.

**Card Files**: Each of the 22 Major Arcana cards has a dedicated markdown file containing:
- Traditional divinatory meanings (upright/reversed)
- Archetypal psychology patterns
- Symbolic correspondences (elements, astrology, mythology)
- Narrative/journey context (relationship to other cards)

**Spreads**: Structured patterns for card interpretation (Single Card, Three Card, Five Card Cross, Seven Card Horseshoe, Celtic Cross)

### Two Interaction Modes

1. **Simulated Draws**: Perform tarot spreads for multiple archetypal perspectives. Agents select cards using timestamp-based or thematic methods.

2. **Question-Based Oracle**: Ask specific questions and receive relevant cards based on thematic/symbolic matching.

## Development Commands

This is a documentation-only plugin with no build process, tests, or compilation steps.

### Plugin Management

```bash
# Install plugin locally for testing
claude plugin install /path/to/arcana

# Install from GitHub (once published)
claude plugin install jem-computer/arcana
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

## Content Structure Standards

### Card Files

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
- Card reference list with quick keywords

## When Adding New Cards or Content

1. **Minor Arcana**: Would add 56 cards in four suits (Wands, Cups, Swords, Pentacles). Structure as `cards/minor/{suit}/{card-name}.md`

2. **Court Cards**: 16 cards (Page, Knight, Queen, King × 4 suits). These represent character archetypes rather than journey stages.

3. **New Spreads**: Add to `spreads.md` with positions, use cases, interpretation guidelines, and ASCII layout.

4. **Cross-References**: When adding cards, note relationships to existing cards in the "Narrative/Journey Context" section.

## Plugin Metadata

Defined in `.claude-plugin/plugin.json`:
- `name`: Plugin identifier (used in installation commands)
- `version`: Semantic versioning (current: 0.1.0)
- `description`: Brief description shown when browsing plugins
- `author`: Plugin creator info
