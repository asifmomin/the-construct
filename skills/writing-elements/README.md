# Writing Elements Skill

Master clear, concise, and vigorous writing with timeless principles from *The Elements of Style* by William Strunk Jr.

## Overview

This skill teaches AI agents (and helps you learn) the fundamental principles of good writing through the classic 1918 text *The Elements of Style*. Once installed, Claude Code will automatically apply these principles when writing or reviewing text.

## What You'll Learn

### The Big Four Principles

1. **Use Active Voice** - Write directly and forcefully
2. **Omit Needless Words** - Make every word count
3. **Use Specific Language** - Create vivid, concrete images
4. **State Things Positively** - Say what IS, not just what ISN'T

### Complete Coverage

- **18 core rules** covering grammar, punctuation, and composition
- **Common mistakes** and how to fix them
- **Before/after examples** showing dramatic improvements
- **Practical techniques** for immediate application

## Installation

```bash
# Add The Construct marketplace
/plugin marketplace add asifmomin/the-construct

# Install the writing-elements skill
/plugin install writing-elements@the-construct
```

## Available Commands

### `/review-writing`

Analyze text using Elements of Style principles and get detailed feedback.

**Usage**:
```
/review-writing

[Paste your text]
```

**You'll receive**:
- Overall assessment of writing quality
- Specific issues with explanations
- Concrete suggestions for improvement
- Teaching of applicable principles
- Priority list of most impactful changes

### `/apply-style`

Rewrite text applying Elements of Style principles with before/after comparison.

**Usage**:
```
/apply-style

[Paste your text]
```

**You'll receive**:
- Fully revised version
- Side-by-side comparison
- Explanation of each change
- Summary of improvements (word count, passive voice, etc.)

### `/writing-principles`

Display core Elements of Style principles with examples.

**Usage**:
```
/writing-principles
```

**Options**:
- Comprehensive overview (all principles)
- Specific categories (grammar, composition)
- Deep dive into particular rules
- Quick reference cheat sheet

## Automatic Agent Activation

The Writing Coach agent activates automatically when you:
- Ask for help improving text
- Share drafts for feedback
- Request writing advice
- Generate text with quality emphasis

No need to invoke commands explicitly—just work naturally and the agent will help when appropriate.

## Examples

### Example 1: Email Improvement

**Before** (73 words):
```
I wanted to reach out to you to let you know that there has been a delay
in the completion of the project that we have been working on. The reason
for this delay is due to the fact that there have been some unexpected
technical difficulties that have arisen.
```

**After** (20 words):
```
The project will be delayed due to unexpected technical difficulties. We
are working to resolve these issues quickly.
```

**Improvements**:
- 73% word reduction
- Active voice throughout
- Eliminated needless phrases
- Clearer, more professional

### Example 2: Technical Description

**Before** (45 words):
```
The implementation of the new system has resulted in significant improvements
in terms of operational efficiency. There has been a marked reduction in the
amount of time required for data processing tasks.
```

**After** (16 words):
```
The new system processes data three times faster and has improved operational
efficiency significantly.
```

**Improvements**:
- 64% word reduction
- Specific metrics instead of vague "significant"
- Active voice
- More impactful

### Example 3: The Classic Transformation

**Before** (51 words):
```
There were a great number of dead leaves lying on the ground. The sound
of a guitar somewhere in the house could be heard. It was not long before
he was very sorry that he had said what he had. The reason that he left
college was that his health became impaired.
```

**After** (23 words):
```
Dead leaves covered the ground. Somewhere in the house a guitar hummed
sleepily. He soon repented his words. Failing health compelled him to
leave college.
```

**Improvements**:
- 55% word reduction
- All passive voice converted to active
- Vague language made concrete
- Every word earns its place

## Quick Reference

### Top 10 Rules to Remember

