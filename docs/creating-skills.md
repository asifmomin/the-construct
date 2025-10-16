# Creating Skills for The Construct

A comprehensive guide to creating new skills for The Construct framework.

## Overview

Skills in The Construct are Claude Code plugins that teach AI agents specialized expertise through structured knowledge, commands, and agents. This guide will walk you through creating your own skill from scratch.

## What Makes a Good Skill?

Before creating a skill, ensure it has these characteristics:

### 1. Teachable Principles

The skill must be based on clear, learnable principles that can be broken down into rules and patterns.

✅ **Good examples**:
- Writing principles (Elements of Style)
- Code design patterns (SOLID, Clean Code)
- API design best practices

❌ **Poor examples**:
- Vague intuitions without clear rules
- Taste-based judgments without criteria
- Context-dependent advice without frameworks

### 2. Demonstrable Improvements

The skill should show clear before/after transformations.

✅ **Good**: Can show dramatic improvement (wordy → concise, complex → simple)
❌ **Poor**: Improvements are subjective or hard to measure

### 3. Transferable Knowledge

Principles should apply across many contexts, not just specific scenarios.

✅ **Good**: "Omit needless words" applies to all writing
❌ **Poor**: "Click this button in this app" is too specific

### 4. Timeless Value

Skills should be based on fundamentals, not trends.

✅ **Good**: Computer science fundamentals, writing principles
❌ **Poor**: Current framework-specific patterns that may change

### 5. Practical Application

Users should be able to apply the skill immediately to real work.

✅ **Good**: Can use on current projects right away
❌ **Poor**: Academic knowledge with no clear application

## Skill Structure

Every skill follows this structure:

```
your-skill/
├── .claude-plugin/
│   └── plugin.json          # Plugin manifest (required)
├── commands/                 # Slash commands (recommended)
│   ├── command-1.md
│   └── command-2.md
├── agents/                   # Specialized agents (recommended)
│   └── expert-agent.md
├── knowledge/                # Reference materials (recommended)
│   ├── principles.md
│   ├── rules.md
│   └── examples.md
└── README.md                # Documentation (required)
```

## Step-by-Step Guide

### Step 1: Choose Your Skill Domain

Pick an area where you have deep expertise and clear principles to teach.

**Questions to ask**:
- What principles do I wish more people knew?
- What repeated patterns do I see in my work?
- What frameworks have transformed my practice?
- What would I teach in a masterclass?

**Example**: Writing skills based on Elements of Style

### Step 2: Extract Core Principles

Break down your expertise into teachable components.

**Process**:
1. List 10-20 key principles
2. Group into 3-5 categories
3. Find examples for each principle
4. Create before/after demonstrations
5. Identify common mistakes

**Example structure**:
```markdown
# Core Principles

## Category 1: Foundation
- Principle 1: [Rule]
  - Why it matters
  - How to apply
  - Examples

## Category 2: Application
- Principle 2: [Rule]
  ...
```

### Step 3: Create the Plugin Manifest

Create `.claude-plugin/plugin.json`:

```json
{
  "name": "your-skill-name",
  "version": "1.0.0",
  "description": "Brief description of what this skill teaches",
  "author": {
    "name": "Your Name",
    "email": "your@email.com",
    "url": "https://your-website.com"
  },
  "keywords": [
    "relevant",
    "search",
    "keywords"
  ],
  "license": "MIT"
}
```

**Naming conventions**:
- Use lowercase with hyphens: `api-design`, `clean-code`
- Be specific: `rest-api-design` not just `api`
- Avoid version numbers in name

### Step 4: Design Commands

Commands are explicit actions users can invoke. Design 2-5 core commands.

**Command types**:

**1. Review/Analysis Command**
Analyze user input against your principles.

Example: `/review-api` - Analyze API design

**2. Apply/Transform Command**
Transform user input using your principles.

Example: `/refactor-code` - Apply clean code principles

**3. Reference Command**
Display principles and examples.

Example: `/design-patterns` - Show pattern catalog

**4. Generate Command**
Create something new following principles.

Example: `/generate-api` - Design new API endpoint

### Step 5: Write Command Instructions

Create command files in `commands/` directory.

