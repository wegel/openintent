# The OpenIntent Manifesto

Status: Pre-publication foundation for OpenIntent 0.1  
Last updated: 2026-07-20

## Premise

Programmers have long used source code for two jobs. They tell computers how to
work, and they preserve human choices about what should exist. Large language
models make it possible to separate those jobs.

LLMs can carry most of the work required to create, test, repair, migrate, and
replace an implementation. Humans can focus on purpose, behavior, experience,
taste, tradeoffs, and the boundaries that a product must preserve.

OpenIntent should give humans a creative programming medium for that work. It
should not reduce intent to documentation that someone writes before the real
work starts.

An **intent program** is the human-owned, potentially multimodal source that
expresses what software should mean, do, and feel like. It can contain precise
rules, goals, examples, visual references, models, measurements, open questions,
and choices that the author deliberately leaves to an LLM.

To **compile** an intent program means to ask an LLM-backed process to create or
update working software from the whole program or from a change to it. A compile
can produce code, tests, previews, migrations, questions, and evidence. The
process need not produce the same implementation twice. The resulting software
must still satisfy the intent and survive checks in the real environment.

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

### 3. Let people program intent instead of writing paperwork

An author should be able to define a product's world, name its actors and
concepts, compose behavior, show examples, set boundaries, and run the result.
The work should feel constructive, not administrative.

OpenIntent should support reusable ideas, local changes, composition,
refactoring, experiments, and clear feedback. Its authoring tools may resemble a
text editor, notebook, whiteboard, simulator, design tool, or a combination of
them. Markdown can provide a portable representation without becoming the only
authoring experience.

### 4. Make each useful change runnable

An author should be able to compile a small intent change and experience its
effects without restating the whole product. The compiler should identify what
the change can affect, ask only questions that require human judgment, update
the relevant realizations, and return concrete results.

Authors should be able to use this loop in several ways:

- **Explore:** generate alternatives and learn what they imply.
- **Realize:** produce or update working software.
- **Verify:** challenge a realization against the intent program.

All three modes should help the author refine the program.

### 5. Give every project a blank slate

OpenIntent should provide a small set of powerful ideas rather than a fixed
catalog of everything software may contain. Each project must be free to invent
its own vocabulary, structures, representations, and ways of composing ideas.

A distributed protocol, mobile interface, game, compiler, medical device, and
art installation should not have to pretend that they share one natural shape.
OpenIntent should give their authors common ways to express and compile intent
without flattening their differences.

The method should supply enough grammar for humans and LLMs to work together. It
should not supply the imagination.

### 6. Express both commitment and freedom

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

### 7. Use the medium that carries each idea best

Text often communicates rules, reasons, and tradeoffs well. Images can
communicate visual relationships faster. Interactive prototypes reveal timing
and feel. Formal models can express protocols and state machines. Measurements
can define performance. Audio, video, diagrams, physical references, examples,
and code can also carry intent.

OpenIntent should compose these media instead of forcing every idea into prose.
Humans and LLMs should be able to understand, modify, compare, and preserve the
chosen sources.

A human may use code, pseudocode, or an exact algorithm as intent when that form
expresses a decision best. The method should preserve that decision without
forcing the human to maintain all implementation code around it.

### 8. Write intent early, then let reality teach it

People should write clear intent before implementation when that work helps
them think. They may revise it many times before they compile anything.

Working software will also reveal hidden needs, false assumptions, awkward
experiences, performance limits, and better ideas. Authors should update the
intent program as they implement and test. The compiler should bring discoveries
back to the author instead of silently treating generated code as product
authority.

The program leads the work, and experience improves the program.

### 9. Treat each implementation as a replaceable realization

One intent program may produce several valid implementations for different
platforms, operating conditions, experiments, or moments in a product's life.
Each realization can use a different language or architecture while preserving
the qualities that matter.

Authors should be able to discard and regenerate implementation code without
discarding the product's identity. When they truly care about an internal
choice, they can promote that choice into the intent program and explain why it
must survive.

### 10. Make machines carry the bookkeeping

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
4. Does the LLM carry the implementation and bookkeeping work that does not
   need human attention?
5. Can a project invent a form that we did not anticipate?
6. Can another realization replace the current one without losing what the
   author cared about?
7. Can humans and LLMs understand the result without depending on one vendor?

A feature that fails these questions should change or stay out, even when it
makes the project look more complete.

## Where OpenIntent starts

OpenIntent 0.1 starts with this manifesto. We will add language, workflows,
artifacts, examples, and tools only when they help people write or compile
intent under these tenets. We will test each addition through real creative work
instead of assuming that a complete-looking specification creates a useful
programming medium.
