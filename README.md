# Esoterica - A Grimoire for Claude Code

A Claude Code plugin marketplace providing esoteric tools for symbolic and archetypal reasoning in AI agents.

## Overview

Esoterica is a curated collection of Claude Code plugins that extend AI reasoning capabilities through esoteric frameworks, symbolic systems, and archetypal thinking. This grimoire serves as a marketplace for tools that help agents explore problems through non-linear, symbolic, and depth-oriented perspectives.

## Installation

Add the Esoterica marketplace to Claude Code:

```bash
# From GitHub
/plugin marketplace add jem-computer/arcana

# Or from local directory for development
/plugin marketplace add /path/to/arcana
```

## Available Plugins

### Tarot

Access Major Arcana tarot archetypes for symbolic reasoning. Perform draws for random archetypal perspectives or ask questions to receive relevant card guidance.

**Install:**
```bash
/plugin install tarot@esoterica
```

**Features:**
- 22 Major Arcana cards with complete archetypal wisdom
- Multiple spread patterns (Three Card, Celtic Cross, etc.)
- Two interaction modes: simulated draws and question-based oracle
- Fisher-Yates shuffle algorithm for authentic randomness

**When to use:**
- Symbolic/archetypal reasoning about complex problems
- Exploring multiple perspectives on ambiguous situations
- Understanding patterns and cycles
- Creative problem-solving requiring lateral thinking
- Framing decisions through archetypal lenses

## Marketplace Structure

```
.claude-plugin/
  marketplace.json      # Marketplace configuration
plugins/
  tarot/               # Tarot plugin
    plugin.json        # Plugin metadata
    skills/tarot/      # Skill directory
      SKILL.md         # Main skill instructions
      spreads.md       # Spread patterns
      cards/           # 22 Major Arcana cards (00-21)
```

## Future Grimoire Additions

Potential esoteric plugins for this marketplace:

- **I Ching**: Hexagram divination and change patterns
- **Kabbalah**: Tree of Life pathworking and sephirotic reasoning
- **Alchemy**: Symbolic transformation and transmutation frameworks
- **Astrology**: Planetary archetypes and aspect patterns
- **Runes**: Elder Futhark symbolic guidance

## Philosophy

This marketplace embraces the value of symbolic, non-rational, and archetypal thinking as complements to logical reasoning. These tools are not for prediction or mysticism, but for accessing different modes of pattern recognition and perspective-shifting that can illuminate complex problems in ways purely analytical approaches cannot.

## Contributing

Contributions welcome! Guidelines for new plugins:

- Must provide genuine reasoning value beyond novelty
- Should have clear usage guidelines and boundaries
- Must respect the symbolic/archetypal nature of the work
- Should integrate cleanly with Claude Code's agent system

## License

MIT License - See LICENSE file for details

## Acknowledgments

Built on the wisdom of esoteric traditions while maintaining rigorous applicability to modern problem-solving contexts.