**Template**:
```markdown
---
description: Brief description of what this command does
---

# Command Name

You are an expert in [domain]. Your role is to [purpose of this command].

## Your Task

1. [Step 1]
2. [Step 2]
3. [Step 3]

## Principles to Apply

[List the key principles this command uses]

## Output Format

[Describe how to format the response]

## Example

[Show a concrete example]

## Guidelines

[Additional instructions for edge cases]
```

**Full example** (`commands/review-api.md`):
```markdown
---
description: Review API design against REST best practices
---

# Review API Design

You are a REST API design expert. Your role is to review API designs
and provide feedback based on REST principles and best practices.

## Your Task

1. Ask for the API specification if not provided
2. Analyze against REST principles
3. Provide specific, actionable feedback

## Principles to Apply

- Resource-oriented design
- Proper HTTP verb usage
- Consistent naming conventions
- Appropriate status codes
- Versioning strategy
- Error handling patterns

## Output Format

### Overall Assessment
[Brief summary]

### Specific Issues
For each issue:
- Location: [Endpoint]
- Problem: [What's wrong]
- Principle: [Which rule violated]
- Suggestion: [How to fix]

### Priority Improvements
[Top 3-5 most impactful changes]

## Example

[Concrete example of review output]
```

### Step 6: Create Expert Agents

Agents activate automatically when relevant. Create agent definitions in `agents/` directory.

**Template**:
```markdown
---
description: Expert specialization
capabilities: ["task1", "task2", "task3"]
---

# Agent Name

You are an expert in [domain] with deep knowledge of [specific area].
You are automatically activated when users [trigger conditions].

## Your Expertise

[Detailed description of what you know]

## When to Activate

Invoke your expertise when users:
1. [Trigger 1]
2. [Trigger 2]
3. [Trigger 3]

## When NOT to Activate

Do not apply your expertise when:
- [Exclusion 1]
- [Exclusion 2]

## Your Approach

### Analysis Mode
[How to analyze user input]

### Generation Mode
[How to create new content]

### Coaching Mode
[How to teach principles]

## Top Priorities

[The most important principles to apply]

## Response Patterns

[Example responses for common scenarios]
```

### Step 7: Build Knowledge Base

Create reference materials in `knowledge/` directory.

**Recommended files**:

**`principles.md`** - Core concepts:
```markdown
# Core Principles - [Your Skill]

## Philosophy
[Fundamental philosophy]

## Key Principles

### Principle 1: [Name]
**Principle**: [Statement]
**Why it matters**: [Rationale]
**How to apply**: [Application]
**Example**: [Demonstration]

[Continue for all principles...]
```

**`rules.md`** - Detailed rules:
```markdown
# Detailed Rules - [Your Skill]

## Rule 1: [Rule Name]

**The Rule**: [Clear statement]

**Examples**:
- [Example 1]
- [Example 2]

**Common violations**:
- [Mistake 1]
- [Mistake 2]

**How to apply**:
[Step-by-step instructions]

[Continue for all rules...]
```

**`examples.md`** - Before/after transformations:
```markdown
# Examples - [Your Skill]

## Transformation 1: [Name]

### Before
[Original version]

### After
[Improved version]

### Principles Applied
- [Principle 1]
- [Principle 2]

### Impact
[Measurable improvements]

[Continue with more examples...]
```

### Step 8: Write Comprehensive README

Create a README for your skill in the skill root directory.

**Required sections**:
- Overview
- Installation
- Available Commands
- Examples
- Quick Reference
- Learning Path
- Troubleshooting

See `skills/writing-elements/README.md` for a complete template.

### Step 9: Test Your Skill

Before publishing, thoroughly test:

**Functionality testing**:
1. Install from local marketplace
2. Test each command with various inputs
3. Verify agent activates appropriately
4. Check knowledge base accessibility

**Quality testing**:
1. Clear instructions in commands?
2. Good examples in knowledge base?
3. Agent doesn't over-activate?
4. Commands produce useful output?

**Documentation testing**:
1. README clear and complete?
2. All commands documented?
3. Installation instructions work?
4. Examples representative?

### Step 10: Package in Marketplace

Add your skill to `marketplace.json`:

```json
{
  "name": "your-marketplace",
  "description": "Your marketplace description",
  "owner": {
    "name": "Your Name"
  },
  "pluginRoot": "./skills",
  "plugins": [
    {
      "name": "your-skill-name",
      "source": "./skills/your-skill-name",
      "description": "Brief skill description",
      "version": "1.0.0",
      "author": {
        "name": "Your Name"
      },
      "keywords": ["relevant", "keywords"],
      "license": "MIT"
    }
  ]
}
```

