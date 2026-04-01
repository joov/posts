# AGENTS.md

This file provides guidance to opencode when working in this repository.

## Who I Am

I am a Principal Data & AI Strategy consultant and CISO. I look at new developents in Data & AI. I like to see behind the scenes and to share insights for deeper understanding or better strategy.

**Name:** Johannes Wenzel
**Role:** Principal Data & AI Strategy consultant and CISO

## How This System Works

This is a personal project management system to create medium posts and designed to work with Opencode. It organizes:

- **Tasks/** - Active work and backlog items
- **Posts/** - Individual Posts each containing a medium post
- **Workflows/** - Repeatable processes and playbooks
- **Knowledge/** - Reference materials, research, and people notes
- **Templates/** - Reusable document templates

## Key Directories

```
Tasks/           → Active tasks and backlog
Posts/           → individual posts each creating a post for medium
Knowledge/       → Reference, Research, People notes
Templates/       → Document templates
Tools/           → Scripts and utilities
_Registry/       → System documentation (tags, tools, MCPs)
_temp/           → Scratch space
```

## Key Commands

| Say / Command | Does | Skill |
|---------------|------|-------|
| "suggest" | suggest topic for next post | -- |
| `/collect` | collect knowledge for project at hand | collect |
| `/plan` | plan content and logical structure of the post | plan |
| `/draw` | create mermaid graphs to include in the post | draw |
| `/write` | write the post using plan and graphs | write |
| `/review` | review article for structure, clarity, and accuracy | review |
| `/summarize` | create a LinkedIn abstract with hooks and emojis | summarize |
| `/create [name]` | create new project for a new post | create |

Always update STATUS.md after executing a command or skill

## Context Files

When starting work, Claude should read:

- `GOALS.md` - Current objectives and stakeholders
- `Tasks/active.md` - What I'm currently working on

## Notes

- All files are Markdown
- Templates in `Templates/` for new documents
- Write in English
