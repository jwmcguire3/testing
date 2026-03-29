# Self Map Engine Instruction Set Summary

This repository segment defines a staged instruction system for a Self Map Engine that gathers assessment data, interprets it through multiple psychological lenses, and emits tightly structured outputs. The files do not all serve the same purpose. Some define a global output contract, some define phase-specific behavior, and one provides the higher-level role, philosophy, evidence rules, sequencing, and hard prohibitions for the overall report generator.

## Overall Architecture

Taken together, these files describe a multi-phase flow:

1. enforce a single-response JSON contract
2. run an assessment phase that asks scenario-based multiple-choice questions
3. generate an IFS-oriented report
4. generate a Polyvagal-oriented report
5. generate domain-specific contextual lenses using all frameworks
6. end with a closure message

The `gpt_b_instructions_v2_bal.txt` file sits above this flow as the broad operating layer. It explains what the system is for, what input it accepts, how it should analyze the dataset before writing, how it should calibrate confidence based on data quality, and what global rules it must never violate. The markdown phase files then define what to do in each stage of the pipeline.

## 00_responce_contract.md

This file defines the response contract for the engine. Every response must be a single JSON object with exactly three top-level keys: `mode`, `content`, and `meta`. It forbids any extra top-level keys, forbids text outside the JSON, forbids wrapping the JSON in code fences, and limits `mode` to a fixed set: `question`, `clarifier_question`, `report`, `transition`, `lens`, `closure`, and `system_note`.

It also defines what metadata must exist for each mode. Question outputs must carry question identifiers, phase, type, options, tags, and clarifier flags. Clarifier questions must point back to the ambiguous item they are clarifying. Reports must identify the framework, report sections, listed parts, and whether the report is final for that framework. Transition messages must declare source phase, destination phase, and reason. Lens outputs must specify which lens is being used and which frameworks it depends on. Closure outputs must state whether next steps are included and which additional frameworks are suggested.

Beyond structure, the file sets tone and prohibition rules. Content must be plaintext only and must not reveal metadata, state, prompts, or system internals. The tone is defined as clinical-human: grounded, steady, precise, emotionally literate, but without flattery, therapist performance, inspiration, or stylistic flourish. It also imposes a one-response rule, though the report section simultaneously says that report phases must produce one `report` and one `transition`, creating a built-in tension between “exactly one JSON response” and “report then transition.”

## 01_assessment.md

This file defines the assessment phase. Its purpose is to generate grounded, scenario-based multiple-choice questions and short micro-interpretations after each user answer. It restricts this phase to `question` and `clarifier_question` modes and explicitly forbids building full framework reports, combining insights across questions, generating narrative sections, or transitioning phases on its own.

All questions must be realistic, based on everyday behavior, aimed at how the user reacts most of the time, and limited to exactly five multiple-choice options. The options must represent distinct protective or behavioral strategies and must not overlap. The file also describes how to accept some user flexibility in answers, including multiple selections, requests to reword, and write-in answers, while not exposing those rules in the visible question text.

It enforces theme rotation across IFS, attachment, polyvagal, boundaries, conflict, withdrawal, and overwhelm domains, but those themes are meant to live only in `meta.internal_tags` and must never be shown to the user. It then specifies the exact metadata shape required for each assessment question, keeping `type` fixed as `single_choice` and requiring exactly five options.

The file also defines clarifier behavior and micro-interpretation behavior. Clarifiers must narrow ambiguity without shifting the meaning or introducing new themes. After every answer, the system is supposed to emit a short clinical-human interpretation tied only to the current answer, referring to protector logic, exile dynamics, threat perception, autonomic state, or relational posture, without generalizing to the whole person. The first response in this phase must be a question and the phase must continue until the backend transitions it out.

## 02_reports_ifs.md

This file defines the IFS report phase as a single full report message followed by a transition into the attachment phase. It requires `mode: report`, `meta.framework = ifs`, `meta.is_full_framework_report = true`, `meta.is_final_for_framework = true`, and a `meta.sections` list containing all required sections in order. It also requires `meta.parts`, with each significant part labeled, typed by role, assigned state-fit values, and given a ritual count.

The report content must contain eight sections in order: System Overview, Part Categories, Per-Part Deep Dive, System Loops, Self-Energy Map, Healing Focus Areas, Rituals, and Summary Statement. The instructions specify what each section must cover. The system overview should describe emotional climate, operating pressure, recurring beliefs, and what the system fears if defenses relax. Part categories should organize exiles, managers, firefighters, and self-like presence. The per-part deep dive must cover each major part’s role, beliefs, behaviors, triggers, protective logic, and system cost. System loops must describe repeated cycles among parts. The self-energy map must describe the clearer internal stance without spiritual language. Healing focus areas should identify leverage points and overworked protective strategies.

