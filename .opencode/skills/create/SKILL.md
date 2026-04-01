---
name: create
description: Create a new project folder for a new post
license: MIT
compatibility: opencode
---

## What I do

Given a project name (passed as argument):

1. Create folder `Projects/<name>/`
2. Create `Projects/<name>/STATUS.md` with the following template:

```markdown
# <name>

## Status: Draft

## Created: <today's date>

## Description
<short placeholder description>

## Steps
- [ ] Collect knowledge
- [ ] Plan content
- [ ] Create graphs
- [ ] Write post
- [ ] Review and publish
```

## When to use me

Use this when a new project/post needs to be created. The user provides the project name as the first argument, e.g. `/create My Amazing Post`.