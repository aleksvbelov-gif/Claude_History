# Plan: YouTube Content AI Agents for @framedbyhistory

## Context

The user runs an English-language history YouTube channel (@framedbyhistory) focused on biographical stories about royals, historical figures, and scandals. They want to automate 3 tasks:
1. Generating topic ideas
2. Writing full video scripts
3. Generating SEO titles + tags

The competitor channel "History Expose" provides the style reference (4 scripts analyzed). The user wants to run everything directly inside Claude Code as slash commands — no separate Python scripts or web apps.

## Approach

Create **3 custom Claude Code slash commands** stored as markdown files in `~/.claude/commands/`. These are invoked by typing `/history-ideas`, `/history-script`, `/history-seo` directly in any Claude Code session.

Each command embeds the full style guide extracted from the competitor's texts so Claude always generates in the correct voice.

---

## Style Guide (extracted from competitor scripts)

Derived from analysis of 4 "History Expose" scripts:

- **Structure**: Hook → Early life → Rise → Crisis/Scandal → Fall/Resolution → Moral conclusion
- **Opening hook**: Dramatic revelation or shocking fact in the first sentence
- **Tone**: Conversational + authoritative. Direct address ("As you might expect", "Talk about a bad omen")
- **Pacing**: Short punchy paragraphs, rhetorical questions, foreshadowing
- **Details**: Specific dates, names, numbers for credibility (e.g. "66-pound wedding dress")
- **Contrast**: Public persona vs private reality
- **Length**: ~1500–2500 words per script (approx. 10–15 min video)
- **Ending**: Tragic or ironic conclusion with brief moralistic reflection

---

## Files to Create

### 1. `~/.claude/commands/history-ideas.md`
**Command:** `/history-ideas`  
**Purpose:** Generates 10 topic ideas for new videos  
**Output:** List with title, hook sentence, and brief angle for each idea  
**Prompt includes:** niche context, style examples, instruction to avoid topics already covered

### 2. `~/.claude/commands/history-script.md`
**Command:** `/history-script`  
**Purpose:** Writes a full ~2000-word video script on a given topic  
**Input:** User provides the topic after the command (e.g. `/history-script Princess Diana`)  
**Output:** Full narration script ready to record, with section markers  
**Prompt includes:** Full style guide above, structure template, competitor tone examples

### 3. `~/.claude/commands/history-seo.md`
**Command:** `/history-seo`  
**Purpose:** Generates YouTube title variants + description + tags  
**Input:** User provides the topic or pastes the script  
**Output:** 5 title options (ranked), 300-char description, 15 tags  
**Prompt includes:** YouTube SEO best practices for history niche, CTR-optimized phrasing patterns from competitor

---

## File Locations

```
C:\Users\Aleksandr\.claude\commands\
├── history-ideas.md
├── history-script.md
└── history-seo.md
```

---

## Usage Flow

```
1. /history-ideas          → pick a topic
2. /history-script [topic] → get full script
3. /history-seo [topic]    → get title + tags
```

---

## Verification

After creating the files:
1. Start a new Claude Code session
2. Type `/history-ideas` — should generate 10 history topic ideas
3. Type `/history-script Queen Alexandra` — should produce a ~2000-word script in competitor style
4. Type `/history-seo Queen Alexandra` — should produce 5 titles + tags
5. Compare script tone against the 4 reference texts from the .docx file
