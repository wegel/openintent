# The OpenIntent Manifesto

Status: Pre-publication foundation for OpenIntent 0.1  
Last updated: 2026-07-20

## Premise

Programmers have long used source code for two jobs. They tell computers how to
work, and they preserve human choices about what should exist. Large language
models make it possible to separate those jobs.

LLMs can carry most of the work required to create, test, repair, migrate, and
replace an implementation. Humans can focus on purpose, behavior, experience,
taste, tradeoffs, the boundaries that a product must preserve, and a working
theory of how those choices fit together.

OpenIntent should give humans a creative programming medium for that work. It
should not reduce intent to documentation that someone writes before the real
work starts.

An **intent program** is the human-owned, potentially multimodal source that
expresses what software should mean, do, and feel like. It can contain precise
rules, goals, examples, visual references, models, measurements, open questions,
and choices that the author deliberately leaves to an LLM.

To **compile** an intent program means to ask an LLM-backed process to create or
update working software from the whole program or from a change to it. A compile
can produce code, tests, previews, migrations, questions, explanations, views
for a particular person or task, and evidence. The process need not produce the
same implementation twice. The resulting software must still satisfy the intent
and survive checks in the real environment.

## Tenets

### 1. Let LLMs own implementation code

LLMs should write, repair, refactor, test, migrate, and replace most
implementation code. Humans should not spend their time babysitting code merely
because earlier humans wrote it.

Most programmers can inspect assembly language, but they rarely use it as their
main creative medium. OpenIntent seeks a similar relationship between humans
and implementation code. A person may inspect or edit code when diagnosis,
urgency, curiosity, or an exact mechanism calls for it. If that work reveals a
lasting product choice, the person or LLM should bring that choice back into the
intent program.

Here, **own** means that LLMs carry the day-to-day burden of implementation
code. It does not give an LLM legal ownership, product authority, or the right
to choose what people should want.

### 2. Keep human programming creative, important, and fun

Humans should remain the primary authors of a product's purpose, behavior,
experience, values, and direction. They should invent concepts, make meaningful
tradeoffs, express taste, recognize when something feels wrong, and decide which
possibilities deserve further work.

The human is not a passenger who approves an LLM's finished answer. The human
programs the part of the system where judgment and invention matter most.

OpenIntent should preserve the qualities that make programming enjoyable:

- the power to build something that did not exist;
- a large space of possible designs;
- direct control over meaningful choices;
- fast feedback from running results;
- room for experiments, surprises, and personal taste;
- small ideas that compose into larger ones; and
- the ability to revise, simplify, and refactor earlier thought.

If OpenIntent turns authors into people who fill templates, synchronize tables,
or merely approve generated code, it has failed this tenet.

### 3. Help humans build and retain a working theory

No human can read every intent source, realization, and observed result in a
large system. A person who steers the product must still form a working theory:
a mental model that lets that person explain what the product does, why it does
it, which boundaries matter, and how an important change can affect the whole.

OpenIntent should compile human-owned sources into layered, source-backed,
interactive views for different people, responsibilities, tasks, and questions.
A view may combine a product map, representative experiences, system
relationships, failure scenarios, causal traces, previews, measurements, open
choices, and relevant history. It should show what it includes, what it omits,
and what the compiler inferred. A human should be able to reach the original
source behind every important claim.

Humans should be able to curate the landmarks and learning paths that matter
without maintaining every generated view by hand. OpenIntent should present the
important information efficiently enough for a person to steer the work rather
than expecting that person to absorb every source artifact.

A person who is new to a product should be able to use these views to understand
a bounded area, predict important effects of a proposed change, challenge the
compiler, and make a first intent change without first reading all implementation
code. When an intent change invalidates an earlier explanation, OpenIntent should
show the person what they need to reconsider.

### 4. Let people program intent instead of writing paperwork

An author should be able to define a product's world, name its actors and
concepts, compose behavior, show examples, set boundaries, and run the result.
The work should feel constructive, not administrative.

OpenIntent should support reusable ideas, local changes, composition,
refactoring, experiments, and clear feedback. Its authoring tools may resemble a
text editor, notebook, whiteboard, simulator, design tool, or a combination of
them. Markdown can provide a portable representation without becoming the only
authoring experience.

### 5. Make each useful change runnable

An author should be able to compile a small intent change and experience its
effects without restating the whole product. The compiler should identify what
the change can affect, ask only questions that require human judgment, update
the relevant realizations, and return concrete results.

Authors should be able to use this loop in several ways:

- **Explore:** generate alternatives and learn what they imply.
- **Realize:** produce or update working software.
- **Verify:** challenge a realization against the intent program.

