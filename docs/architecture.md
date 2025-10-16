# The Construct - Architecture Design

## Overview

The Construct is a framework that delivers specialized skills to AI agents through Claude Code's plugin system. Each skill is packaged as a Claude Code plugin that can be installed from The Construct marketplace.

## Core Concepts

### Skills as Plugins

Each skill in The Construct is a self-contained Claude Code plugin that includes:

- **Commands**: Slash commands that invoke skill-specific capabilities
- **Agents**: Specialized subagents with domain expertise
- **Knowledge Base**: Reference materials and principles encoded in markdown
- **Examples**: Before/after demonstrations of the skill in action

### Skill Delivery Architecture

```
┌─────────────────────────────────────────────────────┐
│           The Construct Marketplace                 │
│  (marketplace.json listing all available skills)    │
└────────────────┬────────────────────────────────────┘
                 │
                 │ Users install skills via:
                 │ /plugin marketplace add the-construct
                 │ /plugin install writing-elements@the-construct
                 │
                 ▼
┌─────────────────────────────────────────────────────┐
│              Claude Code Instance                   │
│                                                     │
│  ┌─────────────────────────────────────────┐      │
│  │   Writing Elements Skill Plugin         │      │
│  │                                           │      │
│  │  • Commands: /review-writing             │      │
│  │              /apply-style                │      │
│  │              /writing-principles         │      │
│  │                                           │      │
│  │  • Agent: Writing Coach                  │      │
│  │           (auto-invoked for writing)     │      │
│  │                                           │      │
│  │  • Knowledge: Elements of Style rules    │      │
│  │               Examples & patterns        │      │
│  └─────────────────────────────────────────┘      │
└─────────────────────────────────────────────────────┘
```

## Directory Structure

```
the-construct/
├── marketplace.json              # The Construct marketplace manifest
├── README.md                     # Project overview and quick start
├── docs/
│   ├── architecture.md          # This file - architecture design
│   ├── creating-skills.md       # Guide for creating new skills
│   └── tech/                    # Technical documentation
│       └── claude-code-plugins/ # Claude Code plugin reference
├── skills/                      # Individual skill modules
│   └── writing-elements/        # First skill: Elements of Style
│       ├── .claude-plugin/
│       │   └── plugin.json     # Plugin manifest
│       ├── commands/            # Slash commands
│       │   ├── review-writing.md
│       │   ├── apply-style.md
│       │   └── writing-principles.md
│       ├── agents/              # Specialized agents
│       │   └── writing-coach.md
│       ├── knowledge/           # Reference materials
│       │   ├── principles.md   # Core writing principles
│       │   ├── rules.md        # Specific rules from the book
│       │   └── examples.md     # Before/after examples
│       └── README.md           # Skill-specific documentation
└── templates/                   # Templates for new skills
    └── skill-template/         # Starter template
        ├── .claude-plugin/
        │   └── plugin.json
        ├── commands/
        ├── agents/
        └── README.md
```

## Writing Elements Skill Design

### Components

#### 1. Commands (`commands/`)

**`/review-writing`**
- Analyzes provided text using Elements of Style principles
- Identifies violations of key rules
- Suggests specific improvements
- Rates text on clarity, conciseness, and vigor

**`/apply-style`**
- Takes text and rewrites it applying Elements of Style rules
- Focuses on: removing needless words, using active voice, clarity
- Shows before/after comparison
- Explains what was changed and why

**`/writing-principles`**
- Displays the core principles from Elements of Style
- Shows examples of each principle
- Interactive reference guide

#### 2. Agent (`agents/writing-coach.md`)

A specialized subagent that:
- Has deep knowledge of Elements of Style principles
- Automatically invoked when Claude detects writing/editing tasks
- Provides feedback on drafts
- Suggests improvements based on style rules
- Teaches principles through examples

#### 3. Knowledge Base (`knowledge/`)

**`principles.md`** - The foundational rules:
- Elementary Rules of Usage (Chapter I)
- Elementary Principles of Composition (Chapter II)
- A Few Matters of Form (Chapter III)
- Words and Expressions Commonly Misused (Chapter IV)
- Words Often Misspelled (Chapter V)

