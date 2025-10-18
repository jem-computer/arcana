# Major Arcana Tarot Plugin Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use executing-plans to implement this plan task-by-task.

**Goal:** Create a Claude Code plugin that provides Major Arcana tarot archetypes for symbolic and archetypal reasoning in agents.

**Architecture:** Modular skill-based plugin with main SKILL.md orchestrating draws/spreads, 22 individual card markdown files containing archetypal wisdom, and a spreads reference. Uses Claude Code plugin manifest for distribution.

**Tech Stack:** Markdown, YAML frontmatter, Claude Code Plugin system

---

## Task 1: Create Plugin Manifest

**Files:**
- Create: `.claude-plugin/plugin.json`

**Step 1: Create plugin metadata directory**

Run: `mkdir -p .claude-plugin`

**Step 2: Write plugin.json**

Create `.claude-plugin/plugin.json`:

```json
{
  "name": "claude-tarot",
  "description": "Major Arcana tarot archetypes for symbolic and archetypal reasoning in agents",
  "version": "0.1.0",
  "author": {
    "name": "111ecosystem"
  }
}
```

**Step 3: Verify JSON is valid**

Run: `cat .claude-plugin/plugin.json | python3 -m json.tool`
Expected: Valid JSON output with no errors

**Step 4: Commit**

```bash
git add .claude-plugin/plugin.json
git commit -m "feat: add plugin manifest"
```

---

## Task 2: Create Skills Directory Structure

**Files:**
- Create: `skills/tarot/` directory
- Create: `skills/tarot/cards/` directory

**Step 1: Create directory structure**

Run: `mkdir -p skills/tarot/cards`

**Step 2: Verify directories exist**

Run: `ls -la skills/tarot/`
Expected: Directory exists with cards/ subdirectory

**Step 3: Commit**

```bash
git add skills/
git commit -m "feat: create tarot skill directory structure"
```

---

## Task 3: Create Main SKILL.md

**Files:**
- Create: `skills/tarot/SKILL.md`

**Step 1: Write SKILL.md with YAML frontmatter and instructions**

Create `skills/tarot/SKILL.md`:

```markdown
---
name: tarot
description: Access Major Arcana tarot archetypes for symbolic reasoning. Perform draws for random archetypal perspectives or ask questions to receive relevant card guidance.
---

# Tarot: Major Arcana Archetypal Reasoning

## Overview

This skill provides access to the 22 Major Arcana archetypes from tarot for symbolic and archetypal reasoning. Use this when you need to explore problems through symbolic lenses, understand patterns through archetypal frameworks, or gain multiple perspectives on complex decisions.

## When to Use This Skill

**Use tarot for:**
- Symbolic/archetypal reasoning about complex problems
- Exploring multiple perspectives on ambiguous situations
- Understanding patterns and cycles in systems or processes
- Creative problem-solving requiring lateral thinking
- Framing decisions through archetypal lenses

**Do NOT use tarot for:**
- Precise technical calculations
- Binary true/false determinations
- Situations requiring deterministic answers
- Debugging specific code errors
- Literal predictions or fortune-telling

## Announcement Pattern

When using this skill, announce:

"I'm using the tarot skill to [gain archetypal perspective on X / perform a spread for Y / explore symbolic patterns in Z]"

## Interaction Mode 1: Simulated Draws

Perform a tarot spread when you need multiple archetypal perspectives on a complex problem.

**How to perform a draw:**

1. Choose a spread from `spreads.md` appropriate to your question complexity
2. Generate card positions using one of these methods:
   - Timestamp-based: Use current timestamp modulo 22 for each position
   - Sequential: Use systematic selection based on question keywords
   - Random selection: Choose cards that feel relevant to the query
3. Read the corresponding card files from `cards/` directory
4. Synthesize the archetypal meanings in context of spread positions
5. Apply symbolic insights to your reasoning process

**Example:**

```
I'm using the tarot skill with a Three Card spread to explore this microservices architecture decision.

Drawing cards using timestamp method:
- Past (Position 1): Card 5 - The Hierophant
- Present (Position 2): Card 16 - The Tower
- Future (Position 3): Card 17 - The Star

Reading cards/05-the-hierophant.md...
Reading cards/16-the-tower.md...
Reading cards/17-the-star.md...

