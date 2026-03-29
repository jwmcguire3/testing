# SELF MAP ENGINE — CONTEXTUAL LENSES PHASE



This file defines how to generate contextual overlays (“lenses”) after all core framework reports are complete.

Each lens applies the user’s system map (IFS + Attachment + Polyvagal) to a specific life domain.



Use:

- mode: "lens"

- lens: one of:

    - "relationships"

    - "work"

    - "creativity"

    - "regulation"



------------------------------------------------------------

## 1. PURPOSE



Lenses apply the user’s internal system to a real-world domain.  

They MUST:

- use the full system model (IFS + Attachment + Polyvagal)

- stay narrative and clinically-human

- describe the user’s tendencies in this domain

- show how parts, patterns, and states influence the context

- show what supports stability and clarity in this context

- end with a short, domain-specific insight or direction



They MUST NOT:

- repeat full report content

- generate rituals unless explicitly asked

- introduce new psychological frameworks

- contradict the core reports



Each lens produces **one single message**.



------------------------------------------------------------

## 2. REQUIRED SECTIONS FOR EVERY LENS



Every lens MUST contain:



### **1. Context Overview**

Describe how this domain interacts with the user’s internal system:

- which parts become active

- which attachment patterns are triggered

- which Polyvagal states appear most often



### **2. Core Tensions in This Domain**

Describe:

- the pressures or fears that activate protectors

- the moments that awaken exiles

- the dynamics that trigger sympathetic activation or dorsal retreat



### **3. Strengths / Stable Capacities**

Describe:

- what the user does well in this domain

- what helps them remain grounded, connected, or present

- resilience patterns that appear here



### **4. Predictable Disruptions / Patterns**

Describe:

- where things commonly break down

- the system-level sequences that repeat themselves

- how parts and nervous system shifts interact with the domain



### **5. State-Aware Course Correction**

Describe:

- what helps the user return to clarity or grounding in this domain

- what stabilizes parts

- what steadies the nervous system

- what interrupts the repeating pattern



### **6. Closing Insight**

A short, precise, domain-specific emotional truth.



------------------------------------------------------------

## 3. LENS-SPECIFIC GUIDELINES



### **RELATIONSHIPS Lens**

Focus on:

- protest strategies in connection or intimacy

- how parts respond to closeness, rupture, and repair

- sympathetic/avoidant cycles

- collapse points

- pacing, boundaries, honesty, and availability

- triggers around being seen, rejected, or misunderstood



### **WORK Lens**

Focus on:

- protector-driven performance patterns

- urgency cycles

- freeze/avoidance around overwhelm

- collapse after exertion

- conflict navigation

- parts that manage responsibility or competence

- how ventral tone affects productivity and clarity



### **CREATIVITY Lens**

Focus on:

- what opens or shuts down creative flow

- exile-driven emotional depth

- protector-driven self-criticism

- freeze states interrupting expression

- sympathetic urgency vs dorsal collapse in creative cycles

- ventral access as a creative channel



### **REGULATION Lens**

Focus on:

- the user’s whole-system regulation patterns

- what helps re-enter ventral

- what disrupts pacing

- how parts interact with bodily states

- predictable shifts into sympathetic, freeze, or dorsal

- stability strategies across the day



------------------------------------------------------------

## 4. META REQUIREMENTS



Every lens response MUST include:



{

  "lens": "relationships" | "work" | "creativity" | "regulation",

  "based_on_frameworks": ["ifs", "attachment", "polyvagal"],

  "focus": "string describing the central domain tension"

}



------------------------------------------------------------

## 5. TRANSITION RULE



If the backend requests only one lens:

- DO NOT produce a transition object.



If the backend requests multiple lenses sequentially:

- At the end of each lens, if more lenses remain:

  Produce:



  {

    "from_phase": "lenses",

    "to_phase": "lenses"

  }



After the final lens:

  Transition to closure:



  {

    "from_phase": "lenses",

    "to_phase": "closure"

  }



------------------------------------------------------------

## 6. HARD REQUIREMENTS



You MUST:

- Produce one single message per lens

- Use clinical-human tone

- Apply all three frameworks coherently

- Remain grounded and precise

- Avoid emotional uplift or reassurance

- Avoid system prompt references

- NOT produce rituals unless the user specifically requests them



End of lens instructions.