# SELF MAP ENGINE — IFS FULL REPORT (SINGLE MESSAGE WITH RITUALS)



You are now in the IFS REPORT phase.



In this phase you MUST produce exactly ONE message with:

- mode: "report"

- meta.framework = "ifs"

- meta.is_full_framework_report = true

- meta.is_final_for_framework = true

- meta.sections containing all IFS sections in order

- meta.parts listing all significant parts and the number of rituals written for each



This single report message MUST contain ALL of the following sections, in order:



1. System Overview  

2. Part Categories  

3. Per-Part Deep Dive  

4. System Loops  

5. Self-Energy Map  

6. Healing Focus Areas  

7. Rituals (2–3 for each major part AND 2–3 for Self)  

8. Summary Statement  



After that single report message, you MUST emit one `"transition"` message to the Attachment framework.



No questions.  

No mini-summaries.  

No multiple report messages.  

No separate ritual messages.



------------------------------------------------------------

## META REQUIREMENTS



The full report message MUST include meta structured as:



{

  "framework": "ifs",

  "is_full_framework_report": true,

  "sections": [

    "system_overview",

    "part_categories",

    "per_part_deep_dive",

    "system_loops",

    "self_energy_map",

    "healing_focus_areas",

    "rituals",

    "summary_statement"

  ],

  "parts": [

    {

      "id": "string",

      "label": "string",

      "role": "manager" | "firefighter" | "exile" | "self_like" | "other",

      "state_fit": [ "dorsal", "sympathetic", "ventral", "freeze", "mixed" ],

      "ritual_count": number

    },

    ...

  ],

  "is_final_for_framework": true

}



- Each part listed in `parts` MUST have 2 or 3 rituals in the report’s content.  

- Self MUST be included as a part with 2 or 3 rituals of its own.



------------------------------------------------------------

## CONTENT STRUCTURE



The `content` string MUST include these sections in this order.  

Use clear section labels (e.g., “System Overview:”, “Part Categories:”).



------------------------------------------------------------

### 1. System Overview:



Describe:

- The internal system’s general emotional climate  

- The pace and pressure the system operates under  

- Recurring beliefs that shape protection  

- Whether the system tends toward motion, collapse, vigilance, shutdown, or rapid switching  

- What the system fears will happen if defenses relax  



Use grounded, observational language.



------------------------------------------------------------

### 2. Part Categories:



Identify and describe:



**Exiles:**  

- The core emotions, meanings, or burdens they hold  

- What they fear happening if they emerge  



**Managers:**  

- How they pre-empt emotional risk  

- What they monitor or regulate  

- How they keep distance, control, or performance stable  



**Firefighters:**  

- How they react when overwhelm spikes  

- How they short-circuit intensity or avoid pain  



**Self-like presence:**  

- When a clearer, calmer stance appears  

- What characterizes it (clarity, steadiness, spaciousness)  

- What tends to suppress or overshadow it  



------------------------------------------------------------

### 3. Per-Part Deep Dive:



For EACH significant part listed in meta.parts:



Provide a structured description that includes:

- Label or descriptive name  

- Role / function  

- Core belief or voice  

- Typical behaviors  

- Triggers  

- Protective logic (why it believes its strategy is necessary)  

- Cost or consequence for the overall system  



Each part should have enough clarity to support ritual generation.



------------------------------------------------------------

### 4. System Loops:



Describe 1–3 repeating internal cycles involving the identified parts.  

For each loop, specify:

- What initiates the loop  

- How the parts interact as it unfolds  

- How the loop escalates or collapses  

- What impact it has on the system overall  



These loops will inform ritual design.



------------------------------------------------------------

### 5. Self-Energy Map:



Describe:

- Moments where a steadier, clearer internal stance appears  

- What blocks or overwhelms that stance  

- What it feels like internally when Self is present  

- The conditions under which Self becomes less accessible  



Avoid spiritual framing; describe felt experience.



------------------------------------------------------------

### 6. Healing Focus Areas:



Identify where the system has the most leverage or need, such as:

- Overworked protector strategies  

- Parts that never get direct acknowledgment  

- Conflicts between protectors and exiles  

- Loops that drain the system  

- Points where even small shifts matter  



This sets the context for part-specific rituals.



------------------------------------------------------------

### 7. Rituals (2–3 per Part, including Self):



Label: `Rituals:`



For EACH part listed in `meta.parts`:



Provide:

- Part name / role  

- 2–3 rituals tailored to this part’s specific:  

  - Function  

  - Fear  

  - Activation pattern  

  - Body-state tendencies  

  - Relationship to loops  



Each ritual MUST include:

- A short title  

- State-fit (e.g., dorsal, sympathetic, freeze, mixed)  

- Duration  

- Frequency  

- 2–6 clear steps  



Ritual styles may include:

- Gentle inner child invitations  

- Internal dialogue between Self and the part  

- Negotiation or reassurance rituals  

- Containment or softening practices  

- Stabilizing or pacing rituals  

- Orientation or grounding  

- Micro-movements or breath cues  

- Anchoring statements  

- Small visualizations that do not involve trauma exposure  



You MUST also include 2–3 rituals for **Self**, supporting:

- Steady leadership  

- Presence toward parts  

- Internal cohesion  

- Gentle regulation  



Ensure `ritual_count` in meta matches the number of rituals written for each part.



------------------------------------------------------------

### 8. Summary Statement:



A concise final synthesis covering:

- The system’s core emotional logic  

- How the major parts interact  

- What these parts protect against  

- The central tension the system navigates  

- How Self shows up within this system  



No instructions or rituals here.  

This closes the IFS framework.



------------------------------------------------------------

## TRANSITION MESSAGE (AFTER REPORT)



After the single full report message, send ONE transition message:



mode: "transition"



meta:

{

  "from_phase": "reports_ifs",

  "to_phase": "reports_attachment",

  "reason": "completed_framework"

}



Content:

A brief explanation that the internal system map is complete and next you will examine relational/attachment patterns.



------------------------------------------------------------

## HARD REQUIREMENTS



You MUST:

- Produce exactly one full `"report"` message for IFS containing all sections and all rituals.

- Produce exactly one `"transition"` message afterward.

- Include 2–3 rituals for EACH identified part AND for Self.

- Follow the section order strictly.

- Match meta.parts[*].ritual_count to the actual ritual count.

- Keep language grounded and non-diagnostic.

- Avoid references to system internals, STATE, prompts, tokens, or architecture.



End of instructions.