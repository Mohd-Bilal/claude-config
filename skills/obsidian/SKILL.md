---
name: obsidian
description: >
  Use this skill whenever the user asks to create, update, or organize notes in their Obsidian vault.
  Triggers include: "create a note", "add to obsidian", "save this to my vault", "make obsidian notes",
  "research and save", or any request to document/summarize a topic into Obsidian. Also triggers when
  the user asks to link notes, build a graph, or organize existing vault content.
---

# Obsidian Note-Taking Skill

## Core Conventions

### 1. Note Naming
- **Index / hub notes**: Always prefix with the topic name.
  - ✅ `JavaScript Event Loop — Index.md`
  - ❌ `Index.md`
- **Subtopic notes**: Use numbered prefixes for ordered series.
  - ✅ `01 - How JS Executes Code.md`
- **Standalone notes**: Use clear, descriptive names. No generic titles like `Notes.md`.

### 2. Folder Organization
- **Always check if a related folder already exists** before creating a new one.
  - If a `JavaScript/` folder exists and the topic is JS-related → put it inside `JavaScript/`.
  - Merge related subtopics into the same folder rather than creating sibling folders.
- Folder structure should reflect the **topic hierarchy**, not the request order.
- Prefer depth over breadth: `JavaScript/Event Loop/` > `JavaScript Event Loop/`

### 3. Note Structure
Every note should follow this template:

```markdown
# Title

Brief 1–2 line summary of what this note covers.

---

## Section 1
...

## Section 2
...

---

## Links
- [[Folder/Related Note 1]]
- [[Folder/Related Note 2]]

## Sources
- [Source Title](URL)
```

- Keep notes **concise and to the point** — no filler, no padding.
- Use code blocks for all code samples.
- Use tables for comparisons.
- Use `>` blockquotes for key insights or callouts.

### 4. Wikilinks
- Always use full vault-relative paths: `[[JavaScript/Event Loop/01 - How JS Executes Code]]`
- Every note must link back to its index/hub note.
- Cross-link between related leaf notes to create a mesh (not just a star) in the graph view.

### 5. Sources
- Every note that pulls from external research **must** include a `## Sources` section at the bottom.
- List each source as a markdown link: `- [Title](URL)`
- If the content is from Claude's own knowledge, note: `> Source: Claude's training knowledge as of [date].`

### 6. Index Notes
- Every folder with 3+ notes should have a hub/index note.
- Index note name: `{Topic Name} — Index.md` (e.g., `Cassandra — Index.md`)
- Index notes must contain:
  - A brief topic summary
  - A linked list of all notes in the folder
  - A mental model or key insight block

---

## Workflow: Creating a Note Set

1. **Check for existing folders** that the topic could belong to.
2. **Create the folder** (if needed) using `obsidian:folder_create`.
3. **Create the index note** first, named `{Topic} — Index.md`.
4. **Create subtopic notes** in logical order, each linking back to the index.
5. **Update the index** with links to all created notes.
6. **Add sources** to every note that uses researched content.

---

## Example: Good vs Bad

| Scenario | ❌ Bad | ✅ Good |
|----------|--------|---------|
| Index file name | `Index.md` | `Cassandra — Index.md` |
| Folder for a JS topic when `JavaScript/` exists | `JS Event Loop/` | `JavaScript/Event Loop/` |
| Note with no sources | *(no sources section)* | `## Sources` at bottom |
| Wikilink style | `[[01 - How JS Executes Code]]` | `[[JavaScript/Event Loop/01 - How JS Executes Code]]` |
| Generic note name | `Notes.md` | `Write Path in Cassandra.md` |
