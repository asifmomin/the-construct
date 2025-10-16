# The Construct

> "I know kung fu." — Neo, The Matrix

**The Construct** is an open-source framework for uploading specialized skills into agentic AI systems like Claude Code. Just as Neo learned martial arts instantly through the Construct training program, this framework enables AI agents to acquire expertise through structured skill modules.

## Quick Start

```bash
# Add The Construct marketplace
/plugin marketplace add asifmomin/the-construct

# Install writing skills
/plugin install writing-elements@the-construct

# Start using immediately
/review-writing
[Paste your text for expert feedback]
```

## Available Skills

### Writing Skills: The Elements of Style ✅ Available Now

Master clear, concise writing with timeless principles from Strunk & White's *The Elements of Style*.

**What it does**:
- Reviews and improves your writing automatically
- Applies 18 core principles of effective composition
- Teaches grammar, style, and rhetorical techniques
- Converts wordy, passive text into clear, vigorous prose

**Commands**:
- `/review-writing` - Get detailed feedback on your text
- `/apply-style` - Rewrite text with Elements of Style principles
- `/writing-principles` - Learn the core rules with examples

**Typical results**:
- 30-60% reduction in word count
- 100% more impactful prose
- Professional, authoritative tone

**Example transformation**:

Before (51 words):
> There were a great number of dead leaves lying on the ground. The sound of a guitar somewhere in the house could be heard. It was not long before he was very sorry that he had said what he had.

After (18 words):
> Dead leaves covered the ground. Somewhere in the house a guitar hummed sleepily. He soon repented his words.

**See**: [skills/writing-elements/README.md](skills/writing-elements/README.md) for full documentation.

## Installation

### Prerequisites

- Claude Code installed and running
- Basic familiarity with slash commands

### Step-by-Step

1. **Add the marketplace**:
   ```bash
   /plugin marketplace add asifmomin/the-construct
   ```

2. **Browse available skills**:
   ```bash
   /plugin
   ```
   Select "Browse Plugins" to see all available skills

3. **Install a skill**:
   ```bash
   /plugin install writing-elements@the-construct
   ```

4. **Start using**:
   ```bash
   /writing-principles
   ```

That's it! The skill is now active.

## Usage Examples

### Improve an Email

```
/apply-style

I wanted to reach out to you to let you know that there has been a delay
in the completion of the project. The reason for this delay is due to the
fact that there have been unexpected technical difficulties.
```

**Result**: Concise, professional version with 60% fewer words.

### Get Writing Feedback

```
/review-writing

[Paste your draft]
```

**Result**: Detailed analysis with specific suggestions and teachable moments.

### Learn the Principles

```
/writing-principles
```

**Result**: Interactive guide to core writing rules with examples.

### Automatic Activation

```
Help me write a professional email explaining the project delay.
```

**Result**: Writing coach agent automatically activates and applies Elements of Style principles.

## License

MIT License - Free to use, modify, and distribute.

---

**Ready to start?** Install the writing skills and watch your prose transform:

```bash
/plugin marketplace add asifmomin/the-construct
/plugin install writing-elements@the-construct
/writing-principles
```

**Remember**: Like Neo in The Matrix, you can learn new skills instantly. But mastery comes from practice. 🥋
