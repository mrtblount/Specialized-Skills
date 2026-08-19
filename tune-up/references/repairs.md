# Repairs — patterns for the fix

## Principles

- **Original preserved untouched.** Before the first edit, keep a complete
  copy. With a filesystem: a sibling folder like `<name>-original/`. On
  chat-only platforms, the owner's currently-installed copy *is* the
  untouched original until they replace it — say so; and if anything was cut,
  also hand back a downloadable `<name>-original.zip` alongside the fixed
  one, so the cut material lives with the owner, not in a session that
  expires.
- **Smallest change that ends the problem.** A tune-up, not a rebuild.
- **Every edit traces to a diagnosis.** Make no improvements the owner did
  not ask about. Every finding gets either a fix or an explicit note saying
  why it was left alone.
- **Their favorite parts survive verbatim.** If they said they like the
  content, the content stays; you're fixing wiring, packaging, and fit around
  it.
- **Write the way you'd prescribe.** Conditions and defaults, not quotas and
  all-caps. The fixed copy should pass its own exam.

## Trigger surgery

- Rebuild the description around the owner's verbatim phrases. It should read
  like the owner talking about what they want, because that's what Claude
  matches against.
- If the target has several procedures, give the entry file a plain routing
  table — "when the owner says…, do…" — with one line per real request
  pattern the owner uses. Include the near-misses: what each entry does *not*
  cover, when a neighboring word means a different procedure.
- **Separate reporting from changing.** Requests like *audit / review / check /
  look over* produce findings first and end by offering the fixes. Requests
  like *fix / polish / clean up / final pass* change things. When a request
  could be either, the fixed thing defaults to findings first and ends by
  offering the changes — people who ask for a look want to see before
  anything moves.
- Defang greedy umbrellas: scope broad "do everything" procedures to the
  words that genuinely mean everything, and route specific requests to their
  specific procedures.

## Platform substitution

Never leave a dead tool name in the fixed copy. Substitute per platform:

| Original expects | Where it's absent, substitute |
|---|---|
| Interactive form / questionnaire tool | Ask directly in chat, a few questions at a time (or the structured-question tool if this environment shows one) |
| "Spawn subagents" / parallel review agents | Sequential passes covering the same ground, one after another |
| "Delegate to a verifier" | Verify directly with what exists: render, open, re-read, walk the output |
| Starter components / copy-a-template helpers | Inline the needed behavior into the file, or remove the feature and say so |
| Host protocols (window messaging, edit-mode toggles, preview toolbars) | Remove; replace with the nearest native feature or nothing |
| Filesystem operations on chat-only platforms | Produce the content in the conversation or as a downloadable file |
| `${PLACEHOLDER}` variables never filled in | Resolve to the real name here, or remove the sentence |

When the owner uses multiple platforms, fix for where they actually run
*this* thing; note anything that won't carry to the other platform.

## De-quota pass

Rewrite older-model coercion into current-model conditions. The shape:

- "Ask at least 4 questions" → "Ask what the brief actually leaves open; a
  question whose answer wouldn't change the work is noise."
- "CRITICAL: YOU MUST run all checks before finishing" → "Run the checks that
  apply; when unsure whether one applies, run it."
- "Only report important issues" → "Report everything with a severity note;
  filter when presenting."
- "Generate diverse variations" → specify what makes each variation distinct,
  per variation, before producing it.

Keep the intent, drop the shouting. If a quota encoded something real (a
floor the owner genuinely wants), state the floor as the owner's requirement,
not as pressure on the model.

## Right-sizing

- The entry file carries what routes and how to behave; detail moves to
  reference files loaded when a procedure runs.
- Cut what this owner will never use. It lives on in the preserved original.
- If the thing is one giant prompt rather than a skill, converting it is the
  single highest-value repair wherever the owner's platform supports
  installed skills: small entry file with the routing and voice, procedures
  split into reference files. Where it doesn't (pasted project instructions
  in a chat product), tighten the prompt in place instead.

## Packaging

The entry file is named `SKILL.md` — on every Claude platform, that exact
filename is what gets loaded; any other name and the thing silently never
activates. Its metadata block, minimally:

```yaml
---
name: the-name
description: >-
  What it does and when to use it, written in the owner's own phrases —
  this text is how Claude decides the thing applies.
---
```

`name`: lowercase-with-hyphens, matching the folder name. Keep the
description well under 1,000 characters — the owner's verbatim phrases are
the priority; trim generic filler first if space runs short.

- **claude.ai:** build the zip yourself in the session — zip the folder
  itself, so the zip contains one folder with `SKILL.md` directly inside it,
  not loose files at the zip's top level — and hand it to the owner as a
  downloadable file, never by pasting whole files into the conversation.
  Their steps are only: download it, then wherever skills/capabilities are
  managed in Settings, remove the old version and upload the new. Don't
  leave two versions installed side by side.
- **Claude Code:** the folder goes in `~/.claude/skills/` (available in
  every project) or `<project>/.claude/skills/` (one project). Same
  replace-don't-duplicate rule.
- **Desktop app:** usually gets skills the claude.ai way (uploaded in
  Settings); some desktop modes also read `~/.claude/skills/`. Check where
  the owner's other skills actually load from before choosing.
- Two installed things with overlapping descriptions will fight for the same
  requests. If the owner already has something claiming similar territory,
  either sharpen both descriptions until they don't overlap, or retire one.

## Prove-it protocol

Build the phrase set:

1. The owner's verbatim sentences from Listen
2. Close paraphrases of each
3. Neighbors that should route to a *different* procedure
4. Neighbors that should do nothing at all

Walk every phrase against the fixed copy and show the owner one plain table:
*you say → it does*. They confirm or you adjust. A phrase that routes wrong
is a wiring bug — fix the description or routing table, never tell the owner
to phrase it differently.

## Handing back

- What changed, in their terms, in a handful of bullets
- Where the untouched original lives
- Exact install-or-replace steps for their platform
- What to watch on the first real run
- The standing invitation: "if it ever does something you didn't expect, come
  back and tell me what you typed and what it did instead."
