# Agent Skills

A collection of specialized skills for AI agents, designed to work with opencode and similar agent systems.

## Installation

### Install All Skills

```bash
# Clone directly to your agent's skill directory
git clone https://github.com/kaka/skills.git ~/.agents/skills/rubyllm
```

### Install Individual Skills

Use Git sparse checkout to download only specific skills:

```bash
# Download only the tools skill
git clone --filter=blob:none --sparse https://github.com/kaka/skills.git ~/.agents/skills/rubyllm-tools
cd ~/.agents/skills/rubyllm-tools
git sparse-checkout set rubyllm/tools
git checkout master -- rubyllm/tools/*
mv rubyllm/tools/* .
rm -rf rubyllm
cd ~
```

**Multiple skills:**

```bash
# Download tools, agents, and rails
git clone --filter=blob:none --sparse https://github.com/kaka/skills.git ~/.agents/skills/my-skills
cd ~/.agents/skills/my-skills
git sparse-checkout set rubyllm/tools rubyllm/agents rubyllm/rails
git checkout master -- rubyllm/tools/* rubyllm/agents/* rubyllm/rails/*
mv rubyllm/tools/* ~/.agents/skills/rubyllm-tools/
mv rubyllm/agents/* ~/.agents/skills/rubyllm-agents/
mv rubyllm/rails/* ~/.agents/skills/rubyllm-rails/
rm -rf ~/.agents/skills/my-skills
```

**Simple approach (clone once, pick what you need):**

```bash
# Clone to temporary location
git clone --depth 1 https://github.com/kaka/skills.git /tmp/skills

# Copy only the skills you need
cp -r /tmp/skills/rubyllm/tools ~/.agents/skills/rubyllm-tools
cp -r /tmp/skills/rubyllm/agents ~/.agents/skills/rubyllm-agents

# Clean up
rm -rf /tmp/skills
```

### Install to Custom Directory

```bash
# Clone to any directory your agent uses
git clone https://github.com/kaka/skills.git ~/my-agent-skills/rubyllm
```

## Available Skills

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

### Using Git Worktrees

Worktrees allow you to maintain a local copy for testing while contributing to the main repository.

#### Setup

```bash
# 1. Fork the repository on GitHub, then clone your fork
git clone https://github.com/yourusername/skills.git ~/Code/kaka/skills
cd ~/Code/kaka/skills

# 2. Create a worktree for testing with your agent
# This creates a separate branch for local testing
git worktree add -b local-testing ~/.agents/skills/rubyllm master

# 3. Keep main repo for development, worktree for testing
# ~/Code/kaka/skills/        <- Development (master branch)
# ~/.agents/skills/rubyllm/  <- Testing (local-testing branch)
```

#### Workflow

```bash
# Make changes in your development directory
cd ~/Code/kaka/skills/rubyllm
vim tools/SKILL.md

# Test with your agent (worktree has the changes)
# Your agent uses ~/.agents/skills/rubyllm/

# When ready, commit in development directory
cd ~/Code/kaka/skills
git add rubyllm/tools/SKILL.md
git commit -m "Improve tools documentation"

# Sync to worktree for more testing
git worktree list  # Verify worktree is up to date

# Push to your fork
git push origin master

# Open a pull request on GitHub
```

#### Merging Test Branch Back to Master

```bash
# After testing in worktree, merge changes back
cd ~/Code/kaka/skills
git checkout master
git merge local-testing
git push origin master
```

#### Worktree Commands

```bash
# List all worktrees
git worktree list

# Add a worktree
git worktree add <path> <branch>

# Remove a worktree
git worktree remove <path>

# Clean up stale worktrees
git worktree prune
```

### Why Worktrees?

- **True separation**: Development and testing environments are independent
- **No symlinks**: Each directory is a proper git working tree
- **Branch flexibility**: Test on separate branches without affecting main development
- **Clean workflow**: Standard git commands work in both locations
- **Agent compatibility**: Works naturally with agent systems that expect skills in `~/.agents/skills/`

### Contribution Guidelines

1. **Fork** the repository on GitHub
2. **Clone** your fork locally
3. **Create a worktree** for testing:
   ```bash
   git worktree add -b testing ~/.agents/skills/rubyllm master
   ```
4. **Make changes** in your development directory
5. **Test** with your agent using the worktree
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
└── rubyllm/                      # All RubyLLM skills
    ├── SKILL.md
    ├── tools/
    ├── agents/
    ├── rails/
    └── ...

~/.agents/skills/rubyllm/        # Worktree for testing
├── .git                          # Worktree git file
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

# Worktree automatically stays in sync
# Or manually update:
cd ~/.agents/skills/rubyllm
git pull
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

4. **Test locally** using your worktree

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
