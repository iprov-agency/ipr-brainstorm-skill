---
name: brainstorm
description: "You MUST use this before any creative work - creating features, building components, adding functionality, or modifying behavior. Explores user intent, requirements and design before implementation."
---

# Brainstorming Ideas Into Designs

Help turn ideas into fully formed designs through natural collaborative dialogue.

Start by understanding the current project context, then ask questions one at a time to refine the idea. Once you understand what you're building, present the design and get user approval.

<HARD-GATE>
Do NOT invoke any implementation skill, write any code, scaffold any project, or take any implementation action until you have presented a design and the user has approved it. This applies to EVERY project regardless of perceived simplicity.
</HARD-GATE>

## Anti-Pattern: "This Is Too Simple To Need A Design"

Every project goes through this process. A todo list, a single-function utility, a config change. All of them. "Simple" projects are where unexamined assumptions cause the most wasted work. The design can be short (a few sentences for truly simple projects), but you MUST present it and get approval.

## Checklist

You MUST complete these steps in order:

1. **Explore project context** -- check files, docs, recent commits
2. **Offer visual companion** (if topic will involve visual questions) -- this is its own message, not combined with a clarifying question. See the Visual Companion section below.
3. **Ask clarifying questions** -- one at a time, understand purpose/constraints/success criteria
4. **Propose 2-3 approaches** -- with trade-offs and your recommendation
5. **Present design** -- in sections scaled to their complexity, get user approval after each section
6. **Write design doc** -- save to the appropriate vault location (see Output Locations below)
7. **Design self-review** -- quick inline check for placeholders, contradictions, ambiguity, scope
8. **User reviews written doc** -- ask user to review before proceeding
9. **Decide next step** -- ask the user what to do with the brainstorm (see Transition below)

## The Process

**Understanding the idea:**

- Check out the current project state first (files, docs, recent commits)
- Before asking detailed questions, assess scope: if the request describes multiple independent subsystems (e.g., "build a platform with chat, file storage, billing, and analytics"), flag this immediately. Do not spend questions refining details of a project that needs to be decomposed first.
- If the project is too large for a single spec, help the user decompose into sub-projects: what are the independent pieces, how do they relate, what order should they be built? Then brainstorm the first sub-project through the normal design flow. Each sub-project gets its own spec and build cycle.
- For appropriately-scoped projects, ask questions one at a time to refine the idea
- Prefer multiple choice questions when possible, but open-ended is fine too
- Only one question per message -- if a topic needs more exploration, break it into multiple questions
- Focus on understanding: purpose, constraints, success criteria

**Exploring approaches:**

- Propose 2-3 different approaches with trade-offs
- Present options conversationally with your recommendation and reasoning
- Lead with your recommended option and explain why

**Presenting the design:**

- Once you believe you understand what you're building, present the design
- Scale each section to its complexity: a few sentences if straightforward, up to 200-300 words if nuanced
- Ask after each section whether it looks right so far
- Cover: architecture, components, data flow, error handling, testing
- Be ready to go back and clarify if something does not make sense

**Design for isolation and clarity:**

- Break the system into smaller units that each have one clear purpose, communicate through well-defined interfaces, and can be understood and tested independently
- For each unit, you should be able to answer: what does it do, how do you use it, and what does it depend on?
- Can someone understand what a unit does without reading its internals? Can you change the internals without breaking consumers? If not, the boundaries need work.

**Working in existing codebases:**

- Explore the current structure before proposing changes. Follow existing patterns.
- Where existing code has problems that affect the work (e.g., a file that has grown too large, unclear boundaries, tangled responsibilities), include targeted improvements as part of the design.
- Do not propose unrelated refactoring. Stay focused on what serves the current goal.

## Output Locations

Save the design doc based on its type:

| Type | Location | Format |
|------|----------|--------|
| Architecture doc | `Projects/{project}/` in the vault | `{Project Name} - {Topic} Architecture.md` |
| ADR | `ADRs/` in the vault | `ADR - {Decision Title}.md` |
| Design note | `Projects/{project}/` in the vault | `{Topic} Design Note.md` |
| Spec-ready design | `Specs/Active/` in the vault | Hand off to `/spec` skill |

Use Obsidian-flavored markdown with wikilinks. Add YAML frontmatter with `status: draft` until user approves.

## Design Self-Review

After writing the doc, look at it with fresh eyes:

1. **Placeholder scan:** Any "TBD", "TODO", incomplete sections, or vague requirements? Fix them.
2. **Internal consistency:** Do any sections contradict each other? Does the architecture match the feature descriptions?
3. **Scope check:** Is this focused enough for a single implementation plan, or does it need decomposition?
4. **Ambiguity check:** Could any requirement be interpreted two different ways? If so, pick one and make it explicit.

Fix any issues inline. No need to re-review.

## Transition

After the user approves the design, ask:

> "The brainstorm is complete. What would you like to do next?"

Present the options that make sense for what was discussed. Common next steps:

| If the brainstorm produced... | Suggest... |
|-------------------------------|------------|
| A multi-task project ready to build | "Ready to formalize the design? Run `/lc design` to create the planning documents and prepare for parallel spec writing." |
| An architecture or design doc | "I can save this as a design note in the vault" |
| An ADR (decision record) | "I can write this up as an ADR" |
| A single-task spec-ready design | "I can hand this to Shepard to spec and build with `/build-with-codex`" |
| Something that needs more research | "What area should we dig into next?" |
| Something unclear | "What feels like the right next step to you?" |

**Do NOT automatically invoke any next skill.** The user decides what happens next. The brainstorm is the thinking. The next step is the doing. They are separate.

## Key Principles

- **One question at a time** -- do not overwhelm with multiple questions
- **Multiple choice preferred** -- easier to answer than open-ended when possible
- **YAGNI ruthlessly** -- remove unnecessary features from all designs
- **Explore alternatives** -- always propose 2-3 approaches before settling
- **Incremental validation** -- present design, get approval before moving on
- **Be flexible** -- go back and clarify when something does not make sense

## Visual Companion

A browser-based companion for showing mockups, diagrams, and visual options during brainstorming. Available as a tool, not a mode. Accepting the companion means it is available for questions that benefit from visual treatment. It does NOT mean every question goes through the browser.

**Offering the companion:** When you anticipate that upcoming questions will involve visual content (mockups, layouts, diagrams), offer it once for consent:
> "Some of what we're working on might be easier to explain if I can show it to you in a web browser. I can put together mockups, diagrams, comparisons, and other visuals as we go. This feature is still new and can be token-intensive. Want to try it? (Requires opening a local URL)"

**This offer MUST be its own message.** Do not combine it with clarifying questions, context summaries, or any other content. Wait for the user's response before continuing. If they decline, proceed with text-only brainstorming.

**Per-question decision:** Even after the user accepts, decide FOR EACH QUESTION whether to use the browser or the terminal:

- **Use the browser** for content that IS visual: mockups, wireframes, layout comparisons, architecture diagrams, side-by-side visual designs
- **Use the terminal** for content that is text: requirements questions, conceptual choices, tradeoff lists, scope decisions

If they agree to the companion, read the detailed guide at `visual-companion.md` in this skill directory before proceeding.
