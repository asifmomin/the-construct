# Plugin marketplaces

Plugin marketplaces are catalogs of available plugins that make it easy to discover, install, and manage Claude Code extensions. A marketplace is simply a JSON file that lists available plugins and their sources.

## Overview

Marketplaces provide several key benefits:

- **Centralized discovery**: Browse all available plugins in one place
- **Version management**: Track and update plugin versions
- **Team distribution**: Share plugins across your organization
- **Flexible sources**: Support for git repositories, GitHub repos, local paths, and package managers

### Prerequisites

- Claude Code installed and running
- Basic familiarity with JSON file format
- For creating marketplaces: Git repository or local development environment

## Add and use marketplaces

### Add GitHub marketplaces

The easiest way to add a marketplace is from a GitHub repository:

```bash
/plugin marketplace add owner/repo
```

This will:
- Clone or fetch the repository
- Look for `marketplace.json` in the root
- Register the marketplace with Claude Code
- Make all plugins available for installation

Examples:

```bash
# Add official Claude Code marketplace
/plugin marketplace add anthropics/claude-code-plugins

# Add your organization's marketplace
/plugin marketplace add your-company/claude-plugins

# Add a community marketplace
/plugin marketplace add community/awesome-claude-plugins
```

### Add Git repositories

You can add marketplaces from any Git hosting service:

```bash
# GitLab
/plugin marketplace add https://gitlab.com/company/plugins.git

# Bitbucket
/plugin marketplace add https://bitbucket.org/company/plugins.git

# Self-hosted Git
/plugin marketplace add https://git.company.com/team/plugins.git
```

### Add local marketplaces for development

When developing plugins locally, add your development directory as a marketplace:

```bash
# Add a directory containing marketplace.json
/plugin marketplace add ./my-marketplace

# Add a specific marketplace.json file
/plugin marketplace add ./path/to/marketplace.json

# Add from a URL
/plugin marketplace add https://url.of/marketplace.json
```

### Install plugins from marketplaces

Once you've added a marketplace, you can install plugins:

```bash
# Install specific plugin
/plugin install plugin-name@marketplace-name

# Or use interactive menu
/plugin
```

The interactive menu (`/plugin`) provides:
- List of all available plugins from all marketplaces
- Plugin descriptions and versions
- Installation status
- Easy enable/disable/uninstall options

## Create your own marketplace

### Prerequisites for marketplace creation

- Git repository (GitHub, GitLab, or any Git host)
- Understanding of JSON file format
- One or more plugins to distribute

### Marketplace file structure

Create a `marketplace.json` file in your repository root:

```json
{
  "name": "company-tools",
  "description": "Internal development tools and workflows",
  "version": "1.0.0",
  "owner": {
    "name": "DevTools Team",
    "email": "[email protected]",
    "url": "https://github.com/company"
  },
  "pluginRoot": "./plugins",
  "plugins": [
    {
      "name": "code-formatter",
      "source": "./plugins/formatter",
      "description": "Automatic code formatting on save",
      "version": "2.1.0",
      "author": {
        "name": "DevTools Team"
      },
      "keywords": ["formatting", "code-style", "automation"]
    },
    {
      "name": "deploy-helper",
      "source": "https://github.com/company/deploy-plugin.git",
      "description": "Streamlined deployment workflows",
      "version": "1.5.0",
      "author": {
        "name": "DevOps Team"
      }
    }
  ]
}
```

### Marketplace schema

#### Required fields

```json
{
  "name": "marketplace-name",
  "owner": {
    "name": "Owner Name"
  },
  "plugins": []
}
```

#### Complete schema

```json
{
  "name": "marketplace-name",
  "description": "Marketplace description",
  "version": "1.0.0",
  "owner": {
    "name": "Owner Name",
    "email": "[email protected]",
    "url": "https://example.com"
  },
  "homepage": "https://marketplace.example.com",
  "repository": {
    "type": "git",
    "url": "https://github.com/owner/repo.git"
  },
  "pluginRoot": "./plugins",
  "plugins": [
    {
      "name": "plugin-name",
      "source": "./path/or/url",
      "description": "Plugin description",
      "version": "1.0.0",
      "author": {
        "name": "Author Name",
        "email": "[email protected]",
        "url": "https://author.example.com"
      },
      "keywords": ["tag1", "tag2"],
      "license": "MIT",
      "homepage": "https://plugin.example.com",
      "repository": {
        "type": "git",
        "url": "https://github.com/owner/plugin.git"
      }
    }
  ]
}
```

