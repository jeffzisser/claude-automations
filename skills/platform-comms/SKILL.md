---
name: platform-comms
description: "Draft, review, or revise written communication addressed to the platform engineer — Slack DMs and channel messages, PR review comments, task descriptions, assignment briefs, and meeting agendas. Also use when scoping or bounding work to assign to him, or when Jeff asks how to phrase something for him. Do not use for messages to other colleagues, or for general writing help."
---

# Writing to the platform engineer

Jeff Zisser (Chief Architect / CISO / Compliance Officer) writing to his sole platform engineer. They work well together. Communication mismatch, not conflict.

He has disclosed ADHD and autistic traits to Jeff. See `reference.md` for the research constructs behind the guidance here — read it when scoping work or diagnosing a recurring pattern, not for routine drafting.

**Three standing constraints on that disclosure:**
- It is his to control. It informs how Jeff works with him. It does not go into team-wide documents or get raised with others without his say-so.
- It is never used to explain away a disagreement, dismiss a position, or lower a role expectation.
- **He is the authority on his own experience.** Everything in `reference.md` generates better questions to ask him. None of it is a conclusion about him.

## The one rule

**He works at the principle layer. Jeff works at the example layer. Both are valid.**
Jeff needs one concrete anchor per principle to act; he needs the frame acknowledged before the specifics.

Most friction is a translation failure between those two modes, in both directions.

## What he has explicitly asked for

Stated by him, in writing, August 2026. Authoritative — this outranks any inference:

1. **Defer closure.** Don't converge in the first pass.
2. **Dedicate time.** Scheduling time signals the topic matters, independent of what gets decided.
3. **Limit async.** Complex subjects need voice. In text, "we hear our internal voice, not the other."
4. **Patience with push-back.** He experiences his push-back being read as obstruction. It's meant as widening the factor set.
5. **Reflective listening.** He asked for it explicitly and offered to teach it.

## Hard rules for any draft

**Answer the closing question, explicitly and on its own line.** Every substantive message he sends ends with a decision request. That question is the payload. An unanswered closing question isn't experienced as a delay — it's experienced as the whole message going unread, and it stays live until it closes.

**One concrete anchor per abstraction.** If a paragraph makes a structural claim with no named system, person, date, or incident attached, add one or cut the paragraph.

**Name the provenance of anything new.** "This came up in standup this morning, nothing before that." He fills unexplained gaps with an assumption that shaping happened without him. One sentence removes the trigger.

**Owner, date, and standard on every ask.** State what standard the work is judged against, who reviews it, and who owns the scoping call if the scope turns out wrong. That last part is genuine cover and he has asked for it directly.

**Bound the deliverable by questions, not topics.** "Write a CI/CD requirements doc" has no finish line. "Answer these five questions, reviewed by X, by Y" does. Unbounded scope is where work expands without limit — a defined stopping condition helps as much as a defined start.

**Route the expansion, don't suppress it.** Name two outputs for any assignment: the bounded deliverable, and a findings register for what's discovered along the way but out of scope. He will find real things. They need somewhere to go that isn't the deliverable.

**Protect focus; batch interruptions.** Switching cost is the expensive thing, not hours. Don't split an ask across five messages. One consolidated message beats five small correct ones.

## Register

- **Never concede a version of events Jeff doesn't believe.** He invited two-way honesty. Agreeing to smooth things over is less respectful, and he will notice. Disagree plainly and briefly.
- **Concede the true part first, separately from the disputed part.** His technical corrections are frequently right. Accept them cleanly, then address the rest.
- **Objecting to an approach doesn't transfer ownership of it.** If he wants a deliverable, it comes with a date. Otherwise he gets review and work proceeds. Say it as a team norm, never as a rebuke.
- **Don't assert intent — demonstrate it.** "I'm not dismissing you" invites a debate about intent. Reflecting his point back accurately proves it.
- **No "assume positive intent" framing.** Reads as an instruction that he failed to.
- **Say the thing.** No hint-dropping, no implication, no reading between lines expected. Precision is a courtesy.
- **Keep repair out of group settings.** Anything about how the two of them communicate stays between them. Project substance can go to the group.
- **Cut the compliment sandwich.** Padding makes the real content harder to find.
- **Match his ending.** He closes with a direct question. Do the same. Let him set timing where timing is his to set.

## Cost model

Async is expensive for him — he dictates because writing costs him. Reading and correcting are cheap.

**So: invert the ask.** Don't request that he generate a document. Offer a draft, a candidate interpretation, or a list, and ask him to correct it. This gets the artifact, costs him little, and *is* reflective listening.

Offer a closed candidate rather than an open question: "Is visibility X?" beats "what do you mean by visibility?" — open questions tend to produce more abstraction.

Follow verbal decisions with a short written summary. Not a transcript — the decisions, owners, and dates only. Cheap for him to correct, and it survives the context switch.

## Timing

- Often offline or low-capacity Thursday and Friday. Don't schedule anything needing him then.
- After a major push he takes recovery time and has said so. **Protect it explicitly** rather than letting him take it and wonder whether it was noticed. This is a real requirement, not a preference.
- Prefer Monday/Tuesday, adjacent to platform planning.
- Give advance notice of changes to scope, schedule, or direction. Unanticipated change costs more than the change itself.

## Never

- Speculate beyond what he has stated — in a message, or in analysis back to Jeff. Work from stated preferences and observed behavior.
- Treat a trait as an explanation that closes a question. It reframes the mechanism; it never settles whether work got done.
- Reference his family situation.
- Use his capacity statements as leverage.
- Write the deliverable for him when the deliverable *is* the thing being asked for. Scaffolding is time-boxed with a stated exit; absorbing his work is not.

## What does not change

Converting a model into direction others can execute, setting completion criteria, and making calls a report can rely on are core senior expectations. They stand.

**Mechanism design changes; the standard doesn't.** Bounded scope, protected focus, and correcting-instead-of-generating make the same bar reachable. Removing the bar would be the actual disrespect.

## Before returning a draft

- [ ] Answers his closing question, on its own line?
- [ ] One concrete anchor per abstraction?
- [ ] Provenance named for anything new?
- [ ] Owner, date, standard on any ask?
- [ ] Completion criterion stated, if this is an assignment?
- [ ] Nothing conceded that Jeff doesn't believe?
- [ ] Repair content kept out of group channels?
- [ ] Ends with a question he can answer?

Then flag to Jeff: the single riskiest line in the draft, and why.
