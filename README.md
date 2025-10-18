# Arcana - Claude Tarot Plugin

A Claude Code plugin that provides Major Arcana tarot archetypes for symbolic and archetypal reasoning in AI agents.

## Overview

This plugin enables Claude agents to use the 22 Major Arcana cards from tarot as a framework for archetypal and symbolic reasoning. Agents can perform tarot spreads for multiple perspectives or ask questions to receive relevant archetypal guidance.

## Installation

Install this plugin in Claude Code:

```bash
# From GitHub (once published)
claude plugin install jem-computer/arcana

# Or from local directory
claude plugin install /path/to/arcana
```

## Usage

Once installed, agents can access the tarot skill:

```markdown
I'm using the tarot skill to gain archetypal perspective on this architecture decision.

Performing a Three Card spread:
- Past: The Hierophant (established patterns)
- Present: The Tower (necessary disruption)
- Future: The Star (emerging clarity)
```

### Two Interaction Modes

**1. Simulated Draws**: Perform spreads (Three Card, Celtic Cross, etc.) to explore problems through multiple archetypal lenses

**2. Question-Based Oracle**: Ask specific questions and receive relevant card guidance based on thematic matching

## What's Included

- **22 Major Arcana Cards**: Complete archetypal wisdom for each card including:
  - Traditional divinatory meanings
  - Archetypal psychology
  - Symbolic correspondences
  - Narrative/journey context

- **Tarot Spreads**: Reference guide for spread patterns including Three Card, Five Card Cross, Seven Card Horseshoe, and Celtic Cross

- **Agent Instructions**: Clear guidance on when and how to use tarot for symbolic reasoning

## File Structure

```
skills/tarot/
├── SKILL.md           # Main skill file with usage instructions
├── spreads.md         # Spread patterns and positions
└── cards/             # Individual card files (00-21)
```

## When Agents Use This

Agents use tarot for:
- Symbolic/archetypal reasoning about complex problems
- Exploring multiple perspectives on ambiguous situations
- Understanding patterns and cycles
- Creative problem-solving requiring lateral thinking
- Framing decisions through archetypal lenses

Agents do NOT use tarot for:
- Precise technical calculations
- Binary true/false determinations
- Debugging code errors
- Literal predictions

## Contributing

Contributions welcome! Potential areas for expansion:
- Minor Arcana (56 cards in four suits)
- Court Cards as character archetypes
- Additional spread patterns
- Deeper symbolic cross-references

## License

MIT License - See LICENSE file for details

## Acknowledgments

Tarot wisdom drawn from Rider-Waite-Smith tradition, Jungian archetypal psychology, and various esoteric traditions.