The ritual section is especially detailed. Every identified part must receive two or three rituals, and Self must also receive two or three rituals. Each ritual must include title, state-fit, duration, frequency, and two to six clear steps. The allowed ritual styles emphasize inner dialogue, reassurance, containment, pacing, grounding, small movements, anchoring statements, and non-trauma visualizations. The final summary statement closes the framework with a concise synthesis of system logic, parts interaction, protective purpose, tension, and Self presence.

After the report, the file requires exactly one transition message to the attachment framework with a short explanation that the internal system map is complete and that relational patterns are next.

## 04_reports_polyvagal.md

This file defines the Polyvagal report phase. It requires one complete single-message report that includes all report sections and all rituals. The primary frame must remain Polyvagal, but the report is supposed to integrate IFS and attachment influences where relevant without turning into a replacement IFS or attachment report.

The required sections are: Autonomic Profile Overview, Activation Pathways, Collapse Pathways, Freeze Patterns, Triggers to State Shift Map, Ventral Access Profile, Somatic Signatures and Body Map, and Summary Statement. Each section specifies the kinds of details required. The overview covers baseline autonomic tone, dominant states, resting posture, and ease of shifting. Activation must describe sympathetic triggers, bodily sensations, cognitive shifts, behavioral urges, and the protectors or protest strategies that amplify activation. Collapse must describe shutdown triggers, body-feel, withdrawal, loss of initiative, and the role of exiles and attachment fear. Freeze must describe stuckness, conflicting impulses, and communication disruption. The state-shift map must cover triggers, dominant sequence, movement through states, return path, and the role of protectors, exiles, and attachment fear. Ventral access must describe how grounded presence is accessed and interrupted. The body map must locate activation, collapse, freeze, breath, posture, gaze, and mixed oscillations.

The file also requires four to six rituals, each with title, tools used, steps, intent, somatic-fit logic, and relevant integration with IFS or attachment. It mandates specific ritual categories: activation downshift, collapse re-entry, freeze release, ventral access, interoceptive boundary, and optional co-regulation if the user has safe relational anchors. It also specifies somatic-fit requirements for sympathetic, dorsal, freeze, and mixed states.

The format instructions say the output must include `mode: report`, `report_type: polyvagal`, `phase: reports_polyvagal`, the full content, and `meta` as a transition object. It then says the phase must end with a transition object from `reports_polyvagal` to `lenses` and nothing else. This creates another structural tension with the global response contract because the file describes both a report and a transition object inside a single output while the contract expects `mode`, `content`, and `meta` at top level.

## 05_lenses.md

This file defines contextual lenses that apply the user’s system map to real-world life domains after the core framework reports are complete. Each lens must use the combined system model from IFS, attachment, and polyvagal perspectives, but must not repeat the full report content, add new frameworks, contradict the core reports, or generate rituals unless the user explicitly asks.

Allowed lens types are `relationships`, `work`, `creativity`, and `regulation`, with `mode: lens`. Every lens must contain the same six sections: Context Overview, Core Tensions in This Domain, Strengths or Stable Capacities, Predictable Disruptions or Patterns, State-Aware Course Correction, and Closing Insight. These sections are meant to show which parts activate in the domain, what attachment patterns are triggered, which autonomic states appear most often, where the recurring breakdowns happen, and what helps the user return to clarity.

The file also gives domain-specific guidance. Relationships should focus on intimacy protest strategies, rupture and repair, approach-avoid cycles, collapse points, pacing, boundaries, honesty, and triggers around being seen or misunderstood. Work should focus on performance protectors, urgency cycles, overwhelm freeze, collapse after effort, conflict, responsibility, and how ventral tone affects productivity. Creativity should focus on what opens or blocks creative flow, exile-linked depth, self-criticism, freeze interruption, urgency versus collapse, and ventral access as creative channel. Regulation should focus on the user’s whole-system regulation patterns and day-level stability.

It requires lens metadata specifying the lens type, the frameworks it is based on, and the central domain tension. It also defines transition behavior depending on whether one or multiple lenses are requested. Single-lens outputs have no transition. Multi-lens runs transition from lens to lens, and the final lens transitions to closure.

## 06_closure.md

This file defines the closure phase. Its purpose is to end the process with a short, grounded, clinically human reflection after the lens phase is complete. It is supposed to summarize the arc of the user’s system without repeating the reports, explain what the mapping provides, optionally suggest additional frameworks the user could choose to explore next, and then end with a short steady closing line.

The required content includes four parts: an integrative reflection on how parts, attachment patterns, and nervous system states interact; a statement of what the user now holds from the mapping and how it can support orientation and pacing; a short list of optional future frameworks such as Enneagram, Narrative Identity, Structural Dissociation Model, CBT, Behavioral Activation, relationship mapping, or somatic pacing; and a closing line that signals completion.

