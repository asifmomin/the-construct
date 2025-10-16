# Plugins

Plugins allow you to extend Claude Code's functionality by adding custom commands, agents, hooks, and MCP servers. They can be shared across projects and teams, installed from marketplaces, and customized to automate your workflows.

## Quickstart

### Prerequisites
- Claude Code installed on your machine
- Basic familiarity with command-line tools

### Create your first plugin

Follow these steps to create a simple plugin:

#### 1. Create the marketplace structure

```bash
mkdir test-marketplace
cd test-marketplace
```

#### 2. Create the plugin directory

```bash
mkdir my-first-plugin
cd my-first-plugin
```

#### 3. Create the plugin manifest

```bash
mkdir .claude-plugin
cat > .claude-plugin/plugin.json << 'EOF'
{
  "name": "my-first-plugin",
  "description": "A simple greeting plugin to learn the basics",
  "version": "1.0.0",
  "author": {
    "name": "Your Name"
  }
}
EOF
```

#### 4. Add a custom command

Create a command file:

```bash
mkdir commands
cat > commands/hello.md << 'EOF'
---
description: Greet the user with a personalized message
---

# Hello Command

Greet the user warmly and ask how you can help them today. Make the greeting personal and encouraging.
EOF
```

#### 5. Create the marketplace manifest

Navigate back to your marketplace directory and create a marketplace.json:

```bash
cd ..
cat > marketplace.json << 'EOF'
{
  "name": "test-marketplace",
  "owner": {
    "name": "Your Name"
  },
  "plugins": [
    {
      "name": "my-first-plugin",
      "source": "./my-first-plugin",
      "description": "A simple greeting plugin to learn the basics",
      "version": "1.0.0"
    }
  ]
}
EOF
```

#### 6. Install and test the plugin

```bash
# Add your local marketplace
/plugin marketplace add .

# Install your plugin
/plugin install my-first-plugin@test-marketplace

# Test your new command
/hello
```

### Plugin structure overview

A typical plugin has the following structure:

```
my-first-plugin/
├── .claude-plugin/
│   └── plugin.json          # Plugin metadata (required)
├── commands/                 # Custom slash commands (optional)
│   └── hello.md
├── agents/                   # Custom agents (optional)
│   └── helper.md
└── hooks/                    # Event handlers (optional)
    └── hooks.json
```

## Install and manage plugins

### Add marketplaces

Before you can install plugins, you need to add a marketplace:

```bash
# Add a GitHub marketplace
/plugin marketplace add your-org/claude-plugins

# Add a Git repository
/plugin marketplace add https://gitlab.com/company/plugins.git

# Add a local marketplace for development
/plugin marketplace add ./my-marketplace
```

### Browse available plugins

Open the plugin management interface:

```bash
/plugin
```

This will show you an interactive menu where you can:
- Browse available plugins from all configured marketplaces
- See which plugins are installed
- Enable/disable plugins
- Install new plugins

### Install plugins

#### Via interactive menu (recommended)

1. Open plugin management: `/plugin`
2. Select "Browse Plugins"
3. Choose a plugin from the list
4. Confirm installation

#### Via direct commands

```bash
# Install a specific plugin
/plugin install formatter@your-org

# Enable a plugin
/plugin enable plugin-name@marketplace-name

# Disable a plugin
/plugin disable plugin-name@marketplace-name

# Remove a plugin
/plugin uninstall plugin-name@marketplace-name
```

## Development workflow

When developing plugins, use this iterative workflow:

### 1. Create a local development marketplace

```bash
mkdir dev-marketplace
cd dev-marketplace
mkdir my-plugin
# Add your plugin files to my-plugin/
```

### 2. Add the local marketplace

```bash
/plugin marketplace add ./dev-marketplace
```

### 3. Make changes and test

```bash
# Make changes to your plugin files
# Uninstall and reinstall to test changes
/plugin uninstall my-plugin@dev-marketplace
/plugin install my-plugin@dev-marketplace
```

### 4. Verify your changes

Test your plugin thoroughly:
- Test all custom commands
- Verify agents are invoked correctly
- Check hook behavior
- Test with different project types

## Repository-level configuration

You can configure plugins at the repository level using `.claude/plugins.json`:

```json
{
  "marketplaces": [
    {
      "name": "company-tools",
      "source": "https://github.com/company/claude-plugins"
    }
  ],
  "plugins": [
    {
      "name": "code-formatter",
      "marketplace": "company-tools",
      "enabled": true
    }
  ]
}
```

This allows you to:
- Share plugin configuration across your team
- Ensure consistent tooling across projects
- Manage plugins declaratively

## Next steps

### For users
- Discover community plugins and marketplaces
- Explore available plugins for your tech stack
- Share useful plugins with your team

### For developers
- Create custom plugins for your workflows
- Publish plugins to share with others
- Contribute to community marketplaces

### For team leads
- Establish plugin governance policies
- Create team-specific marketplaces
- Define standard plugin configurations