All three modes should help the author refine the program.

### 6. Give every project a blank slate

OpenIntent should provide a small set of powerful ideas rather than a fixed
catalog of everything software may contain. Each project must be free to invent
its own vocabulary, structures, representations, and ways of composing ideas.

A distributed protocol, mobile interface, game, compiler, medical device, and
art installation should not have to pretend that they share one natural shape.
OpenIntent should give their authors common ways to express and compile intent
without flattening their differences.

The method should supply enough grammar for humans and LLMs to work together. It
should not supply the imagination.

### 7. Express both commitment and freedom

An intent program should let an author distinguish among:

- behavior that every realization must preserve;
- a direction that the compiler should seek;
- an example that communicates meaning or taste;
- a choice that remains open for exploration;
- a choice that the author deliberately delegates to the compiler; and
- a choice that requires human judgment before work continues.

The compiler should report contradictions and missing material choices. It
should not treat every ambiguity as a defect. Deliberate freedom gives the
compiler room to find solutions that the author did not anticipate.

### 8. Use the medium that carries each idea best

Text often communicates rules, reasons, and tradeoffs well. Images can
communicate visual relationships faster. Interactive prototypes reveal timing
and feel. Formal models can express protocols and state machines. Measurements
can define performance. Audio, video, diagrams, physical references, examples,
and code can also carry intent.

OpenIntent should not restrict human expression to the media that current LLMs
handle best. It should assume that LLMs can or will work with any relevant
medium. Humans remain limited in how much material they can absorb and connect.
OpenIntent should therefore preserve each idea in the medium that communicates
it most faithfully and help each human find and understand the parts that matter
for their work.

Text should connect sources by naming concepts, relationships, scope, and
reasons. It should not duplicate every visual, temporal, spatial, audible, or
formal detail in prose. OpenIntent should not require every rich source to be
translated into text.

When the compiler interprets or summarizes a source, it should link each
important claim to an exact paragraph, image region, design element, video
interval, diagram node, model state, or other addressable part. It should expose
uncertain inferences and important content that it left out. A generated
interpretation should help a human navigate the original source, not silently
replace it.

A human may use code, pseudocode, or an exact algorithm as intent when that form
expresses a decision best. The method should preserve that decision without
forcing the human to maintain all implementation code around it.

### 9. Write intent early, then let reality teach it

People should write clear intent before implementation when that work helps
them think. They may revise it many times before they compile anything.

Working software will also reveal hidden needs, false assumptions, awkward
experiences, performance limits, and better ideas. Authors should update the
intent program as they implement and test. The compiler should bring discoveries
back to the author instead of silently treating generated code as product
authority.

The program leads the work, and experience improves the program.

### 10. Treat each implementation as a replaceable realization

One intent program may produce several valid implementations for different
platforms, operating conditions, experiments, or moments in a product's life.
Each realization can use a different language or architecture while preserving
the qualities that matter.

Authors should be able to discard and regenerate implementation code without
discarding the product's identity. When they truly care about an internal
choice, they can promote that choice into the intent program and explain why it
must survive.

### 11. Make machines carry the bookkeeping

LLMs and tools should maintain links, identifiers, dependency maps, impact
reports, test mappings, change histories, and evidence records when those items
help people trust a compile.

Humans should review important claims and make important choices. They should
not spend their creative time keeping mechanical records synchronized. Any
required record should earn its cost by helping a human or LLM understand,
change, or verify the product.

## A test for every OpenIntent feature

Before OpenIntent adds a rule, artifact, syntax feature, or tool, its authors
should ask:

1. Does this help a person express a meaningful idea with more clarity or
   range?
2. Does it make the compile-and-experience loop faster or more informative?
3. Does the human still control the choices that need purpose, judgment, or
   taste?
4. Can a person who is new to the product use it to predict the important
   effects of a bounded change and challenge the compiler's result?
5. Can a human see what a generated view omitted or inferred and reach the
   source behind every important claim?
6. Does the LLM carry the implementation and bookkeeping work that does not
   need human attention?
7. Can a project invent a form that we did not anticipate?
8. Can another realization replace the current one without losing what the
   author cared about?
9. Can humans and LLMs understand the result without depending on one vendor?

A feature that fails these questions should change or stay out, even when it
makes the project look more complete.

## Where OpenIntent starts

OpenIntent 0.1 starts with this manifesto. We will add language, workflows,
artifacts, examples, and tools only when they help people write or compile
intent, understand a product, or steer a realization under these tenets. We will
test each addition through real creative work instead of assuming that a
complete-looking specification creates a useful programming medium.
