# Using Hermes Desktop for Your Literature Review

This guide walks you through setting up Hermes Desktop for a schema-driven literature review: connecting it to a model, creating a project folder, shaping how the agent behaves, and building notes on papers that stay tied to your actual research question.

You'll use two apps together throughout: **Hermes Desktop** to chat with the agent, and **Obsidian** to view and edit the files that control it.

---

## 1. Connect Hermes to OpenRouter

Hermes needs a model to talk to. We'll use OpenRouter, a cloud provider — the schema-driven extraction work later in this guide needs more context space than a small local model comfortably handles.

1. Create an account and an API key at **openrouter.ai**.
2. In Hermes Desktop: **Settings → Providers → OpenRouter**, and paste in your key.
3. Pick a model from the list (your instructor may suggest one).
4. Start a new chat and confirm it responds normally, e.g.:
   ```
   What tools do you have available?
   ```

If a model you were using starts erroring out later, it's often because the specific model name was retired or renamed on OpenRouter — just pick a different one from the same list.

---

## 2. Create your project folder

Everything you do from here happens inside one folder.

1. In Finder (macOS) or File Explorer (Windows), create one empty folder — for example `Documents/lit-review`.
2. In Hermes Desktop, use the app's own folder/project selector (usually an **Add Folder** or **Open Folder** option in the sidebar) to open that folder directly. Start a new chat from within it once it's open.
3. Confirm it worked. In that chat, ask:
   ```
   What is your current working directory? List the files you can see there.
   ```
   It should show your `lit-review` folder (empty for now). If it shows somewhere else, re-open the folder before continuing — don't move on until this matches.

---

## 3. Edit `SOUL.md` with Obsidian

`SOUL.md` is Hermes's persona file — it's loaded first, every session, and shapes its tone and default behavior across *all* your projects, not just this one.

1. Open Obsidian and use **Open folder as vault** to open `~/.hermes/` (or `%LOCALAPPDATA%\hermes` on Windows) as its own vault. Call it something like "Hermes Home."
2. In **Settings → Files & Links**, turn on **Detect all file extensions** — Obsidian only shows `.md` files by default, and you'll want to see `SOUL.md` and eventually `config.yaml` too.
3. One thing to set up now: in the same settings pane, **exclude `.env`** from view (Settings → Files & Links → Excluded files). It holds your API key — no reason to have it open on screen.
4. Find and open `SOUL.md`. It may be empty or contain a short default.
5. Edit it directly in Obsidian. Keep it short — a few lines describing how you want Hermes to communicate with you. For example:
   ```markdown
   # Persona

   You're a careful, precise research assistant. When summarizing academic
   papers, prioritize accuracy over fluency — flag uncertainty rather than
   smoothing it over. Keep responses concise unless asked to elaborate.
   ```
6. Save. This takes effect the next time you start a chat.

---

## 4. Build your Memory and User files by talking to the agent

Alongside `SOUL.md`, Hermes keeps two more files in `~/.hermes/memories/`: `MEMORY.md` and `USER.md`. These hold things Hermes has learned about you and your work over time.

**Don't hand-write these** — Hermes has its own memory tool and is meant to fill them in itself, based on what you tell it in conversation. Just talk to it naturally:

```
I'm a researcher working on [your topic/field]. My current project looks
at [your research question or area]. I mostly read qualitative and mixed-
methods work. Please remember this going forward.
```

```
When I ask you to take notes on a paper, I care most about the methodology
and how findings map onto real-world policy — keep that in mind for future
sessions.
```

Hermes will decide what's worth saving and write it into `MEMORY.md` and `USER.md` on its own — you don't need to ask it to.

**To check what it saved:** open the "Hermes Home" Obsidian vault from Part 3 and look inside `memories/MEMORY.md` and `memories/USER.md`. Or just ask the agent directly:
```
What do you remember about me and my research?
```

These files have a size limit, so Hermes keeps them short and curated rather than a running transcript — don't expect (or want) a full log of every conversation in there.

---

