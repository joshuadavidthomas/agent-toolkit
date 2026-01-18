# Agent Skills

A curated collection of skills for AI coding agents. Skills are packaged instructions and scripts that extend agent capabilities across development, documentation, planning, and professional workflows.

Skills follow the [Agent Skills](https://agentskills.io/) format.

---

## 🧭 Quick Navigation

**[📚 Available Skills](#-available-skills)** • **[🚀 Installation](#-installation)** • **[📖 Skill Structure](#-skill-structure)** • **[🤝 Contributing](#-contributing)** • **[📄 License](#-license)** • **[🔗 Links](#-links)**

---

## 📚 Available Skills

| Category | Skill | Description |
|----------|-------|-------------|
| 🤖 AI Tools | [codex](skills/codex/README.md) | Advanced code analysis with GPT-5.2 |
| 🤖 AI Tools | [gemini](skills/gemini/README.md) | Large-scale review (200k+ context) |
| 🤖 AI Tools | [perplexity](skills/perplexity/README.md) | Web search & research |
| 📝 Documentation | [backend-to-frontend-handoff-docs](skills/backend-to-frontend-handoff-docs/README.md) | API handoff docs for frontend |
| 📝 Documentation | [frontend-to-backend-requirements](skills/frontend-to-backend-requirements/README.md) | Document frontend data needs |
| 📝 Documentation | [c4-architecture](skills/c4-architecture/README.md) | C4 architecture diagrams |
| 📝 Documentation | [draw-io](skills/draw-io/README.md) | Create/edit draw.io diagrams |
| 📝 Documentation | [excalidraw](skills/excalidraw/README.md) | Excalidraw diagram handling |
| 📝 Documentation | [marp-slide](skills/marp-slide/README.md) | Professional Marp slides |
| 📝 Documentation | [mermaid-diagrams](skills/mermaid-diagrams/README.md) | Software diagrams (flowcharts, ERDs, etc.) |
| 🛠️ Development | [command-creator](skills/command-creator/README.md) | Create Claude Code slash commands |
| 🛠️ Development | [session-handoff](skills/session-handoff/README.md) | AI agent session transfers |
| 🛠️ Development | [reducing-entropy](skills/reducing-entropy/README.md) | Minimize codebase size |
| 🎨 Design & Frontend | [design-system-starter](skills/design-system-starter/README.md) | Bootstrap design systems |
| 🎨 Design & Frontend | [openapi-to-typescript](skills/openapi-to-typescript/README.md) | OpenAPI → TypeScript types |
| 🔧 Utilities | [domain-name-brainstormer](skills/domain-name-brainstormer/README.md) | Generate domain name ideas |
| 🔧 Utilities | [meme-factory](skills/meme-factory/README.md) | Generate memes |
| 🔧 Utilities | [web-to-markdown](skills/web-to-markdown/README.md) | Webpage → Markdown conversion |
| 🎯 Planning | [spec-forge](skills/spec-forge/README.md) | Detailed implementation plans |
| 🎯 Planning | [game-changing-features](skills/game-changing-features/README.md) | Find 10x opportunities |
| 🎯 Planning | [requirements-clarity](skills/requirements-clarity/README.md) | Clarify ambiguous requirements |
| 👔 Professional | [professional-communication](skills/professional-communication/README.md) | Master technical communication |
| 🧪 Testing | [qa-test-planner](skills/qa-test-planner/README.md) | Generate test plans & cases |
| 📦 Git | [commit-work](skills/commit-work/README.md) | High-quality git commits |

---

## 🚀 Installation

### Recommended: Universal Installation (Works with all AI agents)

```bash
npx add-skill leonardocouy/agent-skills
```

This method works with multiple AI coding agents:
- ✅ **Claude Code** - Full plugin support
- ✅ **Codex** - Compatible with skill format
- ✅ **Cursor** - Works with agent skills
- ✅ **Other Agent-based tools** - Universal compatibility

### Alternative Methods

**For Claude Code (Plugin)**
```bash
/plugin install agent-skills@leonardocouy
```

**For Claude Code (Manual)**
```bash
cp -r skills/<skill-name> ~/.claude/skills/
```

**For claude.ai**

Add skills to project knowledge or paste SKILL.md contents into the conversation.

---

## 📖 Skill Structure

Each skill contains:
- `SKILL.md` - Detailed instructions for the agent (with YAML frontmatter)
- `README.md` - User-friendly documentation with examples
- `scripts/` - Helper scripts for automation (optional)
- `references/` - Supporting documentation (optional)

---

## 🤝 Contributing

Contributions are welcome! When adding new skills:

1. Follow the [Agent Skills](https://agentskills.io/) format
2. Include both `SKILL.md` (for agents) and `README.md` (for users)
3. Add YAML frontmatter to `SKILL.md` with `name:` and `description:` fields
4. Update this README.md with a link to your skill

---

## 📄 License

MIT

---

## 🔗 Links

- [Agent Skills Format](https://agentskills.io/)
- [Claude Code Documentation](https://docs.anthropic.com/claude/docs)
- [GitHub Repository](https://github.com/leonardocouy/agent-skills)