1. **Use active voice** - "The committee decided" not "It was decided by the committee"
2. **Omit needless words** - "because" not "due to the fact that"
3. **Be specific** - "It rained for three days" not "Weather was unfavorable"
4. **Be positive** - "He usually came late" not "He was not very often on time"
5. **Use serial comma** - "red, white, and blue"
6. **Don't join independent clauses with comma** - Use semicolon or period
7. **Keep related words together** - "He found only two" not "He only found two"
8. **Place emphatic words at end** - Save the punch for the punchline
9. **One paragraph, one topic** - Clear organization aids comprehension
10. **Begin with topic sentence** - State your point, then develop it

### Common Fixes

| Problem | Solution |
|---------|----------|
| Passive voice | Make the subject act |
| "The fact that" | Eliminate entirely |
| "There is/are" | Use active verb |
| Vague adjectives | Use specific details |
| Negative statements | State positively |
| Long-winded | Cut to 1/3 the words |

## Learning Path

### Week 1: The Big Four
Focus on the four most impactful principles:
- Active voice
- Omit needless words
- Specific language
- Positive form

### Week 2: Grammar Basics
Master the seven usage rules:
- Possessive formation
- Serial commas
- Parenthetic expressions
- Coordinate clauses

### Week 3: Composition
Learn the eleven composition principles:
- Paragraph structure
- Topic sentences
- Sentence variety
- Emphatic placement

### Week 4: Polish
Internalize all principles through practice

## Knowledge Base

This skill includes comprehensive reference materials:

- **`knowledge/principles.md`** - Core principles and philosophy
- **`knowledge/rules.md`** - All 18 rules with detailed examples
- **`knowledge/examples.md`** - Before/after transformations

## Impact Metrics

Applying Elements of Style typically results in:

- **30-60% reduction** in word count
- **80-100% elimination** of passive voice
- **Dramatic improvement** in clarity and impact
- **More professional** and authoritative tone

## Tips for Best Results

### When Reviewing Your Writing

1. **Draft freely** first - Don't self-edit while creating
2. **Apply /review-writing** - Get specific feedback
3. **Use /apply-style** - See the fully revised version
4. **Learn the patterns** - Understand what changed and why
5. **Practice consciously** - Apply principles to next draft

### When Generating New Text

1. **State your goal** clearly
2. **Let the agent apply principles** automatically
3. **Request adjustments** if needed
4. **Learn from the output** - Note techniques used

### Building Long-term Skills

1. **Focus on one principle** per week
2. **Review examples** daily
3. **Practice on real work** - emails, reports, documentation
4. **Track improvements** - Notice your before/after evolution
5. **Teach others** - Best way to internalize

## Source Material

This skill is based on the 1918 edition of *The Elements of Style* by William Strunk Jr., which is in the public domain. The full original text is available in this repository at `/docs/writing/elements-of-style.md`.

The principles have stood the test of time and remain the foundation of clear, effective writing more than a century later.

## Troubleshooting

### Agent not activating?

Make sure the plugin is enabled:
```
/plugin
```
Check that "writing-elements" shows as enabled.

### Commands not available?

Reinstall the plugin:
```
/plugin uninstall writing-elements@the-construct
/plugin install writing-elements@the-construct
```

### Want more aggressive editing?

Use `/apply-style` which applies all principles automatically for maximum impact.

### Want to learn specific rules?

Use `/writing-principles` and ask for deep dive on specific rules.

## What's Next?

After mastering writing elements, look for additional skills in The Construct marketplace:

- **Code Architecture** (coming soon) - Clean Code and design patterns
- **System Design** (coming soon) - Distributed systems principles
- **API Design** (coming soon) - REST and GraphQL best practices

## Contributing

Found a great example transformation? Have suggestions for additional commands? Contributions welcome!

## License

MIT License - Free to use, modify, and distribute.

## Credits

- Original text: William Strunk Jr., *The Elements of Style* (1918)
- Skill implementation: The Construct Team
- Plugin system: Claude Code by Anthropic

---

**Remember**: Clear writing is a skill anyone can develop. These principles work. Apply them consistently, and watch your writing transform.