### Field descriptions

**Marketplace fields:**
- `name` (string, required): Unique marketplace identifier
- `description` (string, optional): Brief marketplace description
- `version` (string, optional): Marketplace version
- `owner` (object, required): Owner information
  - `name` (string, required): Owner name
  - `email` (string, optional): Contact email
  - `url` (string, optional): Owner website
- `homepage` (string, optional): Marketplace homepage URL
- `repository` (object, optional): Source repository info
- `pluginRoot` (string, optional): Default directory for relative plugin paths

**Plugin entry fields:**
- `name` (string, required): Unique plugin identifier
- `source` (string, required): Plugin location (relative path, git URL, etc.)
- `description` (string, required): Brief plugin description
- `version` (string, required): Plugin version
- `author` (object, optional): Plugin author information
- `keywords` (array, optional): Tags for discoverability
- `license` (string, optional): License identifier
- `homepage` (string, optional): Plugin homepage
- `repository` (object, optional): Plugin source repository

### Plugin source types

Marketplaces support various plugin source types:

#### Relative paths

```json
{
  "name": "local-plugin",
  "source": "./plugins/my-plugin"
}
```

Uses marketplace's `pluginRoot` if specified.

#### Absolute paths

```json
{
  "name": "absolute-plugin",
  "source": "/absolute/path/to/plugin"
}
```

#### Git URLs

```json
{
  "name": "git-plugin",
  "source": "https://github.com/org/plugin.git"
}
```

#### GitHub shorthand

```json
{
  "name": "github-plugin",
  "source": "owner/repo"
}
```

#### Git with branch/tag

```json
{
  "name": "versioned-plugin",
  "source": "https://github.com/org/plugin.git#v2.0.0"
}
```

## Hosting options

### GitHub (recommended)

GitHub provides the best experience for marketplace hosting:

1. Create a repository for your marketplace
2. Add `marketplace.json` to the root
3. Add your plugins as subdirectories or submodules
4. Push to GitHub

Structure:

```
claude-plugins/
├── marketplace.json
├── README.md
└── plugins/
    ├── formatter/
    │   └── .claude-plugin/
    │       └── plugin.json
    └── linter/
        └── .claude-plugin/
            └── plugin.json
```

Users can add with:

```bash
/plugin marketplace add your-org/claude-plugins
```

### Other Git services

GitLab, Bitbucket, and self-hosted Git work similarly:

1. Create repository
2. Add `marketplace.json`
3. Share full Git URL

Users add with full URL:

```bash
/plugin marketplace add https://gitlab.com/your-org/plugins.git
```

### Local development

For plugin development and testing:

```bash
# Create local marketplace
mkdir ~/my-plugins
cd ~/my-plugins

# Create marketplace.json
cat > marketplace.json << 'EOF'
{
  "name": "dev-marketplace",
  "owner": {"name": "Developer"},
  "pluginRoot": "./plugins",
  "plugins": [
    {
      "name": "test-plugin",
      "source": "./plugins/test-plugin",
      "description": "Testing new features",
      "version": "0.1.0"
    }
  ]
}
EOF

# Add to Claude Code
/plugin marketplace add ~/my-plugins
```

## Marketplace management

### List marketplaces

```bash
/plugin marketplace list
```

Shows all configured marketplaces with their sources and plugin counts.

### Refresh marketplace

```bash
/plugin marketplace refresh marketplace-name
```

Updates the marketplace data, fetching the latest plugin list and versions.

### Remove marketplace

```bash
/plugin marketplace remove marketplace-name
```

Removes the marketplace configuration. Installed plugins from that marketplace remain installed but won't receive updates.

## Best practices

### For marketplace creators

**Naming conventions**
- Use clear, descriptive marketplace names
- Choose concise plugin names (lowercase with hyphens)
- Use semantic versioning for all versions

**Plugin metadata**
- Provide comprehensive descriptions
- Include relevant keywords for discoverability
- Specify licenses clearly
- Add author contact information

