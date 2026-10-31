# Knowledge Base Schema

## What This Is
The second brain for the owner's **Smart OS**: an AI agent swarm that runs every area of work and life through a set of operating systems. Maintained by an LLM. The owner curates sources and asks questions. The LLM writes and maintains the entire wiki.

An orchestrator agent routes the work while Claude Code, Codex or Cursor do it. [[Home]] is the human landing page for the vault.

## Operating Systems
Every source, wiki page, and output belongs to one OS (or to `me`, which is shared by all of them).

| OS         | Slug    | Scope                                                                                       | Status        |
| ---------- | ------- | ------------------------------------------------------------------------------------------- | ------------- |
| Content OS | content | Copywriting, content calendar, research and social listening, design briefs, past posts and analytics | [planned]     |
| Design OS  | design  | All visual assets: infographics, carousels, thumbnails, motion graphics, slide decks, landing pages | [planned]     |
| GTM OS     | gtm     | Lead generation, outreach, sales                                                            | [planned]     |
| Product OS | product | [What you sell]                                                                             | [planned]     |
| Finance OS | finance | Revenue, expenses, invoices                                                                 | [planned]     |
| Life OS    | life    | Health, habits, personal goals                                                              | [planned]     |

Statuses: planned, building, active. Replace the placeholders as each OS comes online.

To add a new OS: add a row here, create raw/{slug}/, outputs/human/{slug}/ and outputs/agent/{slug}/, create a hub page wiki/{slug}-os.md, link it from wiki/smart-os.md and wiki/index.md, and log it.

## Architecture
- raw/ contains source documents. These are immutable. Never modify files in raw/.
  - raw/me/ holds the owner's voice, proof, and offer. The owner writes these and every OS reads them.
  - raw/{os}/ holds the sources for each OS (research notes, brain dumps, transcripts, articles, meeting notes, exports).
  - raw/ideas/ is the inbox for raw ideas from any OS.
  - raw/assets/ holds images, screenshots, and diagrams referenced by sources.
- wiki/ contains the compiled wiki. The LLM owns this entirely. It creates pages, updates them when new sources arrive, maintains cross-references, and keeps everything consistent.
  - wiki/smart-os.md is the top hub. It links to one hub page per OS: wiki/{os}-os.md.
  - All other pages live flat in wiki/ and link up to their OS hub. A page that spans several OSes links to all of them.
- outputs/ is split by author, then by OS. There are no drafts/ or published/ folders.
  - outputs/human/{os}/ holds what the owner writes. A file here is the latest polished version of that piece. Never write here unless the owner asks; never overwrite a file here — propose changes or write a new version in outputs/agent/.
  - outputs/agent/{os}/ holds what the agents produce (drafts, briefs, variations, reports). Agents write here freely. The owner takes what they like and polishes it into outputs/human/.
  - Content OS outputs are split per platform, then per stage, on both sides: outputs/{human,agent}/content/{Platform}/{Research,Text or Script,Design brief}/{title}/. Stage folders: Research, Text (written platforms) or Script (video platforms), Design brief. Design OS outputs live in outputs/{human,agent}/design/.
  - Each piece gets its own folder named after its title, with its images in an Assets/ subfolder.
  - When an output is valuable enough to inform future queries, promote it into wiki/ as a new page. Your explorations and queries should always add up in the knowledge base.

## Git Sync
The vault is always synced with GitHub. Obsidian Git commits and pushes every 10 minutes and pulls every 10 minutes and on boot. Agents commit to the same repo, so to avoid conflicts:
1. Before you read or change the vault, run `git pull --rebase`.
2. When you finish a change, commit it and push right away. Don't leave vault changes uncommitted at the end of a task.
3. If the push is rejected, run `git pull --rebase` and push again. If there is a conflict, keep both sides' content where you can, and tell the owner what you resolved.
4. `.obsidian/` is tracked on purpose, except `.obsidian/workspace.json`. If an `.obsidian/` file conflicts, keep the newest local version.

## Wiki Conventions
- Every wiki page gets its own .md file in wiki/.
- Every page starts with YAML frontmatter (title, created, last_updated, source_count, status, os) and a one-paragraph summary. `os` lists the OS slugs the page belongs to.
- Use [[page-name]] links between wiki pages. Cross-reference aggressively, including across OSes. The connections between pages are as valuable as the pages themselves.
- Every factual claim cites its source: [Source: filename.md]
- When new information contradicts existing content, flag it explicitly. Don't silently overwrite. Note both claims, cite both sources, flag which is more recent.