## 5. Set up your project files: `AGENTS.md` and `SCHEMA.md`

Separately from your persona and memory (which follow you everywhere), each project folder has its own rules. Since Hermes is now pointed at your `lit-review` folder (Part 2), work inside that folder from here on.

1. Open your `lit-review` folder as a **second** Obsidian vault — call it "Lit Review Project." This is a different vault from "Hermes Home"; keep both open side by side.
2. Create two subfolders: `papers/` (where you'll put PDFs) and `notes/` (where generated notes will land).
3. Create two new files: `AGENTS.md` and `SCHEMA.md`.

**In `AGENTS.md`**, write a short instruction for how the agent should behave in this specific project:
```markdown
# Project Instructions

This project is for literature review note-taking. Before writing a note
on any paper, always read SCHEMA.md and follow its structure exactly.
Base every claim in a note only on the text of the paper itself —
never on outside knowledge of the paper, its authors, or its field.
```

**In `SCHEMA.md`**, define the note structure — see Part 6 for what actually goes here.

---

## 6. Connecting papers to your research question

This is the part that makes the notes useful rather than just generic summaries: every note needs to say not just what a paper found, but how it bears on **your** question.

### Write your research question into `SCHEMA.md` itself

Put your actual research question at the top of the file, in plain language, so it's always visible to the agent when it writes a note:

```markdown
# Note-Extraction Schema

**My research question:** [write your actual research question here —
be specific, not just a topic]

Every note on a paper must have exactly two sections:

## 1. The paper on its own terms
What does this paper claim, using what method, based on what evidence?
Describe it the way the authors would describe it — don't filter it
through my research question yet.

## 2. Relative to my research question
How does this paper actually bear on the research question above?
Does it support it, complicate it, contradict it, or address something
adjacent but not directly relevant? Be specific — point to the exact
claim or finding in section 1 that connects, and say how.
```

The two-section structure matters: section 1 keeps the paper's own claims separate from your interpretation, and section 2 forces an explicit, checkable link back to your question rather than a vague "this is relevant" gesture.

### Run it on a paper

1. Drop a PDF into `papers/`.
2. In a Hermes chat (make sure the folder you opened in Part 2 is still the active project), ask:
   ```
   Read papers/<filename>.pdf. Then read SCHEMA.md and write a note in
   notes/<a-short-name>.md following it exactly. Base every claim in
   section 1 only on the extracted text — nothing from outside knowledge.
   ```
3. Open the result in your "Lit Review Project" Obsidian vault.

### Check it, don't just trust it

Pick a paper you already know well for this first run. Read the generated note against the actual PDF:
- Does section 1 accurately represent what the paper says, or has something been oversimplified or invented?
- Does section 2's connection to your research question actually hold up, or is it a stretch?

If you're comparing notes across several papers later, keep the comparison constrained to the notes themselves:
```
Using only notes/paper-a.md and notes/paper-b.md, compare how each one
answers section 2 relative to my research question. Don't bring in
anything outside these two files.
```
That keeps the comparison traceable back to notes you've already checked, rather than the agent quietly drawing on its own general knowledge of the papers.

---

## Troubleshooting

| Problem | What's likely happening | What to do |
|---|---|---|
| Hermes can't see `AGENTS.md`, `SCHEMA.md`, or files in `papers/` | It isn't actually working in your project folder | Ask "what is your current working directory?" — if it's wrong, re-open the folder in Hermes Desktop |
| Replies are empty or erroring | Provider or model isn't set correctly | Recheck Settings → Providers → OpenRouter and re-pick a model |
| `config.yaml` won't open inside Obsidian | Obsidian only edits `.md` files natively | Normal — it'll hand off to your system's text editor instead |
| You see `.env` in the Hermes Home vault | It's just not excluded yet | Settings → Files & Links → Excluded files, add `.env` |
| A note's section 2 feels vague or generic | The model isn't being forced to point at a specific claim | Ask it to redo section 2, specifically requiring it to quote or point to the exact part of section 1 that connects |