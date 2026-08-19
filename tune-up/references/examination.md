# The exam — six ways an instruction set fights its owner

Run all six parts. Find everything and keep your own complete list with a
severity note per finding; present the owner a short, grouped version in plain
language. Reporting only "important" findings during the exam silently lowers
coverage — filter at presentation, not during discovery.

Severity, in the owner's terms:

1. **Breaks a session** — stalls, dead ends, calls to tools that don't exist
2. **Wrong result** — runs fine but does something other than what they meant
3. **Friction** — works, but costs extra turns, noise, or babysitting
4. **Cosmetic** — worth noting, wouldn't change their day

---

## 1. Intent routing — their words vs. its wiring

The most common failure, and the reason most people say a skill is "broken"
when every file in it is technically fine.

Check:

- **Vocabulary match.** Take every phrase the owner collected in Listen and
  trace where each would land. List the words the thing's description and
  procedures respond to; list the words the owner actually uses. The gaps and
  collisions are the diagnosis.
- **Greedy umbrellas.** One broad procedure (a "final pass," a "do everything"
  mode) positioned so it swallows specific requests. If the specific thing the
  owner asks for is a subset of the umbrella, the umbrella tends to fire.
- **Report vs. change.** For every procedure, ask: does it *tell* the owner
  things, *change* things, or both? Then ask which one the owner expects when
  they use their words. "Audit," "review," "check," "look at" mean *tell me* —
  a procedure that edits in response to those words is a wrong-result failure
  even if its edits are good. When the owner's phrasing genuinely bundles both
  ("review and fix this"), the change half still comes after the findings are
  shown.
- **Missing modes.** Things the owner asks for that no procedure covers at
  all. The model will improvise; sometimes well, sometimes not — either way
  the owner gets inconsistency.

## 2. Platform fit — built for somewhere else

Skills written inside one product often name tools and features that only
exist there.

Check:

- List every named tool, protocol, component, or feature the target calls for.
- Check each against what is actually available where the owner runs it. The
  tools visible in the current session are ground truth for *this* platform;
  for another platform, ask the owner or reason from what that product can do.
- Classify what happens when each missing piece is hit:
  - **Silent skip** — the feature just never happens (owner never knows)
  - **Stall** — the procedure says to wait for a response that will never
    come (owner sees Claude stop cold)
  - **Improvisation** — the model invents a substitute (sometimes fine,
    sometimes bizarre, always inconsistent)

Examples of the class: interactive form/questionnaire tools, "spawn a
subagent" or "launch agents in parallel," copy-a-starter-component helpers,
host window-messaging protocols, unresolved `${PLACEHOLDER}` variables left
from a build step, references to a preview pane or toolbar that isn't there.

## 3. Packaging — is it even installed as what they think it is?

- Is it structured as a skill *on their platform* — the entry file, the
  folder shape, the metadata block at the top — or is it a document that got
  pasted somewhere and only sometimes gets read? Owners often can't tell;
  "not sure if it converted properly" is a packaging question.
- The description at the top is the router: it is how Claude decides the
  thing applies. A vague or missing description means it never activates, or
  activates for the wrong requests. It should contain the owner's own
  phrases.
- Size of the entry file. Everything in it is loaded every time the thing
  activates. A monolith taxes every session; detail belongs in reference
  files loaded when needed.
- Files the entry file points to that don't exist in the folder, and files in
  the folder nothing points to.

## 4. Model fit — written for an older Claude

Current models tend to follow instructions literally and to under-reach for
optional capabilities — calibration guidance, not permanent law; recheck
against the model actually running. Instruction styles that worked by
shouting at older models now misfire.

Detect:

- **Quotas** — "ask at least 4 questions," "generate exactly 3 options."
  Tend to be treated as literal contracts; the model pads to hit the number.
  Replace with the condition the quota was approximating.
- **Coercion** — "CRITICAL: YOU MUST ALWAYS." Causes over-triggering and
  anxious compliance in the wrong situations. State when to act instead.
- **Suppression** — "only report important issues." Followed literally: real
  findings silently vanish. Prefer find-everything, filter-at-presentation.
- **Randomness assumptions** — procedures that expect variety to emerge on
  its own ("generate diverse options"). Variety should be specified
  per-option, not hoped for.
- **Stale model facts** — claims about model names, behaviors, or settings
  that no longer exist. Flag; don't propagate.

## 5. Scope fit — this copy belongs to this owner

- **Dead weight.** Procedures, chapters, or modes this owner will never
  invoke. Cutting them is allowed and kind: less to mis-route, less loaded
  per session, less to read when something goes wrong — and the preserved
  original keeps whatever was cut. Infer likely-unused parts from what the
  owner already told you (someone who only builds landing pages probably
  never touches the slide-deck procedure), then confirm cuts as one grouped,
  optional offer — "you likely never use these; want them gone or left
  alone?" — never a per-item quiz. When in doubt, leave it in.
- **Missing coverage.** Steps their described workflow needs that the target
  doesn't have. Name the gap; add only with the owner's yes — adding scope is
  their call.
- **Wrong defaults.** Assumptions baked in that don't match their reality:
  output format, tech stack, audience, tone, platform. Each one is a small
  recurring tax they pay every use.

## 6. Coherence — does the machinery actually run?

- Contradictions between files, or between the description and the
  procedures.
- Chains to other skills, tools, or files that aren't installed alongside it.
- Orchestration that can't terminate or fans out absurdly — a review
  procedure that launches reviewers whose own instructions launch more
  reviewers; nothing tells the children to run flat.
- Instructions to stop and wait for something that will never respond on this
  platform.
- Steps that depend on an earlier step's output that no step produces.
