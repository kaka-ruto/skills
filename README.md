# Agent Skills

A collection of specialized skills for AI agents, designed to work with opencode and similar agent systems.

## Installation

### Quick Install (Recommended)

```bash
# Clone the repository
git clone https://github.com/kaka/skills.git ~/Code/kaka/skills

# Symlink all skills
ln -s ~/Code/kaka/skills/rubyllm ~/.agents/skills/rubyllm
```

### Install Individual Skills

```bash
# Clone the repository
git clone https://github.com/kaka/skills.git ~/Code/kaka/skills

# Symlink only the skills you need
ln -s ~/Code/kaka/skills/rubyllm/tools ~/.agents/skills/rubyllm-tools
ln -s ~/Code/kaka/skills/rubyllm/agents ~/.agents/skills/rubyllm-agents
ln -s ~/Code/kaka/skills/rubyllm/rails ~/.agents/skills/rubyllm-rails
```

### Install to Custom Directory

```bash
# Clone to your preferred location
git clone https://github.com/kaka/skills.git ~/my-skills

# Symlink to your agent's skill directory
ln -s ~/my-skills/rubyllm ~/.agents/skills/rubyllm
```

## For Contributors

### Using Worktrees (Advanced)

Worktrees allow you to test changes with your agent while developing:

```bash
# Main repo (for development)
git clone https://github.com/kaka/skills.git ~/Code/kaka/skills

# Worktree (for testing with agent) - creates separate branch
cd ~/Code/kaka/skills
git worktree add -b testing ~/.agents/skills/rubyllm master
```

This creates a `testing` branch in `~/.agents/skills/rubyllm/` for local testing.

**Workflow:**
1. Develop in `~/Code/kaka/skills/rubyllm/` on `master`
2. Test in `~/.agents/skills/rubyllm/` on `testing` branch
3. Merge `testing` into `master` when ready
4. Push to GitHub

### Simple Symlink Approach

For most users, symlinks are simpler:

```bash
# Development
cd ~/Code/kaka/skills/rubyllm
vim tools/SKILL.md
git add .
git commit -m "Update tools"

# Test immediately (symlink makes changes instant)
# Your agent will use the updated skill
```

## Available Skills

### RubyLLM Ecosystem (v1.14.1)

Comprehensive skills for building AI-powered Ruby applications:

| Skill | Version | Description |
|-------|---------|-------------|
| [rubyllm](rubyllm/SKILL.md) | 1.14.1 | Main RubyLLM API - chat, providers, configuration |
| [rubyllm/tools](rubyllm/tools/SKILL.md) | - | Function calling, tool creation, security |
| [rubyllm/agents](rubyllm/agents/SKILL.md) | - | Class-based agents, runtime context |
| [rubyllm/rails](rubyllm/rails/SKILL.md) | - | Rails integration, Hotwire, ActiveRecord |
| [rubyllm/embeddings](rubyllm/embeddings/SKILL.md) | - | Vector generation, semantic search, RAG |
| [rubyllm/image-generation](rubyllm/image-generation/SKILL.md) | - | DALL-E 3, image editing, masks |
| [rubyllm/audio-transcription](rubyllm/audio-transcription/SKILL.md) | - | Whisper, diarization, timestamps |
| [rubyllm/moderation](rubyllm/moderation/SKILL.md) | - | Content safety, thresholds |
| [rubyllm/schema](rubyllm/schema/SKILL.md) | 0.3.0 | JSON Schema DSL |
| [rubyllm/mcp](rubyllm/mcp/SKILL.md) | 1.0.0 | Model Context Protocol |
| [rubyllm/instrumentation](rubyllm/instrumentation/SKILL.md) | 0.3.1 | ActiveSupport notifications |
| [rubyllm/monitoring](rubyllm/monitoring/SKILL.md) | 0.3.2 | Dashboards & alerts |
| [rubyllm/red_candle](rubyllm/red_candle/SKILL.md) | 0.2.0 | Local LLM execution |
| [rubyllm/tribunal](rubyllm/tribunal/SKILL.md) | 0.1.1 | LLM testing & evaluation |
| [rubyllm/opentelemetry](rubyllm/opentelemetry/SKILL.md) | 0.4.0 | OpenTelemetry tracing |