**Organization**
- Group related plugins logically
- Use consistent directory structure
- Document plugin requirements and dependencies
- Provide README with usage examples

**Version management**
- Update plugin versions consistently
- Maintain CHANGELOG for plugins
- Tag releases in Git
- Test plugins before publishing updates

**Documentation**
- Create comprehensive marketplace README
- Document each plugin's features
- Provide examples and use cases
- Include troubleshooting guides

### For marketplace users

**Discovering plugins**
- Browse available marketplaces
- Search by keywords
- Check plugin descriptions and versions
- Review author information

**Installing plugins**
- Start with well-documented plugins
- Check version compatibility
- Read plugin documentation
- Test in non-critical projects first

**Updating plugins**
- Regularly refresh marketplaces
- Check for plugin updates
- Review changelogs before updating
- Test updates before team-wide deployment

## Example marketplace configurations

### Team internal tools

```json
{
  "name": "acme-dev-tools",
  "description": "ACME Corp internal development tools",
  "owner": {
    "name": "ACME DevTools Team",
    "email": "[email protected]"
  },
  "pluginRoot": "./plugins",
  "plugins": [
    {
      "name": "acme-formatter",
      "source": "./plugins/formatter",
      "description": "ACME code style formatter",
      "version": "1.0.0"
    },
    {
      "name": "acme-deployer",
      "source": "./plugins/deployer",
      "description": "Deploy to ACME infrastructure",
      "version": "2.1.0"
    }
  ]
}
```

### Community plugins

```json
{
  "name": "awesome-claude-plugins",
  "description": "Community-curated Claude Code plugins",
  "owner": {
    "name": "Community",
    "url": "https://github.com/community"
  },
  "plugins": [
    {
      "name": "react-helper",
      "source": "community/react-plugin",
      "description": "React development utilities",
      "version": "1.5.0",
      "keywords": ["react", "javascript", "frontend"]
    },
    {
      "name": "python-tools",
      "source": "https://github.com/dev/python-plugin.git",
      "description": "Python development tools",
      "version": "2.0.0",
      "keywords": ["python", "testing", "linting"]
    }
  ]
}
```

### Language/framework specific

```json
{
  "name": "rust-plugins",
  "description": "Plugins for Rust development",
  "owner": {
    "name": "Rust Tools Team"
  },
  "plugins": [
    {
      "name": "cargo-helper",
      "source": "rust-tools/cargo-plugin",
      "description": "Cargo workflow automation",
      "version": "1.2.0",
      "keywords": ["rust", "cargo", "build"]
    },
    {
      "name": "rust-analyzer-integration",
      "source": "rust-tools/analyzer-plugin",
      "description": "Enhanced Rust analyzer integration",
      "version": "1.0.0",
      "keywords": ["rust", "lsp", "analysis"]
    }
  ]
}
```

## Troubleshooting

### Common issues

**Marketplace not loading**
- Verify `marketplace.json` exists in repository root
- Check JSON syntax validity
- Ensure all required fields are present
- Verify Git URL is accessible

**Plugin installation fails**
- Check plugin source path is correct
- Verify plugin has valid `plugin.json`
- Ensure Git URL is accessible (if using Git source)
- Check for conflicting plugin names

**Marketplace refresh fails**
- Verify network connectivity
- Check Git credentials (for private repos)
- Ensure repository hasn't been deleted or moved
- Try removing and re-adding marketplace

**Plugin not appearing**
- Refresh marketplace: `/plugin marketplace refresh marketplace-name`
- Check plugin is listed in `marketplace.json`
- Verify plugin source is accessible
- Check for JSON syntax errors

### Getting help

If you encounter issues:

1. Check marketplace and plugin JSON syntax
2. Verify all paths and URLs are correct
3. Test Git URLs independently
4. Review Claude Code logs with `--debug` flag
5. Consult documentation and examples
6. Ask in community forums or support channels

## Next steps

### For users
- **Discover**: Browse community marketplaces
- **Install**: Try popular plugins for your stack
- **Customize**: Configure plugins for your workflow

### For creators
- **Build**: Create plugins for your team
- **Publish**: Share useful plugins with community
- **Maintain**: Keep plugins updated and documented

### For organizations
- **Deploy**: Set up internal marketplace
- **Govern**: Establish plugin policies
- **Scale**: Standardize tools across teams
