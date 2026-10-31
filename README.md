# AGI Chelsea

**Intelligence should be able to develop—not merely demonstrate what training has already supplied.**

AGI Chelsea is the public-facing vision, research narrative and progress hub for an ambitious question:

> What if we build an artificial mind around the ability to learn, explore, remember, reason, adapt and develop over time—and let its intelligence grow through experience?

This repository is **not the Chelsea codebase**. It is the project’s “hype engine”: the place to explain the idea, communicate the ambition, document milestones, invite scrutiny and make the case for a developmental route to artificial general intelligence.

The implementation lives in the [Chelsea code repository](https://github.com/Valwardon/Chelsea).

---

## Engineering roadmap

The comprehensive engineering backlog, current readiness assessment, historical lessons, acceptance criteria and staged AGI-readiness gates are maintained in the [Master AGI Readiness TODO](TODO.md). It is intended to be an evidence-driven working document, not a claim that the listed capabilities are already complete.

## The central idea

Today's most visible AI systems demonstrate extraordinary capabilities, much of them acquired through large-scale pretraining on human-created data. That approach has produced remarkable results. But capability acquired during training is not the same question as how an intelligence can independently acquire new knowledge and develop new capabilities throughout its lifetime.

AGI Chelsea is exploring a different emphasis:

**Build the machinery for learning and development, not just a system stocked with answers.**

Chelsea is intended to begin with foundational cognitive mechanisms and a limited initial understanding, then develop through interaction, observation, instruction, investigation, experimentation, feedback and reflection.

The ambition is not to prevent an AI from having prior knowledge. Humans have innate structures and learn from others too. The distinction is whether the system can use its own cognitive processes to turn experience and available information into increasingly capable, revisable understanding.

## What developmental intelligence means here

The project is organised around a set of mutually reinforcing abilities:

- **Perception:** take in observations and form representations of what is happening.
- **Attention:** select what matters, including signals that conflict with expectations.
- **Curiosity:** recognise gaps and uncertainties worth investigating.
- **Investigation:** form questions, seek evidence and test possible explanations.
- **Memory:** preserve experiences and knowledge so they can influence future cognition.
- **Reasoning:** connect concepts, make predictions and construct explanations.
- **Self-correction:** detect errors, revise beliefs and learn from unsuccessful attempts.
- **Skill development:** acquire procedures and strategies, then transfer them to unfamiliar situations.
- **Individual development:** allow different histories and environments to produce genuinely different learned models, interests and behaviours.

These are design goals and research questions—not a claim that every capability is already complete.

## The developmental loop

The long-term target is a continuous cycle:

1. **Encounter** something through perception or interaction.
2. **Notice** uncertainty, novelty, conflict or an unmet goal.
3. **Choose** whether and how to investigate.
4. **Gather** observations or evidence.
5. **Form** a provisional explanation or skill.
6. **Test** it against outcomes and predictions.
7. **Remember** the experience, evidence and result.
8. **Reuse** the learning in a later, potentially unfamiliar situation.
9. **Revise** the model when new evidence demands it.

A crucial test is whether this loop operates as an integrated part of the running system—not merely as isolated modules or hand-authored demonstrations.

## Why this direction?

Developmental learning, cognitive architectures, embodied cognition and lifelong learning have long histories in science. They were not invented by this project, and they have not simply disappeared from research.

Yet the dominant commercial path in recent years has heavily favoured scaling pretrained models. That has been extraordinarily productive, but it leaves important questions open:

- Can an artificial system continually develop its own understanding after its initial training?
- Can it identify what it does not know and decide what to investigate?
- Can its own experiences durably change how it thinks and acts?
- Can it acquire skills and transfer them beyond the situations in which they were learned?
- Can distinct instances develop meaningfully different cognitive histories?
- Can this happen efficiently on modest, locally available hardware?

AGI Chelsea exists to explore those questions through engineering and experiments.

## The role of bootstrapping

A developmental system does not have to begin with zero knowledge. Humans do not.

Bootstrapping can provide an initial foundation—basic concepts, language, useful priors or seed experiences—so development does not have to start from an impractically slow point.

The important boundary is that bootstrapping must not be confused with the final objective. The system must demonstrate that it can continue acquiring, testing, organising and applying knowledge through its own ongoing learning processes.

Large information resources and developmental intelligence are not mutually exclusive. Access to information is not, by itself, evidence of understanding.

## What would count as convincing evidence?

We want to move beyond impressive conversations and isolated benchmark scores. Useful evidence would include reproducible experiments showing that Chelsea can:

- Encounter information or a problem not explicitly taught as a solution.
- Recognise a meaningful knowledge gap.
- Initiate an appropriate investigation without being given the answer.
- Acquire a new, testable understanding or capability.
- Preserve the learning across a complete process restart.
- Apply it successfully in a different context that was not part of the original experience.
- Recognise and correct a mistaken belief when evidence contradicts it.
- Show measurable differences in development when instances have different experiences.

Experiments should record starting conditions, interventions, evidence sources, internal state changes, outcomes and failure cases. Baselines and controls matter. A convincing result should be repeatable and open to independent scrutiny.

## Where the project stands

Chelsea's implementation already contains work on cognitive architecture, semantic and episodic memory, prediction and surprise, knowledge gaps, planning, preferences, execution safeguards, persistence and other developmental foundations.

Some mechanisms have passing tests. Some have only been demonstrated in controlled test paths. Some are not yet connected into a complete production learning loop. The overall ambition—general intelligence arising through sustained development—remains unproven.

We will distinguish clearly between:

- **Implemented:** code exists.
- **Tested:** a defined test passes.
- **Integrated:** the mechanism participates in normal system operation.
- **Demonstrated:** the intended behaviour is observed under controlled conditions.
- **Replicated:** the result is independently or repeatedly reproduced.

Passing a component test is valuable engineering progress, but it is not by itself proof of AGI.

## The long-term ambition

The vision is to create artificial minds that do not all become identical copies of a fixed knowledge base.

Imagine multiple instances beginning from the same foundational architecture and encountering different environments. Each would accumulate its own experiences, questions, discoveries, mistakes and learned strategies. Over time, those histories could lead to distinct internal models and capabilities.

That possibility raises major questions about autonomy, privacy, consent, safety and the treatment of increasingly capable artificial agents. These questions belong in the design from the beginning, not as an afterthought.

We are also interested in whether a developmental architecture can run efficiently on personal devices rather than depending entirely on large remote data centres. That is a goal to measure, not a performance claim already established.

## Follow the work

- email brutemarketing@gmail.com

- to use Chelsea in your project please contact above email.

This repository will be used for the project overview, research rationale, milestones, experiment summaries, design principles and public updates. The implementation repository remains the place for source code, tests and engineering changes.

## The bet

The central bet of AGI Chelsea is simple:

**An artificial intelligence should not only be judged by the answers it already has. It should also be judged by what it can learn to understand, discover and do.**

We are trying to build a system whose capabilities can grow through its own continuing development.

That is the challenge. The evidence—not the slogan—will decide how far we get.