## For Contributors

### Setting Up Worktrees

Worktrees allow you to work on the public repo while testing locally:

```bash
# 1. Fork and clone
git clone https://github.com/yourusername/cafaye.git ~/Code/kaka/skills
cd ~/Code/kaka/skills

# 2. Create worktree for local agent use
git worktree add ~/.agents/skills/rubyllm rubyllm

# 3. Make changes in either location
# Both point to the same git repository!
vim ~/Code/kaka/skills/rubyllm/tools/SKILL.md

# 4. Test with your agent
# The agent will use ~/.agents/skills/rubyllm/

# 5. Commit and push
cd ~/Code/kaka/skills/rubyllm
git add .
git commit -m "Update tools skill"
git push
```

### Why Worktrees?

- **Single source of truth**: One git repo, two working directories
- **Instant sync**: Changes in either location are immediately available
- **Test locally**: Test with your agent before pushing
- **Clean workflow**: Standard git commands work in both locations
- **Flexible**: Can have different branches checked out in each worktree

### Worktree Commands

```bash
# List all worktrees
git worktree list

# Add a worktree
git worktree add <path> <branch>

# Remove a worktree
git worktree remove <path>

# Prune stale worktrees
git worktree prune
```

### Contribution Workflow

1. **Fork the repository** on GitHub
2. **Clone your fork** locally
3. **Create a worktree** for testing:
   ```bash
   git worktree add ~/.agents/skills/rubyllm rubyllm
   ```
4. **Make your changes** in either location
5. **Test with your agent** to ensure it works
6. **Commit with a clear message**:
   ```bash
   git add .
   git commit -m "Add new feature to tools skill"
   ```
7. **Push to your fork**:
   ```bash
   git push origin master
   ```
8. **Open a Pull Request** on GitHub

### Commit Guidelines

- One commit per completed feature/fix
- Short, clear commit messages (no prefixes like `feat:`, `chore:`)
- Test before committing
- Never use `git add .` - stage specific files

## Directory Structure

```
~/Code/kaka/skills/           # Public repository
├── .git/                      # Git repository
├── rubyllm/                   # RubyLLM skills
│   ├── SKILL.md              # Main skill
│   ├── tools/
│   ├── agents/
│   ├── rails/
│   ├── embeddings/
│   ├── image-generation/
│   ├── audio-transcription/
│   ├── moderation/
│   ├── schema/
│   ├── mcp/
│   ├── instrumentation/
│   ├── monitoring/
│   ├── red_candle/
│   ├── tribunal/
│   └── opentelemetry/
└── .repos/                    # Local source repos (not committed)
    └── ruby_llm/              # Cloned gem repos for reference

~/.agents/skills/             # Local agent directory
└── rubyllm/                  # Symlink or worktree → ~/Code/kaka/skills/rubyllm
```

## Adding New Skills

When adding a new skill:

1. **Create the skill directory**:
   ```bash
   mkdir ~/Code/kaka/skills/newskill
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

3. **Update this README** to include the new skill

4. **Test locally** via the symlink/worktree

5. **Commit and push**

## Symlink vs Worktree

### Symlink (Simpler)
```bash
ln -s ~/Code/kaka/skills/rubyllm ~/.agents/skills/rubyllm
```
- ✅ Simple to understand
- ✅ Instant sync
- ❌ Can be tricky on some systems
- ❌ Doesn't support different branches

### Worktree (More Powerful)
```bash
git worktree add ~/.agents/skills/rubyllm rubyllm
```
- ✅ Full git functionality in both locations
- ✅ Can have different branches
- ✅ Better for complex workflows
- ❌ Slightly more complex setup

**Recommendation**: Use symlinks for simple setups, worktrees for advanced workflows.

## License

MIT License - see LICENSE file

## Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a worktree for testing
3. Make your changes
4. Test with your agent
5. Submit a pull request

See the "For Contributors" section above for detailed instructions.

## Support

- **Issues**: Open an issue on GitHub
- **Discussions**: GitHub Discussions for questions
- **Documentation**: Each skill has its own SKILL.md with detailed usage
