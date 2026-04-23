# Agent Skills

A collection of specialized skills for AI agents, designed to work with opencode and similar agent systems.

## Installation

### Install All Skills

```bash
# Clone all skills to your agent's skill directory
git clone https://github.com/kaka/skills.git ~/.agents/skills
```

### Install RubyLLM Skills Only

```bash
# Clone only RubyLLM skills
git clone https://github.com/kaka/skills.git ~/.agents/skills/rubyllm
```

### Install Core Skills Only

```bash
# Clone repository
git clone https://github.com/kaka/skills.git /tmp/skills

# Copy core skills
cp -r /tmp/skills/continuous-development ~/.agents/skills/
cp -r /tmp/skills/continuous-improvement ~/.agents/skills/
cp -r /tmp/skills/git-workflow ~/.agents/skills/

# Clean up
rm -rf /tmp/skills
```

### Install Individual Skills

The entire repository is only ~200KB, so cloning everything is fast:

```bash
# Clone everything (only ~200KB)
git clone https://github.com/kaka/skills.git /tmp/skills

# Copy only the skills you need
cp -r /tmp/skills/rubyllm/tools ~/.agents/skills/rubyllm-tools
cp -r /tmp/skills/rubyllm/agents ~/.agents/skills/rubyllm-agents
cp -r /tmp/skills/rubyllm/rails ~/.agents/skills/rubyllm-rails

# Clean up
rm -rf /tmp/skills
```

**Or use sparse checkout (advanced):**

```bash
# Clone without files, then select specific skills
git clone --filter=blob:none --sparse https://github.com/kaka/skills.git ~/.agents/skills/rubyllm-tools
cd ~/.agents/skills/rubyllm-tools
git sparse-checkout init --cone
git sparse-checkout set rubyllm/tools
git checkout master
# Move files to correct location
mv rubyllm/tools/* .
rm -rf rubyllm
```

### Install to Custom Directory

```bash
# Clone to any directory your agent uses
git clone https://github.com/kaka/skills.git ~/my-agent-skills/rubyllm
```

## Available Skills

### Core Agent Skills

Essential skills for agent development workflow:

| Skill | Description |
|-------|-------------|
| [continuous-development/](continuous-development/SKILL.md) | Keep development continuous, prioritized, and consistent across sessions |
| [continuous-improvement/](continuous-improvement/SKILL.md) | Continuously improve the development system by fixing process failures |
| [git-workflow/](git-workflow/SKILL.md) | Clean git workflow: work on master, clear commits, no prefixes |

### RubyLLM Ecosystem (v1.14.1)

Comprehensive skills for building AI-powered Ruby applications:

| Skill | Version | Description |
|-------|---------|-------------|
| [SKILL.md](SKILL.md) | 1.14.1 | Main RubyLLM API - chat, providers, configuration |
| [tools/](tools/SKILL.md) | - | Function calling, tool creation, security |
| [agents/](agents/SKILL.md) | - | Class-based agents, runtime context |
| [rails/](rails/SKILL.md) | - | Rails integration, Hotwire, ActiveRecord |
| [embeddings/](embeddings/SKILL.md) | - | Vector generation, semantic search, RAG |
| [image-generation/](image-generation/SKILL.md) | - | DALL-E 3, image editing, masks |
| [audio-transcription/](audio-transcription/SKILL.md) | - | Whisper, diarization, timestamps |
| [moderation/](moderation/SKILL.md) | - | Content safety, thresholds |
| [schema/](schema/SKILL.md) | 0.3.0 | JSON Schema DSL |
| [mcp/](mcp/SKILL.md) | 1.0.0 | Model Context Protocol |
| [instrumentation/](instrumentation/SKILL.md) | 0.3.1 | ActiveSupport notifications |
| [monitoring/](monitoring/SKILL.md) | 0.3.2 | Dashboards & alerts |
| [red_candle/](red_candle/SKILL.md) | 0.2.0 | Local LLM execution |
| [tribunal/](tribunal/SKILL.md) | 0.1.1 | LLM testing & evaluation |
| [opentelemetry/](opentelemetry/SKILL.md) | 0.4.0 | OpenTelemetry tracing |

## For Contributors

### Using Symlinks

Symlinks allow you to develop in a central location while your agent uses the skills from `~/.agents/skills/`.

#### Setup