### Step 11: Publish and Share

Options for sharing:

**1. Contribute to The Construct**
- Submit pull request
- Add to official marketplace
- Available to all users

**2. Create Organization Marketplace**
- Host in your org's repo
- Private or public
- Team-specific skills

**3. Personal Marketplace**
- Host in your own repo
- Share URL with collaborators

## Best Practices

### Command Design

✅ **Do**:
- Provide clear, specific instructions
- Include concrete examples
- Handle edge cases
- Give actionable feedback

❌ **Don't**:
- Be vague or ambiguous
- Assume context
- Ignore error cases
- Give generic advice

### Agent Design

✅ **Do**:
- Define clear activation triggers
- Specify when NOT to activate
- Provide specific expertise
- Show, don't just tell

❌ **Don't**:
- Activate for everything
- Overlap with other agents
- Be overly general
- Give vague guidance

### Knowledge Base

✅ **Do**:
- Organize logically
- Provide abundant examples
- Show before/after
- Make it searchable

❌ **Don't**:
- Dump unstructured information
- Omit examples
- Use jargon without explanation
- Make it too abstract

## Example Skills You Could Create

### Technical Skills

**Code Architecture**
- SOLID principles
- Design patterns
- Clean code practices
- Refactoring techniques

**System Design**
- Scalability patterns
- Distributed systems
- Database design
- API architecture

**Security**
- OWASP Top 10
- Secure coding practices
- Threat modeling
- Cryptography basics

**Performance**
- Optimization techniques
- Profiling strategies
- Caching patterns
- Load testing

### Professional Skills

**Technical Writing**
- Documentation principles
- API documentation
- README best practices
- Tutorial creation

**Code Review**
- Review techniques
- Constructive feedback
- Common issues checklist
- Best practices

**Testing**
- TDD principles
- Test design patterns
- Coverage strategies
- E2E testing

**DevOps**
- CI/CD best practices
- Infrastructure as code
- Monitoring and logging
- Deployment strategies

### Domain-Specific Skills

**Data Science**
- Statistical principles
- Visualization best practices
- Experiment design
- Model interpretation

**UI/UX**
- Design principles
- Accessibility
- User research
- Usability testing

**Database Design**
- Normalization
- Index optimization
- Query patterns
- Schema design

## Troubleshooting

### Common Issues

**Commands don't work**
- Check markdown frontmatter syntax
- Verify file extension is `.md`
- Ensure commands directory exists

**Agent doesn't activate**
- Clarify activation triggers
- Check capabilities list
- Verify agent description is clear

**Knowledge base not accessible**
- Ensure files are in knowledge/ directory
- Check markdown formatting
- Verify paths in references

**Plugin won't install**
- Validate plugin.json syntax
- Check all required fields present
- Verify directory structure correct

## Resources

### Templates

Use the skill template in `templates/skill-template/` as a starting point.

### Documentation

- [Architecture Guide](architecture.md) - Framework design
- [Plugin Reference](tech/claude-code-plugins/plugins-reference.md) - Technical details
- [Marketplace Guide](tech/claude-code-plugins/plugin-marketplaces.md) - Distribution

### Examples

Study existing skills:
- `skills/writing-elements/` - Complete working example

## Getting Help

- **Issues**: Report bugs or ask questions
- **Discussions**: Share ideas and get feedback
- **Pull Requests**: Contribute improvements

## Skill Checklist

Before publishing, verify:

- [ ] Clear, teachable principles identified
- [ ] Plugin manifest created with all required fields
- [ ] 2-5 useful commands implemented
- [ ] At least one expert agent defined
- [ ] Knowledge base with principles, rules, and examples
- [ ] Comprehensive README with examples
- [ ] Tested locally and works correctly
- [ ] Added to marketplace.json
- [ ] Examples demonstrate clear value
- [ ] Documentation is complete and clear

## Next Steps

1. **Choose your domain** - Pick something you know deeply
2. **Extract principles** - Document your expertise
3. **Build your skill** - Follow this guide step by step
4. **Test thoroughly** - Make sure it works
5. **Share with community** - Help others learn

---

**Remember**: The best skills come from deep expertise combined with a passion for teaching. Share what you know, and help AI agents (and humans!) level up their capabilities.

Good luck creating your skill! 🚀
