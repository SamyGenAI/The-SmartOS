# The Smart OS

The Smart OS is an LLM-maintained second brain. It follows Andrej Karpathy's LLM-wiki pattern: you drop raw sources in, an LLM compiles them into a linked wiki, and the work it produces lands in outputs. Your questions and explorations get filed back into the wiki, so the knowledge base compounds over time.

It is organised by operating system (Content, Design, GTM, Product, Finance, Life), one per area of work and life.

## Structure

- `raw/` — your sources. Immutable: the LLM reads them, never edits them.
  - `raw/me/` — your voice, proof, and offer. Fill these in first; every OS reads them.
  - `raw/{os}/` — sources per OS. `raw/ideas/` is the inbox, `raw/assets/` holds images.
- `wiki/` — the compiled wiki, owned by the LLM. Start at `wiki/smart-os.md`; `wiki/index.md` lists every page and `wiki/log.md` records every change.
- `outputs/` — the work. `outputs/agent/{os}/` is what agents produce, `outputs/human/{os}/` is your polished, final version.
- `AGENTS.md` — the schema: rules and workflows the LLM follows.
- `Home.md` — the human landing page.

## Use it with Obsidian

1. Clone this repo (or use it as a template) and open the folder as a vault in Obsidian.
2. Install the **Obsidian Git** community plugin and set it to commit, push, and pull every 10 minutes and pull on boot, so the vault and your agents stay in sync.
3. Open `Home.md`.

## Use it with an AI agent

Point Claude Code, Codex, or Cursor at the vault. They read `AGENTS.md` first, then follow its workflows:

- **Ingest** — add a source to `raw/`, ask the agent to ingest it.
- **Query** — ask a question; the agent reads the index, answers with citations, and offers to file the answer back.
- **Content** and **Design** — ask for a post, script, or visual; drafts go to `outputs/agent/`.
- **Explore** and **Lint** — run periodically to find new connections and keep the wiki healthy.

Agents pull before they work and commit and push right after (see Git Sync in `AGENTS.md`).

## Companion OS repos

- [Smart content system](https://github.com/SamyGenAI/Smart-content-system) — Content OS
- [Smart design system](https://github.com/SamyGenAI/Smart-design-system) — Design OS
- [Smart GTM system](https://github.com/SamyGenAI/Smart-GTM-system) — GTM OS

Part of The Smart Creator.