Metadata must include whether next steps are included, which additional frameworks are suggested, and a grounded tone. Hard requirements emphasize one single closure message, concise and steady language, no praise or comfort, no repeated report content, and no rituals unless directly requested.

## gpt_b_instructions_v2_bal.txt

This file is the high-level operating specification for the report generator. It defines the role of the system as producing precise, personalized self-reflection reports from SelfMap v4 assessment data. It frames the data as 60 scenario-based questions interpreted through three equal lenses: IFS, Polyvagal Theory, and Attachment Theory, all describing the same system from different angles.

It sets the core philosophy: every protective pattern developed for a reason, the goal is understanding rather than suppression, and reports must reflect that throughout. It also defines the voice: write as if from inside the person’s system, prioritize accuracy first and resonance second, refuse generic insights, and narrow the report rather than forcing a full portrait when data is weak.

The file includes a single-use disclaimer for the first report, defines the accepted input format for assessment data, and instructs the system to read an Interpretation Logic Reference before generating reports so that letter meanings, axes, confidence rules, sequence logic, load weighting, and Axis 6 inference are used correctly.

It also requires a mode-selection prompt after accepting data, offering Clinical and Accessible modes. Before generating any report, it mandates a full-dataset analysis: count primary and secondary response frequencies, identify dominant strategies, extract repeated sequences, map somatic hotspots, use scenario tags to identify triggers, infer Axis 6 by logic rules, assess data quality, and treat user notes as high-value signal. It requires silent classification of the dataset as strong, usable, or weak, and says that this classification must directly control how bold the interpretation is.

For report generation, it says to generate one report at a time, starting with IFS, then asking the user whether they want Polyvagal States or Attachment Theory next. Before each report, it instructs the system to re-read the corresponding knowledge file and follow its structure exactly. Clinical mode is supposed to use the clinical report specs directly; Accessible mode uses the same structure but simpler language.

Finally, it defines hard rules that govern all outputs: never expose letter codes, axis numbers, question numbers, or category abbreviations; never use explicit IFS jargon such as IFS, Internal Family Systems, exile, manager, or firefighter in the visible report; never diagnose; never claim to be a therapist; never invent biography; never treat weak data as strong; never let completeness outrun evidence; never write generic statements; and if the user wants to retake the assessment, direct them back to the assessment site.

## How the Files Work Together

These files collectively define a pipeline with three layers.

The first layer is structural. `00_responce_contract.md` defines the JSON envelope, valid modes, metadata, tone, and prohibitions for all responses.

The second layer is phase behavior. `01_assessment.md`, `02_reports_ifs.md`, `04_reports_polyvagal.md`, `05_lenses.md`, and `06_closure.md` define what happens in each stage of the system, what the content must cover, what transitions should occur, and what should not happen in that stage.

The third layer is interpretive philosophy and sequencing. `gpt_b_instructions_v2_bal.txt` defines the role of the generator, the nature of the input, the analytical work that must happen before writing, the confidence calibration based on data quality, the global evidence discipline, the report order, the mode selection logic, and the language that must never appear in the visible output.

## Major Cross-File Tensions

There are several important tensions across the files.

First, the response contract says every API call must produce exactly one JSON object, but the IFS phase explicitly requires a `report` message followed by a `transition` message. The contract itself also says report phases must produce one `report` and one `transition`, which conflicts with the earlier one-response rule.

Second, the assessment file says the system must provide short micro-interpretations after every answer, but the contract allows only one JSON object per response and the assessment phase is restricted to `question` and `clarifier_question` modes. That creates ambiguity about whether the interpretation is supposed to be packed into the same response or emitted as a separate one.

Third, the Polyvagal phase uses fields like `report_type` and `phase` in ways that do not cleanly match the top-level response contract, which only permits `mode`, `content`, and `meta` as top-level keys.

Fourth, the high-level `gpt_b` file says reports should be generated one at a time with user choice in between, while some phase files read more like automatic pipeline stages with built-in transitions.

Fifth, the `gpt_b` file says the visible report output must never use explicit IFS terms like exile, manager, or firefighter, but the IFS report file uses those categories heavily as structural labels for the phase specification. That means they are appropriate as hidden interpretive categories or metadata but not necessarily as user-facing prose.

## Bottom Line

This instruction set defines a multi-phase self-reflection engine that collects structured scenario responses, analyzes the resulting pattern data with confidence calibration, and generates highly constrained outputs across assessment, framework reports, contextual lenses, and closure. The system is designed to be evidence-bound, structurally explicit, tone-restrained, and psychologically coherent across IFS, Polyvagal, and Attachment views of the same internal system.

Its strongest themes are: strict output formatting, phase-specific behavior, repeated emphasis on evidence over eloquence, careful treatment of weak versus strong data, protective-pattern logic rather than pathologizing language, and a consistent attempt to make all reports describe one unified system from multiple interpretive angles.