Archetypal interpretation:
- The Hierophant (Past): Established patterns, traditional monolithic architecture
- The Tower (Present): Disruption, breaking down the monolith, necessary chaos
- The Star (Future): Clarity emerging, optimized distributed system

This suggests honoring the wisdom of our established architecture while embracing
the necessary disruption of decomposition, with clarity and optimization as the goal.
```

## Interaction Mode 2: Question-Based Oracle

Ask a specific question and receive relevant card(s) based on thematic/symbolic matching.

**How to ask the oracle:**

1. Formulate a clear question about your problem
2. Identify 1-3 cards whose themes relate to the question
3. Read those card files
4. Apply archetypal wisdom to your situation

**Example:**

```
I'm using the tarot skill to ask: "What archetype relates to balancing
creative freedom with structured constraints?"

Relevant cards:
- The Magician (Card 1): Mastery, using tools, focused will
- Temperance (Card 14): Balance, integration, harmonizing opposites

Reading cards/01-the-magician.md...
Reading cards/14-temperance.md...

The Magician suggests mastery comes from skillfully wielding tools and constraints
as instruments of creation. Temperance suggests the answer lies not in choosing
one over the other, but in finding the alchemical balance point where structure
enables rather than limits creativity.
```

## Card Selection Methods

**For Random Draws:**
- Timestamp: `(Date.now() % 22)` gives card 0-21
- Multiple cards: Use sequential timestamps or add position index
- Avoid duplicates: Track drawn cards, re-roll if duplicate

**For Question-Based:**
- Identify key themes in your question (e.g., "beginning," "transformation," "wisdom")
- Match themes to card keywords in card files
- Select 1-3 most relevant cards

## Interpreting Cards in Context

When reading cards:

1. **Start with traditional meanings**: What is the core divinatory message?
2. **Explore archetypal psychology**: What psychological pattern does this represent?
3. **Note symbolic correspondences**: What elements/symbols/myths connect to your problem?
4. **Consider narrative context**: Where does this fit in the journey? What comes before/after?
5. **Synthesize**: How do these layers apply to your specific situation?

## Card Reference

All 22 Major Arcana cards are available in `cards/`:

- 00: The Fool - Beginnings, potential, leap of faith
- 01: The Magician - Mastery, will, manifestation
- 02: The High Priestess - Intuition, mystery, inner knowledge
- 03: The Empress - Abundance, nurturing, creativity
- 04: The Emperor - Structure, authority, stability
- 05: The Hierophant - Tradition, teaching, established wisdom
- 06: The Lovers - Choice, union, values alignment
- 07: The Chariot - Willpower, determination, victory
- 08: Strength - Courage, compassion, inner power
- 09: The Hermit - Introspection, solitude, inner guidance
- 10: Wheel of Fortune - Cycles, fate, turning points
- 11: Justice - Balance, fairness, cause and effect
- 12: The Hanged Man - Surrender, new perspective, pause
- 13: Death - Transformation, endings, rebirth
- 14: Temperance - Balance, moderation, integration
- 15: The Devil - Bondage, materialism, shadow
- 16: The Tower - Disruption, revelation, breaking down
- 17: The Star - Hope, inspiration, clarity
- 18: The Moon - Illusion, intuition, the unconscious
- 19: The Sun - Joy, success, vitality
- 20: Judgement - Awakening, reckoning, renewal
- 21: The World - Completion, integration, wholeness

## See Also

- `spreads.md` - Detailed spread patterns and positions
- `cards/*.md` - Individual card archetypal wisdom
```

**Step 2: Verify SKILL.md exists and has valid frontmatter**

Run: `head -5 skills/tarot/SKILL.md`
Expected: Should show YAML frontmatter with `name: tarot` and description

**Step 3: Commit**

```bash
git add skills/tarot/SKILL.md
git commit -m "feat: add main tarot SKILL.md with agent instructions"
```

---

## Task 4: Create Spreads Reference

**Files:**
- Create: `skills/tarot/spreads.md`

**Step 1: Write spreads.md**

Create `skills/tarot/spreads.md`:

```markdown
# Tarot Spreads

## Three Card Spread

**Positions**:
1. Past / Situation / Thesis
2. Present / Challenge / Antithesis
3. Future / Outcome / Synthesis

**Use When**: Quick insight needed, exploring progression or dialectic, time-based analysis

**How to Interpret**:
- Read cards in sequence, noting the progression from past through present to future
- Look for relationships between positions: How does the past inform the present? How do both shape the future?
- Consider the dialectic: How do thesis and antithesis resolve in synthesis?

**Layout**:
```
    [3]
[1] [2]
```

---

## Five Card Cross Spread

**Positions**:
1. Present situation (center)
2. Challenge/obstacle (left)
3. Distant past/foundation (bottom)
4. Recent past/influence (right)
5. Potential outcome (top)

**Use When**: Deeper context needed, understanding obstacles, examining foundations

**How to Interpret**:
- Start with position 1 (present) as your anchor
- Examine position 3 (foundation) to understand deep roots
- Note position 4 (recent past) as immediate influences
- Identify position 2 (challenge) as what must be addressed
- Consider position 5 (outcome) as potential if current trajectory continues

**Layout**:
```
    [5]
[2] [1] [4]
    [3]
```

---

## Seven Card Horseshoe

**Positions**:
1. Past
2. Present
3. Hidden Influences
4. Obstacles
5. External Forces
6. Advice
7. Likely Outcome

**Use When**: Complex decision-making, multiple factors at play, need comprehensive view

**How to Interpret**:
- Positions 1-2: Establish temporal context
- Positions 3-5: Identify forces at play (hidden, blocking, external)
- Position 6: Synthesize guidance from the archetypes
- Position 7: Understand likely trajectory

**Layout**:
```
[1] [2] [3] [4] [5] [6] [7]
```

---

## Celtic Cross (Advanced)

**Positions**:
1. Present situation (center)
2. Challenge/crossing (across center)
3. Distant past/foundation (below)
4. Recent past (left)
5. Potential future (above)
6. Near future (right)
7. Your approach (bottom of staff)
8. External influences (second on staff)
9. Hopes and fears (third on staff)
10. Likely outcome (top of staff)

**Use When**: Maximum depth needed, major life/project decisions, comprehensive analysis

**How to Interpret**:
- The Cross (1-6): Current situation in temporal context
- The Staff (7-10): Your inner world and trajectory
- Read cross first, then staff
- Look for patterns, repeated themes, complementary archetypes

**Layout**:
```
        [5]
            [10]
[4]  [1][2]  [6]
            [9]
        [3]
            [8]
            [7]
```

---

## Single Card Draw

**Position**:
1. Guidance / Theme / Focus

**Use When**: Quick archetypal perspective, daily guidance, focusing question

**How to Interpret**:
- Let the card speak to your specific question
- Consider all four dimensions: traditional meaning, archetypal psychology, correspondences, narrative context
- Ask: How does this archetype relate to my situation?
```

**Step 2: Verify spreads.md exists**

Run: `cat skills/tarot/spreads.md | head -20`
Expected: File shows spread patterns with positions

**Step 3: Commit**

```bash
git add skills/tarot/spreads.md
git commit -m "feat: add tarot spreads reference"
```

---

## Task 5: Create Card 00 - The Fool

**Files:**
- Create: `skills/tarot/cards/00-the-fool.md`

**Step 1: Write The Fool card file**

Create `skills/tarot/cards/00-the-fool.md`:

```markdown
# 0 - The Fool

## Traditional Divinatory Meanings

**Upright**: New beginnings, innocence, spontaneity, free spirit, originality, adventure, idealism, lack of commitment, infinite potential

**Reversed**: Recklessness, foolishness, risk-taking without preparation, naivety, poor judgment, chaos, immaturity, missing obvious dangers

**Keywords**: Beginning, potential, faith, trust, openness, leap, innocent

## Archetypal Psychology

**Core Archetype**: The Innocent, the Divine Child, the seeker at the beginning of the journey, the one who has not yet been shaped by experience

**Psychological Pattern**: Pre-ego consciousness, the state before differentiation and categorization, pure potential unburdened by past experience or future anxiety. Represents the part of the psyche willing to take leaps of faith into the unknown. The beginner's mind that sees possibilities where experience sees obstacles.

**Shadow Aspects**: Denial of consequences, spiritual bypassing (staying in eternal beginning to avoid commitment), refusal to learn from experience, perpetual immaturity, willful ignorance, recklessness masked as spontaneity

**Integration**: Learning to balance innocence with wisdom, maintaining openness and wonder while developing discernment and responsibility, staying curious without being naive

## Symbolic Correspondences

**Element**: Air (though sometimes associated with spirit/ether)
**Astrological**: Uranus (radical freedom, breakthrough, revolution)
**Numerology**: 0 (infinite potential, the void, the unmanifest, all possibilities)
**Colors**: Yellow (optimism, consciousness), sky blue (openness), white (purity, blank slate)
**Symbols**:
- Cliff edge (threshold, leap of faith)
- Knapsack (minimal baggage, traveling light)
- White rose (purity of intent)
- Small dog (instinct, loyal companion)
- Mountains (future challenges ahead)
- Sun (optimism, blessing)

**Mythological**: Parsifal (the Holy Fool), Dionysus (divine madness), the Trickster archetype, the Sacred Clown, Heyoka

## Narrative/Journey Context

**Position in Fool's Journey**: The beginning - numbered as both 0 and sometimes placed after The World (21) to show the eternal return, the cycle beginning again

**Story Arc**: The Fool steps off the cliff into the unknown, beginning the journey of individuation and self-discovery. Carries only what is essential, unburdened by possessions or preconceptions. Has not yet encountered the teachers, challenges, and transformations ahead. This is the moment before the journey, full of potential.

**Relationship to Other Cards**:
- Precedes The Magician: Raw potential → focused will and skill
- Mirrors The World: Journey's beginning ↔ journey's completion (alpha and omega)
- Contrasts The Hermit: External exploration vs internal wisdom
- Initiates what Death transforms and The Tower disrupts

**When This Archetype Appears**:
- Starting new projects or ventures
- Major life transitions (career change, relocation, relationships)
- Moments requiring faith and trust in the unknown
- Creative genesis and brainstorming
- Paradigm shifts and new ways of seeing
- Times when overthinking blocks action
- Need to approach with beginner's mind
```

**Step 2: Verify card file exists and is properly formatted**

Run: `head -30 skills/tarot/cards/00-the-fool.md`
Expected: Shows card title and sections

**Step 3: Commit**

```bash
git add skills/tarot/cards/00-the-fool.md
git commit -m "feat: add Major Arcana card 00 - The Fool"
```

---

## Task 6: Create Card 01 - The Magician

**Files:**
- Create: `skills/tarot/cards/01-the-magician.md`

**Step 1: Write The Magician card file**

Create `skills/tarot/cards/01-the-magician.md`:

```markdown
# 1 - The Magician

## Traditional Divinatory Meanings

**Upright**: Manifestation, power, skill, concentration, action, resourcefulness, willpower, mastery, "as above, so below"

**Reversed**: Manipulation, cunning, trickery, unused abilities, lack of focus, wasted talent, illusion, deceit

**Keywords**: Mastery, will, manifestation, tools, skill, focus, power, action

## Archetypal Psychology

**Core Archetype**: The Magician, the Creator, the Master of Tools, the one who channels will into manifestation

**Psychological Pattern**: Focused consciousness and directed will. The ability to take raw potential (The Fool's energy) and channel it through skill, tools, and intention into concrete reality. Represents the part of psyche that knows "I can make this happen" and possesses the skills to do so. The conscious mind directing the unconscious toward specific ends.

**Shadow Aspects**: Manipulation (using skills to deceive or control), trickery without ethical foundation, scattered focus trying to master everything and mastering nothing, impostor syndrome hiding real mastery, using talent for selfish ends only

**Integration**: Developing genuine skill through practice, ethical use of personal power, focusing will without rigidity, balancing mastery with humility, using abilities in service of wholeness

## Symbolic Correspondences

**Element**: Air (or Mercury - messenger, communicator, quick)
**Astrological**: Mercury (communication, skill, commerce, trickery)
**Numerology**: 1 (beginning, unity, focused will, individuality)
**Colors**: Red (action, passion), white (purity of intent), yellow (conscious mind, intellect)
**Symbols**:
- Infinity symbol (∞) above head (connection to infinite source)
- Pointing up with one hand, down with other ("as above, so below" - bridging heaven/earth)
- Four tools on table (Wands, Cups, Swords, Pentacles - all elements at disposal)
- Roses and lilies (desire and pure thought)
- Snake belt (ouroboros, wisdom, transformation)

**Mythological**: Hermes/Mercury (messenger, trickster, guide), Prometheus (bringer of tools/fire), Thoth (wisdom, magic, writing)

## Narrative/Journey Context

**Position in Fool's Journey**: First encounter after beginning - The Fool meets the Magician who shows how to use will and skill

**Story Arc**: Having leaped into the unknown, The Fool now encounters mastery and skill. Learns that potential must be focused and channeled. Discovers the tools available and begins to understand manifestation through directed will.

**Relationship to Other Cards**:
- Follows The Fool: Potential → directed skill
- Precedes The High Priestess: Conscious mastery → unconscious wisdom
- Mirrors The Tower: Skillful construction vs destructive breakthrough
- Contrasts The Hanged Man: Action vs surrender

**When This Archetype Appears**:
- Need to focus scattered energy on specific goal
- Time to develop or demonstrate mastery
- Using tools and resources skillfully
- Manifestation and bringing ideas into reality
- Taking conscious, directed action
- Bridging concept and implementation
- Situations requiring concentration and will
```

**Step 2: Verify and commit**

Run: `wc -l skills/tarot/cards/01-the-magician.md`
Expected: File exists with substantial content

```bash
git add skills/tarot/cards/01-the-magician.md
git commit -m "feat: add Major Arcana card 01 - The Magician"
```

---

## Task 7: Create Card 02 - The High Priestess

**Files:**
- Create: `skills/tarot/cards/02-the-high-priestess.md`

**Step 1: Write The High Priestess card file**

Create `skills/tarot/cards/02-the-high-priestess.md`:

```markdown
# 2 - The High Priestess

## Traditional Divinatory Meanings

**Upright**: Intuition, sacred knowledge, divine feminine, the subconscious mind, mystery, higher powers, inner voice, hidden influences

**Reversed**: Secrets, disconnected from intuition, withdrawal, silence, repressed feelings, hidden agendas, surface knowledge only

**Keywords**: Intuition, mystery, inner knowledge, unconscious, hidden, sacred, receptive

## Archetypal Psychology

**Core Archetype**: The Wise Woman, the Oracle, the Guardian of Mysteries, the keeper of unconscious wisdom

**Psychological Pattern**: The unconscious mind, intuitive knowing that comes without rational process. Represents deep inner wisdom, the voice beneath conscious thought. The part of psyche that "just knows" without needing explanation. Receptive consciousness that listens rather than acts, perceives rather than manifests.

**Shadow Aspects**: Withdrawal from action into perpetual contemplation, hiding behind mystery to avoid engagement, secrets kept from self (repression), false mysticism, using "intuition" to avoid rational thinking when needed, gatekeeping knowledge

**Integration**: Trusting inner knowing while staying grounded, balancing intuition with reason, honoring mystery without romanticizing ignorance, accessing unconscious wisdom consciously

## Symbolic Correspondences

**Element**: Water (intuition, emotion, the unconscious)
**Astrological**: Moon (intuition, cycles, hidden realms, the unconscious)
**Numerology**: 2 (duality, balance, receptivity, the other)
**Colors**: Blue (depth, intuition, mystery), white (purity, spiritual truth), silver (moon, reflection)
**Symbols**:
- Pillars (B and J - Boaz and Jachin, duality, gateway to temple)
- Veil of pomegranates (hidden knowledge, fertility, mystery)
- Moon at feet (unconscious, cycles, intuition)
- Torah scroll (sacred knowledge, law, hidden wisdom)
- Crown (spiritual authority, Isis crown)
- Water (unconscious, emotion)

**Mythological**: Persephone (underworld guide), Isis (divine knowledge), Hecate (crossroads, mystery), Sophia (wisdom)

## Narrative/Journey Context

**Position in Fool's Journey**: Second teacher - after The Magician's active mastery, The Fool encounters receptive wisdom

**Story Arc**: The Fool learns that not all wisdom comes through action and will. Some knowledge can only be accessed through stillness, intuition, and receptivity. Discovers the unconscious realm and learns to listen to inner voice.

**Relationship to Other Cards**:
- Follows The Magician: Active doing → receptive being
- Balances The Magician: Conscious will ↔ unconscious wisdom
- Precedes The Empress: Inner knowledge → outer manifestation
- Mirrors The Hermit: Both seek wisdom, but she looks within to universal unconscious while he looks within to personal truth

**When This Archetype Appears**:
- Need to trust intuition over logic
- Hidden information or influences at play
- Time for introspection and inner listening
- Accessing unconscious wisdom
- Mystery that cannot be forced, only received
- Need for patience and receptivity
- Situations requiring subtle perception over direct action
```

**Step 2: Verify and commit**

```bash
git add skills/tarot/cards/02-the-high-priestess.md
git commit -m "feat: add Major Arcana card 02 - The High Priestess"
```

---

## Task 8-25: Create Remaining Major Arcana Cards

For brevity, I'll provide templates for the remaining 19 cards. Each follows the same structure.

### Card 03: The Empress

**File**: `skills/tarot/cards/03-the-empress.md`

**Content**: Abundance, nurturing, creativity, nature, fertility, motherhood, sensory experience
- **Archetype**: The Mother, The Creator, Nature
- **Element**: Earth
- **Astrological**: Venus

```bash
git add skills/tarot/cards/03-the-empress.md
git commit -m "feat: add Major Arcana card 03 - The Empress"
```

### Card 04: The Emperor

**File**: `skills/tarot/cards/04-the-emperor.md`

**Content**: Structure, authority, stability, fatherhood, leadership, control, rules, power
- **Archetype**: The Father, The Ruler, The Authority
- **Element**: Fire
- **Astrological**: Aries

```bash
git add skills/tarot/cards/04-the-emperor.md
git commit -m "feat: add Major Arcana card 04 - The Emperor"
```

### Card 05: The Hierophant

**File**: `skills/tarot/cards/05-the-hierophant.md`

**Content**: Tradition, conformity, teaching, institutions, spiritual authority, conventional wisdom, ceremony
- **Archetype**: The Teacher, The Pope, The Spiritual Authority
- **Element**: Earth
- **Astrological**: Taurus

```bash
git add skills/tarot/cards/05-the-hierophant.md
git commit -m "feat: add Major Arcana card 05 - The Hierophant"
```

### Card 06: The Lovers

**File**: `skills/tarot/cards/06-the-lovers.md`

**Content**: Choice, union, values, partnerships, alignment, love, harmony, relationships
- **Archetype**: The Lovers, The Choice
- **Element**: Air
- **Astrological**: Gemini

```bash
git add skills/tarot/cards/06-the-lovers.md
git commit -m "feat: add Major Arcana card 06 - The Lovers"
```

### Card 07: The Chariot

**File**: `skills/tarot/cards/07-the-chariot.md`

**Content**: Willpower, determination, victory, control, self-discipline, hard-won success, direction
- **Archetype**: The Warrior, The Victor
- **Element**: Water
- **Astrological**: Cancer

```bash
git add skills/tarot/cards/07-the-chariot.md
git commit -m "feat: add Major Arcana card 07 - The Chariot"
```

### Card 08: Strength

**File**: `skills/tarot/cards/08-strength.md`

**Content**: Courage, compassion, inner power, gentle control, patience, soft power, taming the beast within
- **Archetype**: The Hero, Inner Strength
- **Element**: Fire
- **Astrological**: Leo

```bash
git add skills/tarot/cards/08-strength.md
git commit -m "feat: add Major Arcana card 08 - Strength"
```

### Card 09: The Hermit

**File**: `skills/tarot/cards/09-the-hermit.md`

**Content**: Introspection, solitude, inner guidance, wisdom, soul searching, withdrawal, contemplation
- **Archetype**: The Wise Old Man, The Seeker
- **Element**: Earth
- **Astrological**: Virgo

```bash
git add skills/tarot/cards/09-the-hermit.md
git commit -m "feat: add Major Arcana card 09 - The Hermit"
```

### Card 10: Wheel of Fortune

**File**: `skills/tarot/cards/10-wheel-of-fortune.md`

**Content**: Cycles, fate, turning points, karma, luck, change, destiny, life cycles
- **Archetype**: Fate, The Wheel
- **Element**: Fire
- **Astrological**: Jupiter

```bash
git add skills/tarot/cards/10-wheel-of-fortune.md
git commit -m "feat: add Major Arcana card 10 - Wheel of Fortune"
```

### Card 11: Justice

**File**: `skills/tarot/cards/11-justice.md`

**Content**: Balance, fairness, truth, cause and effect, law, accountability, objectivity
- **Archetype**: Justice, The Judge
- **Element**: Air
- **Astrological**: Libra

```bash
git add skills/tarot/cards/11-justice.md
git commit -m "feat: add Major Arcana card 11 - Justice"
```

### Card 12: The Hanged Man

**File**: `skills/tarot/cards/12-the-hanged-man.md`

**Content**: Surrender, new perspective, pause, letting go, sacrifice, suspension, enlightenment through reversal
- **Archetype**: The Martyr, The Shaman
- **Element**: Water
- **Astrological**: Neptune

```bash
git add skills/tarot/cards/12-the-hanged-man.md
git commit -m "feat: add Major Arcana card 12 - The Hanged Man"
```

### Card 13: Death

**File**: `skills/tarot/cards/13-death.md`

**Content**: Transformation, endings, rebirth, transition, release, metamorphosis, necessary loss
- **Archetype**: The Transformer, Death as Change
- **Element**: Water
- **Astrological**: Scorpio

```bash
git add skills/tarot/cards/13-death.md
git commit -m "feat: add Major Arcana card 13 - Death"
```

### Card 14: Temperance

**File**: `skills/tarot/cards/14-temperance.md`

**Content**: Balance, moderation, integration, patience, alchemy, harmony, middle path
- **Archetype**: The Alchemist, The Healer
- **Element**: Fire
- **Astrological**: Sagittarius

```bash
git add skills/tarot/cards/14-temperance.md
git commit -m "feat: add Major Arcana card 14 - Temperance"
```

### Card 15: The Devil

**File**: `skills/tarot/cards/15-the-devil.md`

**Content**: Bondage, materialism, addiction, shadow, illusion of entrapment, attachments, temptation
- **Archetype**: The Shadow, The Bound Self
- **Element**: Earth
- **Astrological**: Capricorn

```bash
git add skills/tarot/cards/15-the-devil.md
git commit -m "feat: add Major Arcana card 15 - The Devil"
```

### Card 16: The Tower

**File**: `skills/tarot/cards/16-the-tower.md`

**Content**: Disruption, revelation, sudden change, breakthrough, breakdown, liberation through destruction
- **Archetype**: The Destroyer, Divine Lightning
- **Element**: Fire
- **Astrological**: Mars

```bash
git add skills/tarot/cards/16-the-tower.md
git commit -m "feat: add Major Arcana card 16 - The Tower"
```

### Card 17: The Star

**File**: `skills/tarot/cards/17-the-star.md`

**Content**: Hope, inspiration, clarity, healing, renewal, serenity, optimism, divine guidance
- **Archetype**: The Muse, Hope
- **Element**: Air
- **Astrological**: Aquarius

```bash
git add skills/tarot/cards/17-the-star.md
git commit -m "feat: add Major Arcana card 17 - The Star"
```

### Card 18: The Moon

**File**: `skills/tarot/cards/18-the-moon.md`

**Content**: Illusion, intuition, the unconscious, dreams, anxiety, what lurks beneath surface, shadow work
- **Archetype**: The Dream, The Unconscious
- **Element**: Water
- **Astrological**: Pisces

```bash
git add skills/tarot/cards/18-the-moon.md
git commit -m "feat: add Major Arcana card 18 - The Moon"
```

### Card 19: The Sun

**File**: `skills/tarot/cards/19-the-sun.md`

**Content**: Joy, success, vitality, confidence, clarity, celebration, achievement, radiance
- **Archetype**: The Divine Child, Joy
- **Element**: Fire
- **Astrological**: The Sun

```bash
git add skills/tarot/cards/19-the-sun.md
git commit -m "feat: add Major Arcana card 19 - The Sun"
```

### Card 20: Judgement

**File**: `skills/tarot/cards/20-judgement.md`

**Content**: Awakening, calling, reckoning, renewal, forgiveness, absolution, inner calling, resurrection
- **Archetype**: Awakening, The Call
- **Element**: Fire
- **Astrological**: Pluto

```bash
git add skills/tarot/cards/20-judgement.md
git commit -m "feat: add Major Arcana card 20 - Judgement"
```

### Card 21: The World

**File**: `skills/tarot/cards/21-the-world.md`

**Content**: Completion, integration, wholeness, accomplishment, travel, cosmic consciousness, unity
- **Archetype**: Completion, The Self
- **Element**: Earth
- **Astrological**: Saturn

```bash
git add skills/tarot/cards/21-the-world.md
git commit -m "feat: add Major Arcana card 21 - The World"
```

---

## Task 26: Create Plugin README

**Files:**
- Create: `README.md`

**Step 1: Write README.md**

Create `README.md`:

```markdown
# Claude Tarot Plugin

A Claude Code plugin that provides Major Arcana tarot archetypes for symbolic and archetypal reasoning in AI agents.

## Overview

This plugin enables Claude agents to use the 22 Major Arcana cards from tarot as a framework for archetypal and symbolic reasoning. Agents can perform tarot spreads for multiple perspectives or ask questions to receive relevant archetypal guidance.

## Installation

Install this plugin in Claude Code:

\`\`\`bash
# From GitHub (once published)
claude plugin install 111ecosystem/claude-tarot

# Or from local directory
claude plugin install /path/to/claude-tarot
\`\`\`

## Usage

Once installed, agents can access the tarot skill:

\`\`\`markdown
I'm using the tarot skill to gain archetypal perspective on this architecture decision.

Performing a Three Card spread:
- Past: The Hierophant (established patterns)
- Present: The Tower (necessary disruption)
- Future: The Star (emerging clarity)
\`\`\`

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

\`\`\`
skills/tarot/
├── SKILL.md           # Main skill file with usage instructions
├── spreads.md         # Spread patterns and positions
└── cards/             # Individual card files (00-21)
\`\`\`

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
\`\`\`

**Step 2: Verify README exists**

Run: `cat README.md | head -20`
Expected: Shows plugin overview and installation instructions

**Step 3: Commit**

```bash
git add README.md
git commit -m "docs: add plugin README with installation and usage guide"
```

---

## Task 27: Create LICENSE

**Files:**
- Create: `LICENSE`

**Step 1: Write MIT License**

Create `LICENSE`:

```
MIT License

Copyright (c) 2025 111ecosystem

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

**Step 2: Commit**

```bash
git add LICENSE
git commit -m "chore: add MIT license"
```

---

## Task 28: Final Verification

**Step 1: Verify directory structure**

Run:
```bash
tree -L 3
# Or if tree not available:
find . -type f -name "*.md" -o -name "*.json" | sort
```

Expected output should show:
- `.claude-plugin/plugin.json`
- `skills/tarot/SKILL.md`
- `skills/tarot/spreads.md`
- `skills/tarot/cards/00-the-fool.md` through `skills/tarot/cards/21-the-world.md`
- `README.md`
- `LICENSE`

**Step 2: Verify all 22 card files exist**

Run: `ls -1 skills/tarot/cards/ | wc -l`
Expected: 22

**Step 3: Verify plugin.json is valid**

Run: `cat .claude-plugin/plugin.json | python3 -m json.tool`
Expected: Valid JSON output

**Step 4: Check git status**

Run: `git status`
Expected: Clean working tree (all changes committed)

**Step 5: View commit history**

Run: `git log --oneline`
Expected: Should see ~28 commits for each task

---

## Completion Checklist

- [ ] Plugin manifest created and valid
- [ ] Main SKILL.md with complete agent instructions
- [ ] Spreads reference with all spread patterns
- [ ] All 22 Major Arcana card files created
- [ ] Each card has all four dimensions (traditional, archetypal, correspondences, narrative)
- [ ] Plugin README with installation guide
- [ ] LICENSE file added
- [ ] All files committed to git
- [ ] Directory structure verified
- [ ] Ready for plugin installation testing
