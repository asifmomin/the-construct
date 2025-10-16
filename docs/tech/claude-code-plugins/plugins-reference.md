# Plugins reference

Complete technical reference for the Claude Code plugin system, including schemas, CLI commands, and component specifications.

## Plugin components reference

### Commands

Plugins add custom slash commands that integrate seamlessly with Claude Code's command system.

**Location**: `commands/` directory in plugin root
**File format**: Markdown files with frontmatter

Example command structure:

```markdown
---
description: Brief description of what this command does
---

# Command Name

Detailed instructions for Claude on how to execute this command.
Include specific steps, context, and examples.
```

Key features:
- Commands are automatically registered and available via `/command-name`
- Support for markdown formatting in command content
- Frontmatter metadata for command description
- Can include code examples and detailed instructions

### Agents

Plugins can provide specialized subagents for specific tasks that Claude can invoke automatically.

**Location**: `agents/` directory in plugin root
**File format**: Markdown files describing agent capabilities

Example agent structure:

```markdown
---
description: What this agent specializes in
capabilities: ["task1", "task2", "task3"]
---

# Agent Name

Detailed description of the agent's role, expertise, and when Claude should invoke it.

## Capabilities
- Specific task the agent excels at
- Another specialized capability
- When to use this agent vs others

## Context and examples
Provide examples of when this agent should be used and what kinds of problems it solves.
```

Key features:
- Agents are automatically available to Claude
- Define specific expertise areas
- Claude decides when to invoke agents based on context
- Can have multiple agents with different specializations

### Hooks

Plugins can provide event handlers that respond to Claude Code events automatically.

**Location**: `hooks/hooks.json` in plugin root, or inline in `plugin.json`
**Format**: JSON configuration with event matchers and actions

Example hook configuration:

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write|Edit",
        "hooks": [
          {
            "type": "command",
            "command": "${CLAUDE_PLUGIN_ROOT}/scripts/format-code.sh"
          }
        ]
      }
    ],
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "echo 'Running bash command'"
          }
        ]
      }
    ]
  }
}
```

Available hook events:
- `PreToolUse`: Before a tool is used
- `PostToolUse`: After a tool is used
- `PreMessage`: Before Claude sends a message
- `PostMessage`: After Claude sends a message

Hook types:
- `command`: Execute a shell command
- `agent`: Invoke a custom agent

Environment variables available in hooks:
- `${CLAUDE_PLUGIN_ROOT}`: Path to the plugin directory
- `${CLAUDE_WORKING_DIR}`: Current working directory
- Additional context-specific variables

### MCP servers

Plugins can bundle Model Context Protocol (MCP) servers to connect Claude Code with external tools and services.

**Location**: `.mcp.json` in plugin root, or inline in `plugin.json`
**Format**: JSON configuration for MCP servers

Example MCP server configuration:

```json
{
  "mcpServers": {
    "database-tools": {
      "command": "npx",
      "args": ["-y", "@company/mcp-database-server"],
      "env": {
        "DB_CONNECTION": "${DB_CONNECTION}"
      }
    }
  }
}
```

Key features:
- Connect to external APIs and services
- Extend Claude's capabilities with custom tools
- Support for environment variables
- Multiple MCP servers per plugin

## Plugin manifest schema

The `plugin.json` file defines metadata and configuration for your plugin.

**Location**: `.claude-plugin/plugin.json`

### Required fields

```json
{
  "name": "plugin-name",
  "version": "1.0.0",
  "description": "Brief description of the plugin"
}
```

### Complete schema

```json
{
  "name": "enterprise-plugin",
  "version": "2.1.0",
  "description": "Enterprise development tools and workflows",
  "author": {
    "name": "DevTools Team",
    "email": "[email protected]",
    "url": "https://github.com/company/plugins"
  },
  "keywords": ["development", "automation", "enterprise"],
  "license": "MIT",
  "homepage": "https://github.com/company/plugins",
  "repository": {
    "type": "git",
    "url": "https://github.com/company/plugins.git"
  },
  "commands": [
    "commands",
    "additional-commands"
  ],
  "agents": [
    "agents/code-reviewer.md",
    "agents/test-generator.md"
  ],
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write|Edit",
        "hooks": [
          {
            "type": "command",
            "command": "${CLAUDE_PLUGIN_ROOT}/scripts/format.sh"
          }
        ]
      }
    ]
  },
  "mcpServers": {
    "company-api": {
      "command": "node",
      "args": ["${CLAUDE_PLUGIN_ROOT}/mcp-server/index.js"],
      "env": {
        "API_KEY": "${COMPANY_API_KEY}"
      }
    }
  }
}
```

### Field descriptions

- `name` (string, required): Unique identifier for the plugin. Use lowercase with hyphens.
- `version` (string, required): Semantic version (e.g., "1.0.0")
- `description` (string, required): Brief description of plugin purpose
- `author` (object, optional): Author information
  - `name` (string): Author name
  - `email` (string): Contact email
  - `url` (string): Author website or profile
- `keywords` (array, optional): Tags for discoverability
- `license` (string, optional): License identifier (e.g., "MIT", "Apache-2.0")
- `homepage` (string, optional): Plugin homepage URL
- `repository` (object, optional): Source repository information
  - `type` (string): Repository type (e.g., "git")
  - `url` (string): Repository URL
- `commands` (array, optional): Additional command directories/files
- `agents` (array, optional): Agent file locations
- `hooks` (object, optional): Hook configurations
- `mcpServers` (object, optional): MCP server definitions

## Plugin directory structure

Recommended directory structure for a complete plugin:

```
enterprise-plugin/
├── .claude-plugin/
│   └── plugin.json          # Plugin manifest (required)
├── commands/                 # Slash commands
│   ├── review.md
│   ├── deploy.md
│   └── test.md
├── agents/                   # Custom agents
│   ├── code-reviewer.md
│   └── test-generator.md
├── hooks/                    # Hook configurations
│   └── hooks.json
├── scripts/                  # Helper scripts
│   ├── format.sh
│   └── lint.sh
├── mcp-server/              # MCP server code
│   ├── index.js
│   └── package.json
├── .mcp.json                # MCP server configuration
├── README.md                # Plugin documentation
├── LICENSE                  # License file
└── CHANGELOG.md            # Version history
```

## CLI commands reference

### Plugin management

```bash
# List installed plugins
/plugin

