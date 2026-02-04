# AI-Scaffolding

A Copier-based project scaffolding system that generates AI-ready project structures with appropriate instruction files for Google Antigravity, Anthropic Claude Code, and Cursor AI.

## Features

- 🚀 **Multiple Project Types**: Python, iOS (SwiftUI), macOS (SwiftUI), Website (HTML/CSS/JS), PHP, Next.js, TypeScript, C#/.NET
- 🤖 **AI Tool Support**: Choose between Antigravity, Claude, Cursor, JetBrains, or generate files for all
- 📝 **Smart Templates**: Project-type-specific coding standards and configurations
- 🎯 **Skills Included**: Modular skills for code-style, git-workflow, testing, and more
- 🎲 **Fun Defaults**: Random developer names like "404 Developer Not Found"
- ⚙️ **Auto Git Setup**: Optional Git initialization with initial commit
- 🔧 **Global Skills**: Optional installation of Claude/Cursor skills to home directory

## Installation

```bash
# Install Copier
pip install copier

# Clone this repository
git clone https://github.com/yourusername/AI-Scaffolding.git
cd AI-Scaffolding
```

## Usage

### Interactive Mode (Recommended)

```bash
copier copy . /path/to/new/project
```

You'll be prompted for:
- Project name
- Project type (Python, iOS, macOS, Website, PHP, NextJS, TypeScript, CSharp)
- AI tool preference (Antigravity, Claude, Cursor, JetBrains, or All)
- Git initialization
- Testing setup
- Global skills installation (for Claude/Cursor)
- Author information

### Non-Interactive Mode

```bash
copier copy --trust \
  --data project_name="My Awesome App" \
  --data project_type="Python" \
  --data ai_tool="Antigravity" \
  --data use_git=true \
  --data include_testing=true \
  --data author_name="Your Name" \
  --data author_email="your.email@example.com" \
  . /path/to/new/project
```

> **Note**: Add `--data install_global_skills=true` to install Claude/Cursor skills to your home directory.

## Project Types

### Python
- **Tools**: Ruff (formatter/linter), pytest
- **Files**: `pyproject.toml`, `src/` directory structure
- **Standards**: Python 3.10+, type hints, Google-style docstrings

### iOS / macOS (SwiftUI)
- **Tools**: SwiftFormat, SwiftLint
- **Files**: `.swiftlint.yml`, `.swiftformat`
- **Standards**: Swift 5.9+, MVVM architecture

### Website (HTML/CSS/JS)
- **Tools**: Vite
- **Files**: `package.json`, basic HTML/CSS/JS structure
- **Standards**: Semantic HTML5, modern CSS, ES6+

### PHP
- **Tools**: Composer
- **Files**: `composer.json`, `index.php`
- **Standards**: PHP 8.1+, PSR-12, PSR-4 autoloading

### Next.js
- **Tools**: Next.js, React, TypeScript
- **Files**: `package.json`, Next.js project structure
- **Standards**: React best practices, TypeScript

### TypeScript
- **Tools**: TypeScript compiler, ESLint, Prettier
- **Files**: `tsconfig.json`, `package.json`
- **Standards**: TypeScript 5.0+, strict mode, modern ES features

### C# / .NET
- **Tools**: .NET SDK, Roslyn analyzers
- **Files**: `.csproj`, `Program.cs`
- **Standards**: .NET 8.0+, nullable reference types, async/await

## AI Instruction Files

Based on your `ai_tool` selection, the following files will be generated:

- **Antigravity**: `ANTIGRAVITY.md` - Instructions for Google's Antigravity AI
- **Claude**: `CLAUDE.md` - Memory file for Anthropic's Claude Code
- **Cursor**: `AGENTS.md` - Instructions for Cursor AI
- **JetBrains**: `JETBRAINS.md` - Instructions for JetBrains AI Assistant (IntelliJ IDEA, PyCharm, WebStorm, PhpStorm, etc.)
- **All**: All four files above

Each file contains:
- Project-specific coding standards
- Git workflow guidelines
- Testing conventions (if enabled)
- Quick reference commands
- IDE-specific tips and shortcuts (for JetBrains)

## Skills

The following skills are automatically included based on project type:

| Skill | Python | iOS/macOS | Web/PHP |
|-------|--------|-----------|---------|
| `git-workflow` | ✅ | ✅ | ✅ |
| `code-style` | ✅ | - | - |
| `swift-style` | - | ✅ | - |
| `web-style` | - | - | ✅ |
| `php-style` | - | - | PHP only |
| `testing` | ✅ | ✅ | ✅ |
| `llm-development` | ✅ | - | - |

