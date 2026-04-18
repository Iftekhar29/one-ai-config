# 🚀 AI Files for Every IDE

> Write AI instructions once. Use them everywhere.

![GitHub repo size](https://img.shields.io/github/repo-size/iftekhar29/one-ai-config)
![GitHub stars](https://img.shields.io/github/stars/iftekhar29/one-ai-config?style=social)
![License](https://img.shields.io/badge/license-MIT-green)

---

## ✨ Why This Exists

Modern development is fragmented across multiple AI tools:

- Claude  
- Cursor  
- Copilot  
- Gemini  
- Codex  
- And more...

Each tool expects different config formats.

❌ Result: duplicated effort, inconsistent behavior  
✅ Solution: **a unified AI instruction system**


---


## 📚 Detailed File-per-Tool Reference

| Tool / IDE | Config file(s) | Scope | Also reads AGENTS.md? |
|------------|---------------|-------|------------------------|
| Claude Code | CLAUDE.md<br>CLAUDE.local.md (personal, gitignored) | Project root + subdirs | Via symlink |
| Cursor | .cursor/rules/*.mdc<br>.cursorrules (legacy) | Glob-scoped per .mdc file | Yes, natively |
| Windsurf | .windsurfrules<br>global_rules.md | Project + global | Yes, natively |
| GitHub Copilot | .github/copilot-instructions.md | Repo-level | Yes, natively |
| VS Code (Copilot) | .github/copilot-instructions.md<br>.amazonq/rules/ (Q Developer) | Extension-dependent | Via Copilot |
| Gemini CLI | GEMINI.md<br>~/.gemini/GEMINI.md (global) | Project + global + subdirs | Yes, natively |
| OpenAI Codex CLI | AGENTS.md | Project root | Native format |
| Cline | .clinerules | Project root | Yes, natively |
| Kiro (AWS) | .kiro/steering/*.md | Spec-driven, per-project | Not confirmed |
| JetBrains (Junie) | Built-in AI chat config | IDE-managed | Not confirmed |
| Antigravity (Google) | GEMINI.md / custom | Agent-first platform | Partial |
| Amp (Sourcegraph) | AGENT.md | Project + subdirs | Native format |
| Replit | .replit.md | Project root | Via symlink |
| Firebase Studio | .idx/airules.md | Project root | Via symlink |
| Amazon Q Developer | .amazonq/rules/ | VS Code + JetBrains | No |

---

## 🧠 Core Idea

> **AGENTS.md is the brain. Everything else is just an entry point.**

- Write rules once  
- Let every AI tool follow them  
- Maintain consistency across your entire workflow  

---

## 📂 File-per-Tool Mapping

| Tool | Config |
|------|--------|
| Claude | CLAUDE.md |
| Cursor | .cursorrules / .cursor/rules |
| Copilot | .github/copilot-instructions.md |
| Gemini | GEMINI.md |
| Codex | AGENTS.md |
| Windsurf | .windsurfrules |
| Cline | .clinerules |

All of them → **delegate to AGENTS.md**

---

## 🏗 Architecture (5 Layers)

### 1. AI Instructions (Behavior)
- AGENTS.md (main)
- Tool-specific entry files

### 2. Context (Knowledge)
- docs/architecture.md  
- docs/prd.md  
- docs/api.md  
- docs/conventions.md  

### 3. Safety (Boundaries)
- .aiignore  
- AGENTS.md rules  

### 4. Tools (Integrations)
- .mcp.json  
- External services (GitHub, DB, APIs)

### 5. Philosophy
- AI reads, not guesses  
- AI respects boundaries  
- AI asks when unsure  

---

## ⚡ Quick Start

```bash
git clone https://github.com/iftekhar29/one-ai-config
```

1. Copy files into your project  
2. Edit AGENTS.md  
3. Done — all AI tools now follow your rules  

---

## 🛠 Usage Tips

- Keep AGENTS.md clean and structured  
- Move details into `/docs`  
- Never duplicate instructions across tools  

---

## 🧩 Example Pattern

Every tool file should look like:

```
Read AGENTS.md
```

That’s it.

---

## 🤝 Contributing

Feel free to:

- Improve structure  
- Add support for new tools  
- Share best practices  

---

## 📌 Philosophy

> You control the AI — not the other way around.

---

## ⭐ Support

If this helped you:
- Star the repo  
- Share with your team  
- Build better AI workflows 🚀