# Install a plugin
/plugin install <plugin-name>@<marketplace-name>

# Enable a plugin
/plugin enable <plugin-name>@<marketplace-name>

# Disable a plugin
/plugin disable <plugin-name>@<marketplace-name>

# Uninstall a plugin
/plugin uninstall <plugin-name>@<marketplace-name>

# Update a plugin
/plugin update <plugin-name>@<marketplace-name>
```

### Marketplace management

```bash
# Add a marketplace
/plugin marketplace add <source>

# List marketplaces
/plugin marketplace list

# Remove a marketplace
/plugin marketplace remove <marketplace-name>

# Refresh marketplace data
/plugin marketplace refresh <marketplace-name>
```

## Debugging plugins

### Enable debug mode

```bash
claude --debug
```

This will show:
- Plugin loading details
- Command registration
- Hook execution
- Agent invocations
- MCP server connections

### Common issues

**Plugin not loading**
- Check that `plugin.json` exists in `.claude-plugin/` directory
- Verify JSON syntax is valid
- Ensure all required fields are present

**Command not available**
- Verify command file is in `commands/` directory
- Check that file has `.md` extension
- Ensure frontmatter is properly formatted

**Hook not executing**
- Verify hook matcher syntax
- Check that script has execute permissions
- Ensure environment variables are defined

**MCP server connection failed**
- Check server command and arguments
- Verify required environment variables
- Test server independently

### Validation

Test your plugin before distribution:

```bash
# Install from local path
/plugin marketplace add ./my-plugin
/plugin install my-plugin@local

# Test all commands
/command-name

# Trigger hooks
# (perform actions that should trigger your hooks)

# Check MCP server
# (use features that depend on your MCP server)
```

## Version management

Follow semantic versioning:

- **Major** (1.0.0): Breaking changes
- **Minor** (0.1.0): New features, backward compatible
- **Patch** (0.0.1): Bug fixes, backward compatible

Example version progression:
- `1.0.0` - Initial release
- `1.1.0` - Add new command
- `1.1.1` - Fix command bug
- `2.0.0` - Change command syntax (breaking)

## Best practices

### Plugin design
- Keep plugins focused on a single purpose
- Use clear, descriptive names
- Document all commands and features
- Provide examples and use cases

### Command design
- Write clear instructions for Claude
- Include context and constraints
- Provide examples when helpful
- Keep commands focused and specific

### Agent design
- Define clear areas of expertise
- Document when agent should be invoked
- Avoid overlapping responsibilities
- Test agent behavior thoroughly

### Hook design
- Use specific matchers to avoid unwanted triggers
- Keep hook scripts fast and reliable
- Handle errors gracefully
- Log important events

### MCP server design
- Implement proper error handling
- Validate inputs thoroughly
- Document required environment variables
- Provide clear error messages

## Distribution

### Publishing to marketplaces
1. Test plugin thoroughly
2. Update version in `plugin.json`
3. Add entry to marketplace `marketplace.json`
4. Commit and push changes
5. Tag release in git (optional)

### Team distribution
- Create team marketplace repository
- Add plugins to marketplace
- Share marketplace URL with team
- Document plugin usage

### Public distribution
- Choose open source license
- Add comprehensive README
- Provide examples and documentation
- Submit to community marketplaces