## Global Skills Installation

The scaffolding system can optionally install Claude and Cursor global skills to your home directory during project creation. This makes these skills available across all your projects.

### What Gets Installed

When you enable global skills installation, the following are copied to your home directory:

**Claude Skills** (`~/.claude/skills/`):
- `code-simplifier` - Simplify complex code
- `commit-push-pr` - Automated commit, push, and PR creation
- `techdebt` - Technical debt tracking

**Claude Agents** (`~/.claude/agents/`):
- Custom subagents for specialized tasks

**Cursor Skills** (`~/.cursor/skills-cursor/`):
- Same skills as Claude, adapted for Cursor

**Cursor Agents** (`~/.cursor/agents/`):
- Custom subagents for Cursor

### How It Works

1. During scaffolding, you'll be asked: "Install Claude/Cursor global skills to home directory?"
2. If you answer "Yes", the skills are copied to your home directory
3. **Existing skills are NEVER overwritten** - only new skills are installed
4. The installation only happens if you selected Claude, Cursor, or All as your AI tool

### Manual Installation

You can also manually install these skills later:

```bash
# For Claude
mkdir -p ~/.claude/skills ~/.claude/agents
cp -r template/claude_personal_skills/* ~/.claude/skills/
cp -r template/claude_subagents/* ~/.claude/agents/

# For Cursor
mkdir -p ~/.cursor/skills-cursor ~/.cursor/agents
cp -r template/cursor_personal_skills/* ~/.cursor/skills-cursor/
cp -r template/cursor_subagents/* ~/.cursor/agents/
```

## Updating Existing Projects

One of Copier's best features is the ability to update projects when the template changes:

```bash
cd /path/to/your/project
copier update
```

This will pull the latest template changes and apply them to your project.

## Examples

### Create a Python CLI Tool

```bash
copier copy . ~/Projects/my-cli-tool
# Select: Python, Antigravity, Yes to Git, Yes to Testing
```

### Create an iOS App

```bash
copier copy . ~/Projects/MyiOSApp
# Select: iOS, All (for all AI tools), Yes to Git, Yes to Testing
```

### Create a PHP Website

```bash
copier copy . ~/Projects/my-website
# Select: PHP, Claude, Yes to Git, No to Testing
```

## Customization

### Modifying Templates

All templates are in the `template/` directory with `.jinja` extension. They use Jinja2 syntax for conditionals and variables.

Example:
```jinja
{% if project_type == "Python" -%}
# Python-specific content
{% elif project_type == "iOS" -%}
# iOS-specific content
{% endif %}
```

### Adding New Project Types

1. Add the new type to `copier.yml` under `project_type.choices`
2. Update template files with conditional logic for the new type
3. Create type-specific configuration files if needed
4. Update this README

### Adding New Skills

1. Create a new directory in `skills/`
2. Add a `SKILL.md` file with YAML frontmatter
3. The skill will automatically be copied to generated projects

## Project Structure

```
AI-Scaffolding/
├── copier.yml              # Copier configuration
├── template/               # Template files
│   ├── ANTIGRAVITY.md.jinja
│   ├── CLAUDE.md.jinja
│   ├── AGENTS.md.jinja
│   ├── README.md.jinja
│   ├── .gitignore.jinja
│   ├── pyproject.toml.jinja
│   ├── .swiftlint.yml.jinja
│   ├── .swiftformat.jinja
│   ├── composer.json.jinja
│   ├── package.json.jinja
│   ├── skills/             # Project-local skills
│   ├── claude_personal_skills/  # Claude global skills
│   ├── claude_subagents/        # Claude subagents
│   ├── cursor_personal_skills/  # Cursor global skills
│   └── cursor_subagents/        # Cursor subagents
├── skills/                 # Source skills
│   ├── code-style/
│   ├── git-workflow/
│   ├── llm-development/
│   └── testing/
├── ANTIGRAVITY.md          # This repo's AI instructions
├── CLAUDE.md               # This repo's Claude memory
├── AGENTS.md               # This repo's Cursor instructions
└── README.md               # This file
```

## Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test with `copier copy . /tmp/test-project`
5. Submit a pull request

## License

MIT

## Credits

Inspired by:
- [Copier](https://copier.readthedocs.io/) - The template system
- [Cookiecutter](https://cookiecutter.readthedocs.io/) - Original inspiration
- Boris Cherny's Claude Code tips - Workflow guidelines

---

**Author**: {{ author_name }} (with a touch of humor 😄)