## Index and Log
- wiki/index.md catalogs every page with a one-line description, grouped by OS. The LLM updates this on every ingest. When answering queries, read the index first to find relevant pages, then drill into them.
- wiki/log.md is an append-only chronological record. Format: `## [YYYY-MM-DD] action | os | Description` where action is ingest, query, lint, or update. Parseable with grep.

## Ingest Workflow
When I add a new source to raw/:
1. Read the full source
2. Discuss key takeaways with me
3. Create a summary page in wiki/
4. Update the OS hub page(s) and wiki/index.md
5. Update ALL relevant existing pages across the wiki (a single source should touch multiple pages, often in more than one OS)
6. Add backlinks from existing pages to new content
7. Flag any contradictions with existing wiki content
8. Append entry to wiki/log.md

Process one source at a time. Batch ingesting produces worse results — you lose the ability to guide what matters.

## Query Workflow
When I ask a question:
1. Read wiki/index.md to find relevant pages
2. Read those pages, following [[links]] for connected context
3. Synthesize an answer with citations to wiki pages
4. Render answers as the format that fits best: a wiki page, a comparison table, a briefing, a slide deck (Marp), or a visualization
5. If the answer is substantial, offer to file it back into wiki/ so it compounds
6. If the question reveals a gap, flag it and suggest what sources would fill it

## Content Workflow
When I ask for a post, newsletter, thread, or script, or for help with a draft I wrote:
1. Read raw/me/voice.md, raw/me/proof.md, and raw/me/offer.md
2. Read wiki/content-os.md and the pages relevant to the topic
3. Read my past pieces in outputs/human/content/{Platform}/ as examples of the final, polished version.
4. For a new piece, write research into outputs/agent/content/{Platform}/Research/{title}/, the copy into {Platform}/Text/{title}/ (Script/ for video), and briefs into {Platform}/Design brief/{title}/. For my own piece in outputs/human/, edit only what I asked for.
5. If the piece needs a visual, write a design brief (infographic, carousel, thumbnail, or motion graphic) in {Platform}/Design brief/{title}/ and hand it to Design OS.
6. Use only facts from raw/me/proof.md or cited wiki pages. Never invent numbers, results, or testimonials.
7. When I say a piece is published, log it. Nothing moves: the published version is the one in outputs/human/.

## Design Workflow
When I ask for a visual asset:
1. Read wiki/design-os.md and the design brief, if Content OS wrote one
2. Use the design system repo (see Related Systems) and the references in raw/design/{format}/
3. Write the asset into outputs/agent/design/{title}/
4. When I keep an asset, I move it into outputs/human/ next to the piece it belongs to, or into outputs/human/design/

## Explore Workflow
Periodically, find unexplored connections:
1. Read wiki/index.md and scan all pages for topics that appear in multiple contexts but aren't directly linked, especially across OSes
2. Identify the most interesting unexplored connections
3. For each, explain what insight it might reveal and what source would confirm it
4. Offer to create new pages or add cross-references for confirmed connections

## Lint Workflow
Periodically check for:
- Contradictions between pages
- Stale claims that newer sources have superseded
- Orphan pages with no inbound [[links]], or not linked from their OS hub
- Important concepts mentioned but never explained in their own page
- Missing cross-references
- Claims without source citations
Output: wiki/lint-report-[date].md

## Focus Areas
- Content OS: [your topics]
- Design OS: [the formats you need]
- GTM OS: [your ICP, channels, offer]
- Product OS, Finance OS, Life OS: to be defined

## Expected Source Types
Research notes, brain dumps, filming notes, video transcripts, articles, newsletter issues, published posts, screenshots, lead lists and GTM notes, and later product, finance, and life notes.

## Related Systems
Companion OS repos (The Smart Creator boilerplates):
- [Smart content system](https://github.com/SamyGenAI/Smart-content-system) — Content OS: platform writers, content waterfall, design briefs
- [Smart design system](https://github.com/SamyGenAI/Smart-design-system) — Design OS: graphics, carousels, thumbnails, slides
- [Smart GTM system](https://github.com/SamyGenAI/Smart-GTM-system) — GTM OS: find, score, enrich, export
- [Your tools] — add your own spreadsheets, calendars, and databases here, with the OS they serve