```bash
# 1. Fork the repository on GitHub, then clone your fork
git clone https://github.com/yourusername/skills.git ~/Code/kaka/skills
cd ~/Code/kaka/skills

# 2. Create symlinks for testing with your agent
# RubyLLM skills symlink
ln -s ~/Code/kaka/skills/rubyllm ~/.agents/skills/rubyllm

# Core skills symlinks (optional - if you want to test these too)
ln -s ~/Code/kaka/skills/continuous-development ~/.agents/skills/continuous-development
ln -s ~/Code/kaka/skills/continuous-improvement ~/.agents/skills/continuous-improvement
ln -s ~/Code/kaka/skills/git-workflow ~/.agents/skills/git-workflow
```

**Note:** Remove any existing directories first:
```bash
rm -rf ~/.agents/skills/rubyllm  # Only if it exists as a directory
```

#### Workflow

```bash
# Make changes in your development directory
cd ~/Code/kaka/skills/rubyllm
vim tools/SKILL.md

# Test with your agent (symlink points to the same files)
# Your agent uses ~/.agents/skills/rubyllm/ (which is ~/Code/kaka/skills/rubyllm)

# When ready, commit in development directory
cd ~/Code/kaka/skills
git add rubyllm/tools/SKILL.md
git commit -m "Improve tools documentation"

# Push to your fork
git push origin master

# Open a pull request on GitHub
```

### Why Symlinks?

- **Instant sync**: Changes are immediately available to your agent
- **Single source of truth**: No need to sync between worktrees
- **Simple workflow**: Edit once, test immediately
- **Agent compatibility**: Works naturally with agent systems that expect skills in `~/.agents/skills/`
- **No git complexity**: No worktree branches to manage

### Contribution Guidelines

1. **Fork** the repository on GitHub
2. **Clone** your fork locally
3. **Create symlinks** for testing:
   ```bash
   ln -s ~/Code/kaka/skills/rubyllm ~/.agents/skills/rubyllm
   ```
4. **Make changes** in your development directory
5. **Test** with your agent (changes are instant via symlink)
6. **Commit** with clear messages:
   ```bash
   git add .
   git commit -m "Add new feature to tools skill"
   ```
7. **Push** to your fork
8. **Open a Pull Request**

### Commit Guidelines

- One commit per completed feature/fix
- Short, clear commit messages (no `feat:`, `chore:` prefixes)
- Test before committing
- Stage specific files: `git add <file>` (never `git add .`)

## Directory Structure

```
~/Code/kaka/skills/              # Development repository
├── .git/                         # Git repository
├── .gitignore
├── LICENSE
├── README.md
├── continuous-development/       # Core skill: continuous development workflow
├── continuous-improvement/       # Core skill: continuous improvement process
├── git-workflow/                 # Core skill: clean git workflow
└── rubyllm/                      # All RubyLLM skills
    ├── SKILL.md
    ├── tools/
    ├── agents/
    ├── rails/
    └── ...

~/.agents/skills/                # Agent's skill directory (symlinks)
├── continuous-development/       # Symlink to ~/Code/kaka/skills/continuous-development
├── continuous-improvement/       # Symlink to ~/Code/kaka/skills/continuous-improvement
├── git-workflow/                 # Symlink to ~/Code/kaka/skills/git-workflow
└── rubyllm/                      # Symlink to ~/Code/kaka/skills/rubyllm
    ├── SKILL.md
    ├── tools/
    ├── agents/
    └── ...
```

## Updating Skills

### For Users

```bash
# If you cloned directly to ~/.agents/skills/rubyllm
cd ~/.agents/skills/rubyllm
git pull origin master
```

### For Contributors

```bash
# Pull latest changes to development repo
cd ~/Code/kaka/skills
git pull origin master

# Symlinks automatically point to updated files
# No sync needed - your agent sees changes immediately
```

## Adding New Skills

When adding a new skill:

1. **Create the skill directory**:
   ```bash
   mkdir ~/Code/kaka/skills/rubyllm/newskill
   ```

2. **Create SKILL.md** with frontmatter:
   ```markdown
   ---
   name: newskill
   version: 1.0.0
   description: |
     Description of what this skill does
   allowed-tools:
     - Bash(command *)
   ---
   
   # Skill Name
   
   Documentation...
   ```

3. **Update README.md** to include the new skill in the table

4. **Test locally** using your symlink (changes are instant)

5. **Commit and push**:
   ```bash
   cd ~/Code/kaka/skills
   git add rubyllm/newskill
   git commit -m "Add newskill"
   git push
   ```

## License

MIT License - see LICENSE file

## Support

- **Issues**: Open an issue on GitHub
- **Discussions**: GitHub Discussions for questions
- **Documentation**: Each skill has its own SKILL.md with detailed usage
