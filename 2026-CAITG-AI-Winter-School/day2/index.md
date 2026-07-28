# AI-Augmented Literature Review — Day 2 — CAITG AI Winter School

**What you'll do today:** three activities, each showing a different way an AI tool can help you read and work with academic papers — from the simplest possible case to a fully structured one.

1. **Naive, single-document, fully local** — LM Studio's document chat
2. **Agentic, multi-document, cloud** — Antigravity working across a folder of papers
3. **Schema-driven, structured, traceable** — Hermes + a custom skill

Each activity builds on the one before it — don't skip the first one just because it's the simplest of the three. The contrast between them is the point.

---

## Synthetic papers

I have created some synthetic papers using an LLM. You can download them [here](https://github.com/fraba/presentation/tree/master/2026-CAITG-AI-Winter-School/day2/synth-papers).


## Part 1 — Intro lecture

Start here: **[Intro slides](https://fraba.github.io/presentation/2026-CAITG-AI-Winter-School/day2/wagner-lecture-slides.html)**

This breaks "doing a literature review" into discrete tasks and walks through what an AI tool can take off your hands at each one, and what you should keep for yourself — including two ideas you'll use for the rest of today: distillation (why a short note beats a full paper) and the Zettelkasten method.

---

## Part 2 — Activity 1: LM Studio (fully local, one small paper)

The point of this activity: the model reads the whole paper because it fits entirely inside its context window. Nothing clever is happening, and nothing leaves your laptop — worth noticing before anything more agentic gets layered on top.

### Pick a model
**Discover** tab → search for a small instruct model (Qwen 2.5/3 Instruct or Llama 3.x Instruct, 7–9B is plenty) → pick **Q4_K_M** → **Download**.

### Test it
**Chat** tab → select the model → let it load → send a test message to confirm a normal reply.

### Pick a small paper
A short paper (roughly under 15–20 pages, or a research note/short communication) — it needs to fit comfortably inside the model's context window so LM Studio reads the whole thing rather than falling back to retrieval-based chunking. Pick one you already know well — you'll want that later in this activity.

### Check the context window
Gear icon next to the model picker → **Context Length**. A small paper (a few thousand words) needs roughly 6,000–12,000 tokens depending on the model's tokenizer — raise it if needed and reload the model.

### Attach the paper and ask questions
1. Start a new chat.
2. Click the **paperclip icon** and attach the PDF.
3. Ask direct questions: *"What's the main research question?" "What method did they use?" "What's the sample size?"*

### Notice

- Since you already know the paper, check the answers against it — flag anything wrong, vague, or invented.
- This is **conversation-scoped, not folder-scoped**: start a new chat and the document is gone. No persistent project, no memory of it, nothing written to disk. Activities 2 and 3 each solve that differently.
- If the model fell back to retrieval (a longer paper, or a smaller context window), it's answering from *retrieved fragments*, not the full text — that changes how much you should trust an answer that references something outside those fragments.

---

## Part 3 — Activity 2: Antigravity (cloud, a folder of papers)

Antigravity is Google's agentic IDE — genuinely folder/project-based, unlike LM Studio's per-chat attachment. It runs on Google's own cloud models rather than a local one, so unlike Activity 1, what you send it doesn't stay on your laptop.

### Create a Project
1. Click the **folder-with-a-"+"** icon in the left sidebar.
2. **New Project**.
3. **Add Folder** → point it at a folder of papers.
4. **Create**.

More on Projects, available models, agent modes, and slash commands.

**[Tasks](https://fraba.github.io/presentation/2026-CAITG-AI-Winter-School/day2/antigravity-task.html)**

---

## Part 4 — Activity 3: Hermes Desktop (schema-driven notes)

The third and most deliberate activity: a structured, traceable extraction process using a custom skill and your own note-extraction schema, connected to a cloud model via OpenRouter.

**[Full walkthrough](https://fraba.github.io/presentation/2026-CAITG-AI-Winter-School/day2/)**

That guide covers connecting to a model, creating your project folder, shaping the agent's behavior, and building notes that stay tied to your actual research question.
