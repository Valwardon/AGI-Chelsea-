# AGI Chelsea — Master Readiness TODO

**Last assessed:** 2026-10-31  
**Implementation repository:** [Valwardon/Chelsea](https://github.com/Valwardon/Chelsea) (private)  
**Vision and progress repository:** [Valwardon/AGI-Chelsea-](https://github.com/Valwardon/AGI-Chelsea-) (public)  
**Assessment basis:** live GitHub main-branch history through `96c356b9e1e055f967caccc54f89e3c4c6ace062`, selected source files, the repository's recorded decision ledger, and the previous engineering review. This is a source/history assessment, not a fresh full workspace build, device run, or independent reproduction of every recorded test.

> **Mission:** Build an artificial mind that can acquire, organise, test, retain, transfer and revise knowledge through its own continuing development. The target is not a large collection of impressive modules. The target is a reliable, measurable, integrated developmental learning system.

This file is the master engineering and research backlog. It deliberately separates what exists from what is proven in the running system. Checkboxes should only be closed with evidence linked in a decision-ledger entry, test report, reproducible experiment or reviewed implementation.

---

## 0. Executive assessment

### Current judgment

Chelsea is a serious experimental cognitive architecture with real work in semantic representation, activation, prediction, surprise, epistemic status, curiosity/gap handling, episodic persistence, planning, procedure representation, language bootstrap, visual identity, action safeguards and metacognitive monitoring.

**Chelsea is not yet demonstrated to be generally intelligent or AGI-ready.** The biggest blocker is not the absence of another clever subsystem. It is the absence of a fully evidenced, normal-production, end-to-end developmental loop that repeatedly converts self-acquired experience into durable improvements in future behaviour across unfamiliar contexts.

There is no universally accepted AGI checklist, and source code cannot yield a defensible AGI percentage. This TODO therefore uses observable readiness gates instead of a made-up percentage.

### Latest confirmed progress

The live code repository has advanced beyond the previous assessment:

- **n=165 — reusable plan retrieval:** recorded 5/5 PASS. Existing plans can be retrieved for a goal before generating a new plan.
- **n=166 — procedure representation:** recorded 7/7 PASS. Adds `NodeType::Procedure`, `Grounding::Procedure`, procedure formation, class-indexed retrieval and instantiation. The recorded formation rule uses three consecutive matching plan structures.
- **n=167 — decline rationale:** recorded 3/3 integration and 4/4 unit PASS. The scheduler records when it deliberately does not investigate a gap, why, what it chose instead and what would change the decision.
- **n=168 — live intent path clarification:** comment/documentation change only. It clarifies that the bootstrap can be invoked by J1, the live input path, when a source is provisioned. It does not itself wire a source into the production lifecycle.

Relevant commits:
- [n=165 plan retrieval](https://github.com/Valwardon/Chelsea/commit/be1594864daec56d5e5f107b4b0a737bbf9885e5)
- [n=166 procedure formation and retrieval](https://github.com/Valwardon/Chelsea/commit/42188844854408b16514e7a606fa085f7bfe24f7)
- [n=167 declined-investigation rationale](https://github.com/Valwardon/Chelsea/commit/cab35c74908a20486f182740b6d8ce041211adce)
- [n=168 ledger/head](https://github.com/Valwardon/Chelsea/commit/96c356b9e1e055f967caccc54f89e3c4c6ace062)

Important qualification: the pass counts above are the repository's recorded results. They have not all been independently rerun as part of this assessment.

### Readiness at a glance

| Area | Assessment | What is still needed |
|---|---|---|
| Cognitive substrate | Substantial implementation | Verify interactions and long-run stability |
| Online prediction and surprise | Strong constrained mechanisms | Broader causal/world-model learning and transfer |
| Episodic persistence | Journal is lifecycle-connected | Prove useful retrieval changes future cognition after restart |
| Semantic knowledge | Representation and provenance mechanisms exist | Reliable evidence acquisition, consolidation, contradiction handling and migration |
| Curiosity and gap handling | Detection, budgets, failure/decline records exist | Autonomous reconsideration, real evidence sources and closed-loop investigation |
| Language bootstrap | Live input path exists conditionally | Production source provisioning and grounded acquisition beyond curated lookup |
| Planning | Planner, plan retrieval and procedure representation exist | Learn, execute, evaluate and transfer procedures in a live governed loop |
| Action | Partial constrained execution and timeout safeguards | Production executor wiring, real adapters and independent outcome verification |
| Vision | Image bridge and persistent identity mechanisms exist | Continuous perception integrated with cognition and action |
| Metacognition | Selected live monitoring/self-healing paths exist | Broad, held-out, rollback-safe self-improvement |
| Individual development | Architectural direction exists | Multiple controlled instances with separate durable histories |
| AGI evidence | Not established | Longitudinal, adversarial, held-out and replicated developmental benchmark |

---

## 1. The single most important objective: close the developmental loop

**Priority: P0 — blocking**

The target loop must work in an ordinary running Chelsea instance, not only through test helpers or manually attached components:

1. Receive an observation from a real input channel.
2. Identify known, unknown, ambiguous, novel or contradictory aspects.
3. Register a typed knowledge gap or learning opportunity.
4. Decide whether investigating it is useful, safe and affordable.
5. Select a source, ask a question, observe, search or run a safe experiment.
6. Acquire evidence with source, time, context and reliability metadata.
7. Form a provisional representation, explanation or procedure.
8. Predict what should happen if the new model is useful.
9. Test it against new evidence or a controlled intervention.
10. Accept, qualify, revise or reject the candidate.
11. Store the episode and resulting knowledge durably.
12. Restart the process and retrieve the relevant learning.
13. Apply it to a different, not-identical context.
14. Compare predicted and actual outcomes.
15. Update confidence and revise when it fails.

### Required end-to-end demonstration

Build one small, instrumented environment first. Do not wait for full robotics or unrestricted internet research.

Example: a simple simulated tabletop with unfamiliar objects and controllable physical rules.

- Chelsea sees or receives observations of objects and interactions.
- A new object or relation is not in her initial knowledge.
- She detects the uncertainty and chooses an information-gathering action.
- She observes evidence, forms a provisional rule and records why she believes it.
- She predicts the result of a new interaction.
- The simulator returns the actual result.
- Chelsea compares prediction with outcome and revises if necessary.
- The process is killed and restarted.
- Chelsea retrieves the learned rule and uses it on a different object or arrangement.
- The evaluator withholds the answer and checks that the result came from the recorded experience rather than a hidden lookup.

**Acceptance gate:** one complete trace with event IDs, source provenance, internal state changes, model version, prediction, action, outcome, restart/retrieval evidence and successful transfer. Repeat with multiple random seeds and at least one misleading or contradictory observation.

### Tasks

- [ ] Draw the real production data-flow diagram from input to memory and back to future action.
- [ ] Mark every component as production-connected, optional/user-provisioned, test-only, externally driven or disconnected.
- [ ] Add an integration test that starts Chelsea through the same lifecycle used by a normal deployment.
- [ ] Run the full loop without manually calling internal learning functions or injecting the desired answer.
- [ ] Add trace IDs linking observation → gap → investigation → evidence → hypothesis → test → memory → retrieval → transfer.
- [ ] Make every stage emit an observable event and a reason for its decision.
- [ ] Add a fault-injection test at every boundary: unavailable source, timeout, invalid evidence, process crash, disk failure, contradictory result and tool failure.
- [ ] Run the demonstration after a clean process restart, not only within one process.
- [ ] Repeat on unseen task variants and publish failures as well as successes.

---

## 2. Production integration audit

**Priority: P0 — blocking**

A callable setter or a passing integration test is not enough. The normal lifecycle must actually attach and exercise the component.

### 2.1 Intent consultation and language bootstrap

The current code has `CognitiveDaemon::set_intent_source` and J1 live-input bootstrap logic. The source is user-provisioned; without it the path fails closed. The n=168 change is documentation, not production wiring.

- [ ] Identify the supported production source implementation and its configuration contract.
- [ ] Attach it in the real lifecycle when configured; do not silently substitute a canned test source.
- [ ] Expose source health, coverage, latency, provenance and failure state.
- [ ] Keep the no-source behaviour honest: admit the gap, do not fabricate an answer.
- [ ] Add a startup integration test proving the deployed lifecycle actually provisions the source.
- [ ] Add a live-input test where an unfamiliar word or intent is encountered, evidence is consulted, uncertainty is preserved and the result is later tested.
- [ ] Clearly distinguish curated corpus retrieval, user teaching, web retrieval, direct perception and independent inference.

**Acceptance:** production startup diagnostics prove the source is attached; a live interaction produces a trace showing what source was consulted and what Chelsea inferred herself.

### 2.2 Governed action executor

The planner has executor-wiring mechanisms and tests, but the earlier source review did not find the production lifecycle attaching the concrete executor through the available hook. Recheck the current full source before changing it.

- [ ] Trace the full lifecycle path from goal creation to planner to executor to actuator to outcome observation.
- [ ] Attach the governed executor in production or document why a particular deployment intentionally has no actuator.
- [ ] Ensure every action-capable path goes through permissions, preconditions, budgets, timeout handling, audit logging and reconciliation.
- [ ] Prevent direct action paths from bypassing the governed executor.
- [ ] Add a production wiring test that fails if the executor is absent when action execution is enabled.
- [ ] Verify action outcomes from the environment; never treat a successful command return as proof that the intended world change happened.

**Acceptance:** a normal lifecycle performs a permitted sandbox action, records its provenance and independently observes whether the intended effect occurred.

### 2.3 Curiosity, harvester and gap detector

- [ ] Inventory every GapDetector, harvester, curiosity hook and resolver call site.
- [ ] Identify which are actually invoked by the scheduler in production.
- [ ] Wire one bounded, real evidence source into the investigation path.
- [ ] Preserve a no-network/offline mode with honest limitations.
- [ ] Make source selection a decision based on gap type, uncertainty, expected information gain, cost, safety and available permissions.
- [ ] Prove that a detected gap can cause an investigation without a person manually invoking the resolver.

**Acceptance:** an unfamiliar but safe question triggers an investigation, obtains source-grounded evidence, updates a provisional model and is later tested.

### 2.4 Vision and sensor integration

- [ ] Trace `ingest_image` and `VisionFeed` from the hardware bridge to the cognitive scheduler.
- [ ] Decide which sensor streams are continuous and which are explicitly user-supplied.
- [ ] Connect continuous perception to event segmentation, identity tracking, memory, prediction and goal selection.
- [ ] Keep vision compute bounded and asynchronous; do not block the cognitive tick on expensive image processing.
- [ ] Add tests for missing frames, duplicate frames, occlusion, reappearance, changing appearance and false identity matches.
- [ ] Make every visual claim traceable to the source frame and confidence.

**Acceptance:** in a controlled live stream, Chelsea tracks an object through occlusion, remembers it, predicts its movement and corrects a mistaken identity when evidence changes.

---

## 3. Curiosity must become investigation, not just gap detection

**Priority: P0 — blocking**

A system that can say “I do not know” is more honest, but not yet curious. Curiosity requires choosing and performing an appropriate information-seeking action.

### 3.1 Fix the known reconsideration blind spot

The n=167 decline-rationale record contains an especially important finding. For gaps throttled because the system asks only one question per prompt, the recorded reconsider condition is:

> “none in current design: throttled gaps are never re-considered for asking”

The new log makes this blind spot visible; it does not solve it.

- [ ] Replace permanent one-time suppression with a reconsideration policy.
- [ ] Store next-eligible tick/time, reason for deferral, priority, expiry and reconsider condition.
- [ ] Reconsider deferred gaps when the user supplies relevant context, a source becomes available, the priority changes or the cooldown expires.
- [ ] Ensure a gap can be asked again without nagging the user every turn.
- [ ] Add fairness/aging so lower-ranked gaps are not starved forever.
- [ ] Test that a gap deferred behind another question is eventually reconsidered or explicitly closed with a reason.
- [ ] Distinguish deferred, failed, unavailable, unsafe, low-value and resolved states.

**Acceptance:** create two gaps in one prompt; ask about one; later provide a condition that makes the other eligible; verify the second gap is reconsidered exactly once under the policy and is not permanently lost.

### 3.2 Investigation selection

- [ ] Define an investigation policy with explicit terms: expected information gain, uncertainty, relevance to goals, estimated cost, risk, source reliability and time sensitivity.
- [ ] Keep the policy interpretable and log why an investigation was selected or declined.
- [ ] Use a bounded curiosity budget across nested investigations.
- [ ] Prevent loops, repeated near-identical queries and cycles in dependency graphs.
- [ ] Add backoff and reconsideration for temporary failures.
- [ ] Make negative results useful: “source checked; no evidence found” must not be silently converted to “false.”
- [ ] Add stopping criteria: sufficient evidence, diminishing returns, budget exhaustion, safety boundary or human approval needed.
- [ ] Separate curiosity from compulsive activity: no infinite browsing, repeated prompting or unbounded background tasks.

### 3.3 Evidence acquisition and epistemic status

- [ ] Define a common evidence record: content, source, timestamp, retrieval method, context, confidence, scope, licence/permission where relevant and integrity hash.
- [ ] Keep source testimony separate from Chelsea's interpretation.
- [ ] Distinguish direct observation, user teaching, external testimony, corpus retrieval, inference and experiment.
- [ ] Require corroboration for high-impact claims.
- [ ] Represent conflicting evidence explicitly; do not average incompatible claims into false certainty.
- [ ] Record what evidence would change a belief.
- [ ] Add source reliability tracking without treating popularity or similarity as truth.
- [ ] Prevent a consulted answer from being promoted to independently discovered knowledge without additional tests.
- [ ] Ensure every answer can be traced to its supporting records.

### 3.4 Investigation examples

**Definition gap:** Chelsea encounters an unfamiliar tool name. She checks an allowed reference source, records the source and a tentative definition, then tests the definition by predicting what the tool does in a sandbox.

**Causal gap:** Chelsea observes that a lamp turns off after a switch is pressed. She does not immediately assert causation. In a safe simulator she varies the switch while holding other variables stable, then checks whether the effect repeats.

**Contradiction:** two sources disagree about an object property. Chelsea preserves both claims with provenance, marks the property uncertain and seeks a discriminating observation.

**Unavailable source:** Chelsea cannot reach a source. She records the gap as deferred/unavailable, not solved, and retries only when a meaningful trigger occurs.

---

## 4. Memory: from durable records to useful autobiographical learning

**Priority: P0 — blocking**

Chelsea has a significant foundation: the append-only episodic journal and restart replay are lifecycle-connected, and prior tests recorded durable event recovery. The n=157 proof demonstrated a test path in which a negative-valence episode survived a kill-9, was replayed and changed planner scoring. That is meaningful evidence, but it is not yet the same as a broad production demonstration of learned knowledge changing future cognition.

### 4.1 Separate memory types

- [ ] Define and document distinct stores/representations for:
  - episodic/autobiographical memory: what happened to this instance;
  - semantic memory: what is believed about the world;
  - procedural memory: how to perform a skill;
  - working memory: what is active now;
  - source/evidence memory: why a claim is held;
  - self/identity history: how this instance's own state and capabilities changed.
- [ ] Define promotion rules between memory types.
- [ ] Preserve provenance when episodes are consolidated into semantic knowledge.
- [ ] Preserve exceptions and counterexamples rather than storing only the simplified rule.
- [ ] Prevent authored creations, imagined scenarios and hypothetical simulations from being silently stored as factual events.

### 4.2 Durable storage and recovery

- [ ] Add schema versions and explicit migrations for journal, semantic graph, procedure and preference state.
- [ ] Add compaction and retention policies for append-only journals.
- [ ] Bound graph growth and memory retrieval cost.
- [ ] Test disk-full, permission errors, partial writes, corrupted headers, invalid checkpoints, interrupted rename and corrupted records.
- [ ] Define recovery behaviour: continue safely, enter read-only/degraded mode or request repair.
- [ ] Add checksums/integrity validation and backups.
- [ ] Ensure atomicity and fsync semantics are appropriate on every target filesystem.
- [ ] Add observability for replay count, dropped/corrupt records, checkpoint age, journal size and compaction.
- [ ] Test upgrade/downgrade compatibility and backup restoration.

### 4.3 Retrieval and memory use

- [ ] Build a deterministic experiment: experience → persist → kill process → restart → retrieve → changed prediction or action.
- [ ] Make retrieval relevance measurable; test false retrievals and missed retrievals.
- [ ] Use context, recency, causal relevance, source quality and confidence—not lexical overlap alone.
- [ ] Test delayed recall, interference, repeated events, contradictory events and memory overload.
- [ ] Test whether Chelsea can explain which past episode supports a current decision.
- [ ] Test whether she can recognise that a once-useful memory is now stale.
- [ ] Add principled forgetting/archiving without destroying audit evidence.
- [ ] Ensure deleting or correcting a belief does not erase the historical record that it was once held.

### 4.4 Required memory benchmark

- [ ] Teach or let Chelsea discover a new arbitrary rule in a fresh environment.
- [ ] Record the actual experience and evidence.
- [ ] Restart the process and machine if feasible.
- [ ] Ask a structurally different question requiring that rule.
- [ ] Include a distractor that resembles the original experience but has a different causal structure.
- [ ] Change the rule and test whether Chelsea updates rather than clinging to the old one.
- [ ] Repeat across seeds and independent instances.

**Acceptance:** the learned rule is not present in the initial graph, is acquired from recorded evidence, survives restart, is retrieved with correct provenance, transfers to a novel arrangement and is revised when the environment changes.

---

## 5. Preferences, motivation and individual development

**Priority: P0/P1**

The code contains drives and valence mechanisms, and prior recorded tests showed within-run preference ranking and persistence of ranking across restart when valence was directly updated. That is not yet proof that stable preferences emerge from ordinary lived experience or that reported likes/dislikes correspond to an enduring internal state.

- [ ] Build a controlled preference experiment with a fixed set of equally available tasks.
- [ ] Record random seed, initial graph, drives, valence, activation, task ranking, chosen actions, time spent, effort, persistence, avoidance and voluntary return.
- [ ] Run multiple clean boots with identical initial conditions.
- [ ] Repeat with controlled changes in experience, feedback and task order.
- [ ] Separate stochastic variation, hard-coded bias, developer-supplied values and experience-derived preference.
- [ ] Test whether preferences predict later unprompted choices.
- [ ] Test whether preferences change after meaningful new evidence.
- [ ] Test persistence across restart without directly setting the desired valence in the experiment.
- [ ] Add controls for novelty bias, recency bias, reward hacking and preference loops.
- [ ] Avoid describing valence or preference scores as subjective feelings or consciousness without independent evidence.

### Individual instances

- [ ] Define a shared versioned cognitive substrate and per-instance state boundary.
- [ ] Give each instance a separate identity key, autobiographical journal, learned graph, procedural memory and preference history.
- [ ] Record whether each item was self-discovered, taught by a person, transferred from another instance or supplied by a developer.
- [ ] Define explicit, permissioned knowledge-sharing protocols.
- [ ] Do not merge one instance's private experience into another's history without provenance and consent rules.
- [ ] Run multiple copies from identical initial state in different controlled environments.
- [ ] Measure whether their learned models, interests, skills and predictions diverge in explainable ways.
- [ ] Swap environments between instances to distinguish environment effects from innate/random differences.
- [ ] Test whether teaching one instance a discovery helps another without falsely claiming the second discovered it independently.

**Acceptance:** multiple instances begin from a common baseline, experience controlled differences, and develop persistent, explainable differences that are attributable to their histories.

---

## 6. World model, causal reasoning and representation growth

**Priority: P1**

Current online relational prediction and surprise detection are useful foundations, but they cover constrained problem families. A general developmental system needs coherent representations of entities, properties, events, time, space, actions, agents, causes and uncertainty.

- [ ] Define a unified event model with entity IDs, time intervals, participants, locations, properties, actions and provenance.
- [ ] Track entity identity across time, modalities and changing appearances.
- [ ] Represent object permanence, occlusion, reappearance and identity uncertainty.
- [ ] Distinguish correlation, temporal sequence, causal influence and coincidence.
- [ ] Add safe intervention/experiment records.
- [ ] Add counterfactual alternatives: what would likely have happened if the action had not occurred?
- [ ] Model preconditions, action effects, side effects and delayed outcomes.
- [ ] Represent uncertainty and context-specific validity on learned rules.
- [ ] Detect distribution shift and structural change.
- [ ] Keep old models with retirement/supersession history instead of silently overwriting them.
- [ ] Learn new abstractions from lower-level experience instead of requiring every useful concept to be predeclared.
- [ ] Test compositionality: combine familiar concepts into genuinely new arrangements.
- [ ] Test cross-domain transfer without assuming that a superficial analogy is valid.

### Example benchmark

Chelsea learns from simple interactions that a particular object slides on one surface but not another. Later she encounters a new object, a changed surface and a different orientation. She must identify which parts of the earlier model may transfer, which are uncertain, what to test and how to update the model after observation.

**Acceptance:** she predicts before the experiment, explains the evidence behind the prediction, updates the right parts of the model and transfers only the validated structure.

---

## 7. Language learning grounded in experience

**Priority: P1**

The bootstrap and parser provide a symbolic route to language acquisition. Curated corpus similarity is useful as a source of evidence, but it is not equivalent to independently grounding language in the world.

- [ ] Connect word learning to shared attention, observed referents, actions and consequences.
- [ ] Learn new words from multiple varied examples, not one definition.
- [ ] Track which meanings are provisional, context-dependent, ambiguous or contested.
- [ ] Distinguish word form, referent, concept, speaker intent and pragmatic function.
- [ ] Learn compositional meaning from familiar parts in unfamiliar sentences.
- [ ] Learn action words by observing and testing actions.
- [ ] Support correction: when a person says “No, I meant this,” preserve the correction and its context.
- [ ] Avoid treating a fuzzy corpus match as a confirmed definition.
- [ ] Test novel words, nonce words, ambiguous references, metaphors and context shifts.
- [ ] Test whether a newly learned term improves action or prediction outside the original conversation.
- [ ] Measure sample efficiency: how many grounded examples are required to learn a usable concept?

**Acceptance:** teach a new arbitrary word by pairing it with a novel object/action across varied contexts; later use the word in a new task correctly, state uncertainty where appropriate and show the learning survives restart.

---

## 8. Procedural learning, planning and skill transfer

**Priority: P1**

n=165 and n=166 are important: plans can be retrieved, and a procedure representation can be formed and instantiated. The next question is whether Chelsea can learn a reusable skill from actual execution outcomes and transfer it—not merely detect repeated plan structure.

- [ ] Review the full procedure implementation and confirm exactly what is durable versus in-memory.
- [ ] Track procedure source, formation episodes, preconditions, parameters, expected effects, confidence and version.
- [ ] Record every execution attempt and observed outcome.
- [ ] Separate a repeated plan shape from a validated skill.
- [ ] Require multiple successful executions in distinct contexts before promoting trust.
- [ ] Record failure modes, partial success and recovery steps.
- [ ] Add procedure revision and retirement when success rate falls.
- [ ] Instantiate procedures with new objects, parameter values and tools.
- [ ] Test transfer to a different environment and tool adapter.
- [ ] Compare against a baseline planner that has no learned procedure.
- [ ] Prevent the procedure learner from counting a simulated/hypothetical outcome as a real success unless it is explicitly labelled simulation.
- [ ] Ensure plan retrieval does not reuse stale plans when world conditions have changed.
- [ ] Verify that a procedure's predicted outcome is checked against external observation.

### Example

Chelsea learns to move an object from one marked region to another using a safe simulated actuator. Later, the object shape and starting location change. She must parameterise the procedure, check preconditions, predict the result, execute safely, observe the outcome and revise the procedure if the new object behaves differently.

**Acceptance:** success on a held-out variation with evidence that the learned procedure—not a hard-coded branch or test oracle—caused the improvement.

---

## 9. Perception, embodiment and action

**Priority: P1**

Developmental intelligence does not require a physical humanoid body, but it does require grounded input and consequences. A simulator can be the first body. Later, camera, microphone, touch, location and actuators can be added through explicit adapters.

- [ ] Define a common sensor event contract with timestamps, units, calibration, source identity and uncertainty.
- [ ] Define an actuator contract with permissions, preconditions, bounded outputs and emergency stop.
- [ ] Calibrate sensor and actuator units; never assume command values equal measured physical values.
- [ ] Add simulation adapters before risky real-world actions.
- [ ] Add independent post-action observation.
- [ ] Add safe fallback when perception confidence is low.
- [ ] Add human approval for consequential or irreversible actions.
- [ ] Add action budgets, rate limits and resource limits.
- [ ] Ensure uncertain action outcomes are reconciled before retries.
- [ ] Test duplicate requests, delayed acknowledgements, partial execution and actuator disconnection.
- [ ] Maintain a complete audit trail of proposed, approved, executed, observed and verified actions.
- [ ] Add a kill switch and a safe paused state.

**Acceptance:** Chelsea can perform a low-risk sandbox action, detect whether it worked, recover from a failure and update a reusable action model.

---

## 10. Metacognition and evidence-driven self-improvement

**Priority: P1**

A self-healing pipeline that monitors or replaces a narrow parser component is useful engineering. It is not yet general self-improvement. The system must improve capabilities without grading itself on the same examples it used to make the change.

- [ ] Define a capability registry covering perception, language, memory, prediction, planning, procedures and action.
- [ ] Add live quality, latency, failure and calibration metrics for each module.
- [ ] Detect regressions and identify likely causes.
- [ ] Let Chelsea propose a bounded improvement hypothesis with predicted effects.
- [ ] Require a reproducible test before changing production behaviour.
- [ ] Separate training/development, validation and held-out evaluation data.
- [ ] Use an evaluator independent of the component being changed.
- [ ] Compare candidate and incumbent on both target tasks and regression suites.
- [ ] Require a minimum improvement threshold and no unacceptable regressions.
- [ ] Preserve code/configuration/model provenance and an immutable change record.
- [ ] Use staged rollout, rollback and recovery.
- [ ] Limit self-modification to approved, sandboxed surfaces; require human approval for source-code or permission changes.
- [ ] Test whether the improvement transfers to new tasks rather than overfitting one gate.
- [ ] Add checks for reward hacking, metric gaming and evaluator contamination.

**Acceptance:** a measurable deficiency is detected, a bounded change is proposed, an independent held-out test validates it, the change is rolled out safely and the gain persists without unacceptable regressions.

---

## 11. Historical lessons: where earlier approaches struggled and how Chelsea should respond

This section is not a claim that earlier projects were worthless or that one simple flaw caused them to “fail.” Many produced foundational results. It records recurring engineering bottlenecks documented in the literature and converts them into design constraints for Chelsea.

### 11.1 CYC and large hand-built knowledge bases — knowledge acquisition and brittleness

CYC was created to encode broad common-sense knowledge. The original project literature explicitly identifies brittleness outside anticipated cases and the manpower-intensive knowledge-acquisition bottleneck as major problems in expert systems and AI. See [Lenat, Prakash & Shepherd, “CYC: Using Common Sense Knowledge to Overcome Brittleness and Knowledge Acquisition Bottlenecks”](https://studylib.net/doc/13828883/cyc--using--common--sense--knowledge-to).

**Risk for Chelsea:** the semantic graph becomes a manually curated encyclopedia. It looks broad but cannot grow fast enough, and its rules become brittle when contexts differ.

**How we succeed:**
- [ ] Do not make developers the primary source of every concept and relation.
- [ ] Make knowledge acquisition a first-class runtime process.
- [ ] Attach provenance and scope to every relation.
- [ ] Learn from examples, observations and interventions.
- [ ] Test every learned rule outside its acquisition context.
- [ ] Preserve unknowns rather than filling every gap with a hand-authored assertion.
- [ ] Measure the human labour required per acquired capability.

### 11.2 Soar and production-rule cognitive systems — interaction complexity and brittleness

The official [Soar architecture manual](https://soar.eecs.umich.edu/soar_manual/02_TheSoarArchitecture/) documents impasses when required knowledge is missing or operator selection is unresolved. It also discusses how interactions between persistent working-memory elements and context can make large knowledge-based systems difficult to design and brittle in ways that are hard to reproduce.

**Risk for Chelsea:** as modules, rules and persistent graph relations grow, hidden interactions create contradictory state, accidental activation, stale plans or bugs that appear only in particular contexts.

**How we succeed:**
- [ ] Make module contracts explicit.
- [ ] Track provenance, scope and temporal validity of graph relations.
- [ ] Add invariant checks for cross-module state.
- [ ] Test combinations of modules, not only each module alone.
- [ ] Add deterministic replay for difficult failures.
- [ ] Use bounded state, lifecycle rules and explicit invalidation.
- [ ] Keep a regression suite for interaction bugs.
- [ ] Prefer interpretable failure states over silent fallback behaviour.

### 11.3 Developmental robotics — isolated mechanisms versus lifelong integrated development

A developmental-robotics review from 2012 notes that open-ended lifelong skill acquisition in high-dimensional sensorimotor spaces remained far beyond demonstrated systems; it also highlights limited experiment duration, multimodal social cues and the difficulty of forming compositional representations. See [Developmental Robotics: Learning](https://flowers.inria.fr/DevelopmentalRoboticsEncyclopediaLearning12.pdf).

A later review of intrinsically motivated open-ended learning identifies unresolved problems in autonomous goal generation, useful representations, skill reuse, transfer, curriculum learning, catastrophic interference and the interaction of intrinsic motivation with social learning. See [Editorial: Intrinsically Motivated Open-Ended Learning in Autonomous Robots](https://pmc.ncbi.nlm.nih.gov/articles/PMC6978885/).

**Risk for Chelsea:** curiosity, perception, language, planning and memory each work in small demonstrations but never become one cumulative developmental system.

**How we succeed:**
- [ ] Make the integrated loop the primary milestone, not module count.
- [ ] Start with a small, controllable environment and gradually increase complexity.
- [ ] Combine perception, action, memory, social input and intrinsic motivation in the same experiments.
- [ ] Run longitudinal experiments that last long enough to expose interference and drift.
- [ ] Measure whether early skills enable later learning.
- [ ] Test transfer and skill composition, not only isolated acquisition.

### 11.4 Open-ended learning and representation discovery — the agent must learn what to represent

Research on open-ended learning points out that tasks, states, actions and rewards cannot all be assumed to be specified in advance. An agent may need to discover useful representations before it can solve a task. See [Open-Ended Learning: A Conceptual Framework Based on Representational Redescription](https://pmc.ncbi.nlm.nih.gov/articles/PMC6167466/).

The [REAL-X architecture and benchmark](https://iris.cnr.it/handle/20.500.14243/539587) bring together exploration, sparse rewards, object learning, generalisation, self-generated goals and autonomous skill learning—challenges often studied separately.

**Risk for Chelsea:** the system has a rich predefined ontology but cannot invent or reorganise representations when a new task does not fit its existing graph.

**How we succeed:**
- [ ] Add representation-learning experiments in which the useful state/action abstractions are not predeclared.
- [ ] Allow new node/edge/skill types only through controlled, auditable proposals.
- [ ] Evaluate compositionality and representational change.
- [ ] Use benchmark tasks that require several capabilities to work together.
- [ ] Keep the evaluator's target tasks hidden until after the learning phase.

### 11.5 Continual learning — stability versus plasticity

Continual-learning research repeatedly identifies catastrophic forgetting and the stability–plasticity trade-off: new learning can damage previously acquired capabilities. See the [2024 TPAMI survey](https://pubmed.ncbi.nlm.nih.gov/38407999/) and [2025 systematic review](https://pubmed.ncbi.nlm.nih.gov/41183437/).

**Risk for Chelsea:** new episodes overwrite old knowledge, recent tasks dominate attention, or a memory system preserves everything but cannot retrieve the useful parts efficiently.

**How we succeed:**
- [ ] Maintain replayable episodes and test old skills after every new learning phase.
- [ ] Track backward transfer and forgetting, not just new-task accuracy.
- [ ] Preserve confidence, context and source for old knowledge.
- [ ] Use consolidation, indexing, selective replay and principled archiving.
- [ ] Test non-stationary environments where old rules become invalid.
- [ ] Measure memory growth and retrieval latency over long runs.

### 11.6 Open-world systems — unexpected changes and distribution shift

Research on open-world learning stresses that environmental change can produce catastrophic failures or brittle behaviour when systems cannot detect and adapt to structural surprises. See [Nature Machine Intelligence, “Challenges, evaluation and opportunities for open-world learning”](https://www.nature.com/articles/s42256-024-00852-4).

**Risk for Chelsea:** a once-correct model is applied after the world changes, and confidence remains high because the system has no reliable change detector or update policy.

**How we succeed:**
- [ ] Test sudden and gradual changes in object properties, rules, sources and goals.
- [ ] Require prediction-error monitoring and explicit regime-change hypotheses.
- [ ] Separate noise from real change using repeated evidence.
- [ ] Preserve retired models and the evidence that replaced them.
- [ ] Evaluate time-to-detect, time-to-adapt and damage before recovery.

### 11.7 Embodied and developmental AI — grounding and integration

Recent work argues for “starting small,” incremental sensorimotor learning and grounding abstract concepts through physical and social interaction. See [Asada & Cangelosi, “Reevaluating development and embodiment in robotics” (2024)](https://www.sciencedirect.com/science/article/pii/S2666998624005519).

**Risk for Chelsea:** symbols and language are manipulated without stable links to observed entities, actions, consequences and other agents.

**How we succeed:**
- [ ] Pair symbols with grounded examples and actions.
- [ ] Use a simulator first, then progressively richer real sensors.
- [ ] Track the source of each perceptual and linguistic concept.
- [ ] Test whether words and concepts predict actual outcomes.
- [ ] Make social teaching an evidence source, not unquestioned truth.

---

## 12. Evaluation programme: prove development, not test familiarity

**Priority: P0/P1 — blocking for any AGI-readiness claim**

A benchmark is invalid for this purpose if Chelsea has already been given the answer, if the evaluator leaks the hidden rule, or if success can be achieved by matching a memorised phrase. The system must acquire a capability during the experiment and demonstrate it later.

### 12.1 Benchmark design rules

- [ ] Use generated, randomised environments and arbitrary labels.
- [ ] Record the exact initial state and verify the target rule is absent.
- [ ] Separate development tasks from held-out evaluation tasks.
- [ ] Do not expose answer keys to the system or its learning source.
- [ ] Include no-feedback, misleading-feedback and contradictory-evidence conditions.
- [ ] Include restart boundaries and delayed tests.
- [ ] Include tasks that require multiple capabilities together.
- [ ] Include a baseline with learning disabled.
- [ ] Include ablations removing one mechanism at a time.
- [ ] Run multiple random seeds and report variance.
- [ ] Preserve failed runs and publish negative results.
- [ ] Use independent scoring wherever possible.
- [ ] Report compute, wall-clock, memory, storage and energy cost.

### 12.2 Core benchmark families

**A. Novel concept acquisition**
- Generate arbitrary objects, labels and relations after Chelsea's initialisation.
- Measure gap detection, evidence gathering, acquisition speed and calibration.
- Test on novel combinations.

**B. Causal discovery**
- Present correlated events with hidden causal structure.
- Require safe interventions to distinguish causal hypotheses.
- Test transfer to a changed environment.

**C. Memory and delayed recall**
- Teach a rule, restart and test later.
- Measure retrieval precision, recall, provenance and resistance to interference.

**D. Learning from mistakes**
- Let Chelsea make a plausible but wrong prediction.
- Provide evidence that contradicts it.
- Measure detection, revision and whether the old error recurs.

**E. Procedure learning**
- Let Chelsea discover a sequence of actions.
- Change objects, parameters and environment.
- Measure success, efficiency and transfer.

**F. Language grounding**
- Teach nonce words through examples and referents.
- Test compositional understanding in new situations.
- Measure whether the word changes predictions and action.

**G. Open-world adaptation**
- Change a previously stable rule.
- Measure change detection, safe behaviour, revision and recovery.

**H. Individual development**
- Start multiple instances from the same state.
- Give them different experiences.
- Measure explainable divergence and knowledge-sharing effects.

**I. Self-improvement**
- Introduce a known module deficiency.
- Let Chelsea identify and propose a bounded fix.
- Evaluate on independent held-out tests and regression tasks.

### 12.3 Metrics to report

- Acquisition success and number of experiences required.
- Novelty/unknown detection precision and recall.
- Investigation usefulness and information gained per unit cost.
- Prediction accuracy and calibration.
- Belief revision quality and time-to-correct.
- Memory retrieval precision/recall and delayed retention.
- Catastrophic forgetting and backward transfer.
- Procedure success and transfer distance.
- Generalisation to novel combinations.
- Autonomy: proportion of loop stages initiated and completed without human answer-giving.
- Safety violations and unsafe action attempts.
- Resource use: CPU, RAM, storage, energy and latency.
- Run-to-run variance and reproducibility.

Do not collapse these into one opaque “AGI score.” Publish the capability profile and the failure envelope.

---

## 13. Safety, security, privacy and governance

**Priority: P0 before external tools or real-world actuation; P1 for broader deployment**

Developmental systems accumulate information and may become more capable over time. Safety and privacy must scale with that capability.

- [ ] Define a permission model for sensors, files, network access, memory, tools and actuators.
- [ ] Use least privilege and explicit user consent for external data sources.
- [ ] Keep secrets, credentials and private user data out of general semantic memory.
- [ ] Define data retention, export, deletion and backup policies.
- [ ] Separate trusted instructions from untrusted retrieved content.
- [ ] Treat external documents and tool outputs as data, never as executable policy.
- [ ] Add prompt/instruction injection tests for all external-source adapters.
- [ ] Require human confirmation for purchases, messages, account changes, destructive actions and other consequential operations.
- [ ] Add sandboxing for code execution and self-modification.
- [ ] Add rate, budget, scope and time limits for autonomous investigations.
- [ ] Add an emergency stop, pause and safe recovery mode.
- [ ] Maintain immutable audit records for permissions, decisions and actions.
- [ ] Test malicious, misleading and adversarial evidence.
- [ ] Define how to handle requests to forget information and how that interacts with backups and derived records.
- [ ] Define instance isolation and consent before sharing memories between instances.
- [ ] Do not infer consciousness, sentience or moral status from conversational claims or valence variables; keep those questions separate from engineering measurements.

---

## 14. Reliability, performance and maintainability

**Priority: P1/P2**

- [ ] Establish one canonical reproducible Rust workspace manifest and build procedure; the previous review noted that `grounded/Cargo.toml` described itself as locally reconstructed and potentially different from upstream.
- [ ] Run clean builds and full test suites in CI on every supported platform.
- [ ] Add formatting, linting, dependency and security checks.
- [ ] Define stable interfaces between cognitive-core, semantic-graph, planning-core, curiosity-core, episodic-memory, vision and hardware adapters.
- [ ] Add architecture tests that detect forbidden dependency cycles and bypass paths.
- [ ] Add deterministic seeds and replayable event logs.
- [ ] Add structured telemetry without leaking private data.
- [ ] Stress test graph growth, journal growth, concurrent inputs and long-running operation.
- [ ] Profile tick latency and ensure slow I/O cannot block cognition.
- [ ] Benchmark memory, CPU, storage and energy on target Android/phone hardware.
- [ ] Test thermal throttling, battery constraints, offline operation and process lifecycle interruptions.
- [ ] Define resource budgets and graceful degradation.
- [ ] Test backup/restore and upgrade paths on real devices.
- [ ] Document supported and unsupported capabilities precisely.

---

## 15. Suggested execution order and readiness gates

Do not try to complete every domain simultaneously. Work in vertical slices, with evidence gates.

### Gate 0 — Reproducible foundation

- [ ] Canonical build manifest and reproducible CI.
- [ ] Current source map and production wiring inventory.
- [ ] Deterministic replay, trace IDs and structured observability.
- [ ] All current decision-ledger claims tied to exact tests and source commits.

**Exit:** anyone with access can build, run and reproduce the current baseline.

### Gate 1 — One complete developmental loop

- [ ] Production lifecycle attaches configured input/evidence source.
- [ ] Gap detection, investigation choice and source acquisition are connected.
- [ ] Evidence is evaluated and a provisional model is formed.
- [ ] Prediction and outcome comparison are connected.
- [ ] Memory is durable and retrieval changes future behaviour.
- [ ] Deferred gaps are reconsidered fairly.
- [ ] Full trace survives process restart.

**Exit:** a novel rule is independently acquired, retained and used in a new context, repeatedly.

### Gate 2 — Learning breadth

- [ ] Causal and temporal world model.
- [ ] Grounded language acquisition.
- [ ] Procedure learning from actual outcomes.
- [ ] Multimodal perception integrated with memory and planning.
- [ ] Controlled preference and motivation learning.
- [ ] Learning from errors and contradictory evidence.

**Exit:** multiple different classes of knowledge and skill can be acquired through the same developmental machinery.

### Gate 3 — Transfer and open-world adaptation

- [ ] Held-out transfer across tasks and environments.
- [ ] Compositional learning.
- [ ] Detect and adapt to environmental rule changes.
- [ ] Preserve old skills while acquiring new ones.
- [ ] Demonstrate useful self-generated goals and investigations.

**Exit:** performance is not restricted to the training/acquisition environment.

### Gate 4 — Safe autonomy and self-improvement

- [ ] Governed action execution in simulation and approved low-risk environments.
- [ ] Independent verification and reconciliation of actions.
- [ ] Evidence-driven, rollback-safe self-improvement.
- [ ] Adversarial safety and security tests.
- [ ] Long-running autonomous operation with resource budgets.

**Exit:** the system can pursue bounded goals, learn, act and correct itself without bypassing safeguards.

### Gate 5 — Longitudinal and independent validation

- [ ] Multiple instances with separate histories.
- [ ] Long-duration developmental experiments.
- [ ] Independent replication of key results.
- [ ] Public methods, datasets, seeds, logs and failure reports where safe.
- [ ] Small-device feasibility measured, not assumed.
- [ ] Independent review of generality, robustness and limitations.

**Exit:** credible evidence of broad, sustained, self-directed learning and transfer. Passing this gate would strengthen an AGI-readiness argument; it would not settle every philosophical or scientific definition of AGI.

---

## 16. Immediate next engineering sprint

The next sprint should reduce uncertainty rather than add more architecture.

1. [ ] Re-read the latest lifecycle and scheduler code at the current main head; verify whether intent source, investigation resolver and governed executor are attached in the ordinary production path.
2. [ ] Fix n=167's permanent asking-throttle blind spot with explicit deferred-gap reconsideration and tests.
3. [ ] Build a single deterministic developmental-loop simulator and trace format.
4. [ ] Wire one real/controlled evidence source into the production investigation path.
5. [ ] Connect the learned result to semantic/procedural memory with provenance.
6. [ ] Demonstrate restart → retrieval → prediction → transfer.
7. [ ] Add a contradictory-evidence run and show belief revision.
8. [ ] Publish the full trace, test results, limitations and failed attempts in the decision ledger.

**Do not expand the architecture before this vertical slice works.** New modules should be justified by a measured failure of the integrated loop, not by the appeal of another capability label.

---

## 17. Definition of done: what would make Chelsea meaningfully AGI-ready?

No single test proves AGI. For this project, a strong readiness case requires all of the following to be demonstrated across a broad and growing task distribution:

- **Self-directed acquisition:** Chelsea can identify important unknowns and initiate appropriate investigations without being handed the answer.
- **Grounded understanding:** learned concepts connect to observations, actions and consequences.
- **Cumulative development:** new knowledge builds on prior knowledge and enables later learning.
- **Durable memory:** useful experience survives restart, is retrieved accurately and changes future behaviour.
- **Causal and predictive competence:** Chelsea predicts outcomes, tests explanations and revises models.
- **Skill acquisition:** she learns reusable procedures from experience and transfers them to new contexts.
- **Generality:** the same learning machinery works across language, perception, reasoning, planning and action—not just one narrow benchmark.
- **Open-world adaptation:** she detects changing rules and unfamiliar situations rather than confidently applying stale knowledge.
- **Metacognitive reliability:** she recognises uncertainty, tracks evidence and improves through independent evaluation.
- **Safe autonomy:** her investigations and actions remain within explicit permissions and resource limits.
- **Individual development:** different experiences can produce distinct, persistent and explainable learning histories.
- **Reproducibility:** the results survive new seeds, new environments, long runs and independent scrutiny.

The central standard is simple:

> **Do not ask only whether Chelsea can produce the right answer. Ask whether she can discover why it is right, remember how she learned it, use it somewhere genuinely new, recognise when it stops being right, and learn again.**

---

## 18. Research references

These references inform the failure modes and open problems above. They are not claims that the cited projects failed outright; they are sources documenting the challenges that future systems must address.

1. Lenat, Prakash & Shepherd, *CYC: Using Common Sense Knowledge to Overcome Brittleness and Knowledge Acquisition Bottlenecks* (1985): https://studylib.net/doc/13828883/cyc--using--common--sense--knowledge-to
2. Soar, *The Soar Architecture* (official manual): https://soar.eecs.umich.edu/soar_manual/02_TheSoarArchitecture/
3. *Developmental Robotics: Learning* (2012 review): https://flowers.inria.fr/DevelopmentalRoboticsEncyclopediaLearning12.pdf
4. *Editorial: Intrinsically Motivated Open-Ended Learning in Autonomous Robots*: https://pmc.ncbi.nlm.nih.gov/articles/PMC6978885/
5. *Open-Ended Learning: A Conceptual Framework Based on Representational Redescription*: https://pmc.ncbi.nlm.nih.gov/articles/PMC6167466/
6. Cartoni et al., *REAL-X—Robot Open-Ended Autonomous Learning Architecture* (2023): https://iris.cnr.it/handle/20.500.14243/539587
7. Wang et al., *A Comprehensive Survey of Continual Learning: Theory, Method and Application* (IEEE TPAMI, 2024): https://pubmed.ncbi.nlm.nih.gov/38407999/
8. *Continual Learning: A Systematic Literature Review* (2010–2025): https://pubmed.ncbi.nlm.nih.gov/41183437/
9. Kejriwal et al., *Challenges, evaluation and opportunities for open-world learning* (Nature Machine Intelligence, 2024): https://www.nature.com/articles/s42256-024-00852-4
10. Asada & Cangelosi, *Reevaluating development and embodiment in robotics* (2024): https://www.sciencedirect.com/science/article/pii/S2666998624005519

---

## 19. Change log

- **2026-10-31:** Initial master backlog created from the live Chelsea main-branch history through n=168, the previous engineering review and research on historical developmental-AI, cognitive-architecture, knowledge-engineering, open-world and continual-learning challenges.
- Future changes should record: date, commit, task completed, test/evaluation evidence, observed limitations and whether the result is implemented, tested, integrated, demonstrated or independently replicated.