**`rules.md`** - Specific, actionable rules:
- Rule 1: Form possessive singular nouns with 's
- Rule 2: In a series use comma after each term
- Rule 13: Omit needless words
- Rule 14: Use active voice
- Rule 17: Keep related words together
- etc.

**`examples.md`** - Before/after demonstrations:
- Example transformations showing rules in action
- Common mistakes and corrections
- Good vs. bad writing samples

### User Experience Flow

1. **Installation**
   ```bash
   /plugin marketplace add anthropics/the-construct
   /plugin install writing-elements@the-construct
   ```

2. **Usage - Explicit Commands**
   ```bash
   # Review existing text
   /review-writing
   [Claude asks for text, analyzes it, provides feedback]

   # Improve text
   /apply-style
   [Claude rewrites text using Elements of Style principles]

   # Learn principles
   /writing-principles
   [Claude shows key rules and examples]
   ```

3. **Usage - Automatic Agent Invocation**
   ```
   User: "Help me improve this paragraph: [text]"
   Claude: [Automatically invokes writing-coach agent]
           [Applies Elements of Style expertise]
           [Provides improvements with explanations]
   ```

## Implementation Strategy

### Phase 1: Foundation
1. Create directory structure
2. Set up marketplace.json
3. Create plugin manifest for writing-elements

### Phase 2: Knowledge Extraction
1. Extract principles from Elements of Style
2. Create knowledge base markdown files
3. Organize rules and examples

### Phase 3: Plugin Development
1. Write slash commands
2. Create writing coach agent
3. Integrate knowledge base references

### Phase 4: Testing & Refinement
1. Test commands with sample texts
2. Verify agent behavior
3. Refine prompts and knowledge base

### Phase 5: Documentation
1. Write skill README
2. Update main README with installation
3. Create guide for adding new skills

## Future Skills

The framework is designed to support any skill that can be taught through:
- Structured principles and rules
- Examples and patterns
- Specialized agent expertise
- Interactive commands

Potential future skills:
- **Code Architecture** (Clean Code, Design Patterns)
- **System Design** (Distributed Systems principles)
- **API Design** (REST, GraphQL best practices)
- **Security** (OWASP Top 10, secure coding)
- **Performance** (Optimization techniques)
- **Testing** (TDD, testing patterns)

## Benefits of Plugin Architecture

1. **Modularity**: Each skill is independent
2. **Discoverability**: Skills listed in marketplace
3. **Version Control**: Skills can be updated independently
4. **Shareability**: Easy to distribute and install
5. **Customization**: Users choose which skills to install
6. **Consistency**: Same installation/usage pattern for all skills

## Technical Implementation Notes

### Plugin Manifest Requirements

Each skill must have `.claude-plugin/plugin.json`:

```json
{
  "name": "skill-name",
  "version": "1.0.0",
  "description": "Brief skill description",
  "author": {
    "name": "The Construct Team"
  },
  "keywords": ["writing", "style", "editing"]
}
```

### Command Format

Commands are markdown files with frontmatter:

```markdown
---
description: What this command does
---

# Command Instructions

Detailed instructions for Claude on how to execute this command.
Include context, constraints, and examples.
```

### Agent Format

Agents are markdown files describing expertise:

```markdown
---
description: Agent specialization
capabilities: ["task1", "task2"]
---

# Agent Name

Detailed description of agent's expertise and when to invoke.
```

### Marketplace Format

The Construct marketplace lists all skills:

```json
{
  "name": "the-construct",
  "description": "Skills marketplace for AI agents",
  "owner": {
    "name": "The Construct Team"
  },
  "plugins": [
    {
      "name": "writing-elements",
      "source": "./skills/writing-elements",
      "description": "Elements of Style writing principles",
      "version": "1.0.0"
    }
  ]
}
```

## Success Metrics

A successful skill implementation should:
1. ✅ Install cleanly via Claude Code plugin system
2. ✅ Provide clear, actionable commands
3. ✅ Have an agent that activates appropriately
4. ✅ Include comprehensive knowledge base
5. ✅ Show measurable improvement in outputs
6. ✅ Be well-documented and easy to use

---

**Version**: 1.0.0
**Last Updated**: 2025-10-16
**Status**: Design Complete - Ready for Implementation
