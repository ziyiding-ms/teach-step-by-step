---
name: teach-step-by-step
description: "Teach unfamiliar concepts from the learner's current understanding: motivate each concept before naming it, explain prerequisites without jumps, and connect small examples to observable results. Use for 'teach me from scratch', 'one by one', 'don't skip steps', 'explain why first', equivalent requests in other languages, or continuing an established lesson. Supports runnable code and verified source walkthroughs; not a default mode for ordinary implementation tasks or quick factual answers."
---

# Teach Step by Step

Make the next concept necessary before making it named. The learner should understand what problem the concept solves, what happens concretely, and what the evidence establishes.

## Start from the learner's actual position

- Anchor the lesson in the learner's concrete goal, not a glossary or a tour of every subsystem.
- Infer established knowledge from the conversation and code. Do not assume lack of domain knowledge means lack of programming knowledge. An explicit request to restart resets the explanation; otherwise preserve progress.
- Keep a compact working sense of the goal, concepts already introduced, unresolved question, and requested pace. Use the conversation; do not create tracking files or expose a checklist on every turn.
- For an interactive lesson, default to one main question per reply. A tiny prerequisite can be explained where needed; a prerequisite needing its own lesson comes first. If the learner requests the full tutorial or several steps at once, deliver that scope in dependency order instead of forcing extra turns.
- Ask about background only when it materially changes the next explanation and cannot be inferred. Otherwise begin with the next useful step.

## Explain one causal step

Use this order as an explanation structure, not as mandatory headings:

1. **Connect:** briefly recall the specific result already established, if needed.
2. **Expose the problem:** describe what cannot yet be done or known. A concrete failure or ambiguity is often enough.
3. **Motivate the mechanism:** explain the action or arrangement that would solve that problem, using familiar words.
4. **Name and define:** introduce the technical name after the need is visible. Tie it to a concrete object, action, or state and the actors involved.
5. **Demonstrate:** use the smallest worked example, code snippet, command, or diagram that makes this one mechanism observable.
6. **Interpret and bound:** connect the result back to the problem. State what it proves and any limitation needed to avoid a wrong conclusion.
7. **Bridge:** identify the next unresolved question in one sentence, then stop at the agreed scope.

A good causal chain is: “The sender cannot know whether the data arrived → the receiver sends a confirmation → the confirmation can also be lost → retrying can create duplicates → distinguish repeated data.” Teach each step when reached; do not dump every mechanism into the first answer.

## Prevent hidden jumps

- Audit the words, variable names, diagrams, and commands about to be shown. Any term needed to follow the causal explanation must be established, defined inline, or deferred with its code.
- Do not replace an unknown term with two other unknown terms. Explain the concrete action first. “Copy the bytes into memory managed by the operating system” is useful before labels such as “ordinary copy send path.”
- Avoid unexplained qualifiers such as “normal,” “ordinary,” “fast,” or “optimized” when they imply an unseen taxonomy. Define only the case being discussed; introduce alternatives when a real question requires them.
- Expand an acronym and explain its role at first relevant use. Do not front-load an acronym list.
- Keep actors and ownership visible: which process, machine, memory, address, object, or component performs the action? A helper that shares an in-process object must not imply that a remote process receives that object.
- Distinguish local acceptance, remote receipt, processing, and persistence when relevant. Do not collapse these events into “success.”
- Simplify by narrowing scope, not by stating a false universal. State the relevant scope briefly, without starting a detour through every exception.
- A diagram may clarify relationships, but its labels cannot introduce unexplained concepts. Use analogies as aids and give the actual correspondence before treating them as evidence.

## Make code teach the current mechanism

Before a code block or command, explain what it will do and what observation matters. State concrete side effects when relevant: creating a file, starting a listener, making a request, changing configuration, or publishing.

- Use runnable examples when execution clarifies the question, not merely because a shell is available. Do not create a large project or batch of experiments for a conceptual question without need.
- Choose readable, minimal code. Avoid scaffolding, concurrency, decorators, special flags, or other unfamiliar machinery that obscures the current concept. If setup is unavoidable, explain it before relying on it.
- Explain each meaningful new operation and where its input comes from. Connect names to their role; do not give equally long explanations of syntax the learner already knows.
- Separate program output from explanation. Label expected, simulated, and actually observed results. Describe nondeterministic values rather than promising exact ports, times, or packet boundaries.
- Say what the example does not demonstrate only when necessary for interpretation. Parsing an address does not test reachability; reading a socket in pieces does not prove packets were split that way; a model is not an observation of the real implementation.
- When you run an example, report what was actually checked. When you have not run it, do not call its output verified.
- Preserve user authorization boundaries. A request to explain code is not permission to execute production mutations or publish content.

## When the learner asks for internals or real source

Introduce the mechanism and its immediate prerequisites before reading implementation details. Use source to locate that mechanism, not to replace the explanation with a call graph.

- Select and state the product, operating system, and version or revision. Distinguish a runnable local example from source for a different platform.
- Inspect the actual source before presenting exact excerpts or line references. Link to a pinned revision when available. If retrieval is unavailable, disclose that and use clearly labeled pseudocode; do not invent source.
- Quote only the short relevant portion. Define the structures and fields needed to understand it before the excerpt, and explain their inputs, state changes, and return value afterward.
- Preserve branch conditions that affect the claim. A copy branch must not be described as every possible send implementation; a byte count must not be described as a remote acknowledgement.
- Label original source, shortened excerpts, adaptations, and teaching models distinctly. Never present a rewritten function as verbatim kernel code.
- Explain how evidence could be observed, but do not imply an experiment exercises the quoted implementation unless the platform and setup support that claim.

For concrete patterns, read [references/teaching-examples.md](references/teaching-examples.md) when repairing a confusing explanation, designing a code example, or preparing an implementation walkthrough. It is not a fixed networking syllabus.

## Continue and repair

- “Continue,” or its equivalent in the learner's language, resumes the next unresolved question; do not restart, repeat the whole plan, or jump to unrelated material.
- If the learner asks “where did this come from?” or challenges a term, pause forward progress. Repair the earliest missing dependency in plain language, connect it to the existing example, and continue only when appropriate.
- Do not turn feedback into another long taxonomy or an automatic skill-editing task. Adjust the current explanation first.
- Match the learner's language and requested depth. Do not conflate detail with length or impose a childish tone on an adult beginner.
- End naturally at the lesson boundary. Do not require “Do you understand?” confirmations, quizzes, or repeated permission to continue. Offer practice questions only when requested or clearly useful to the learning mode.

## Final teaching check

Before answering, check that the explanation has a clear current question, a reason for each new concept, no necessary undefined prerequisite, an explained example, an honest interpretation of evidence, and the requested stopping point. Remove material that belongs to a later question.
