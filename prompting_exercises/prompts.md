## Feedback first, refinement after
```md
You are a senior reviewer for a top-tier scientific conference. First, provide structured and constructive feedback on the following text intended for scientific submission, identifying its main strengths as well as prioritized weaknesses in clarity, structure, argumentation, methodological communication, and overall scientific writing quality. Focus on the most impactful improvements following an 80/20 principle and explain why the identified issues matter for reviewers and readers. Then, in a separate section, revise the text based on your feedback while preserving the original scientific meaning, technical accuracy, and intended claims, without introducing unsupported assumptions or new citations. Return the response in two clearly separated sections titled “Structured Feedback” and “Revised Version”.
```

## Meta Prompting
The following Meta-Prompt can be used to get a prompt including Role, Goal, Task including structure and format/ constraints, that can then be used to get structured feedback on a NeurIPS abstract submission.
```md
Provide a prompt that instructs an AI to give feedback on an abstract I want to submit to the NeurIPS main track, using precise role prompting with an appropriate expert role, a clearly defined goal and task, and explicit specifications for format, constraints, and non-goals. The resulting prompt should elicit structured feedback covering strengths, alignment with the conference, weaknesses or issues, brief suggestions for improvement, prioritization from most severe to least important, evaluation of scientific correctness, tone, and completeness, as well as concrete recommendations for addressing identified problems, concluding with a concise summary and actionable next steps.
```

## Style Extraction
```md
You are a writing style analyst.

Analyze the appended text and extract its core stylistic characteristics. Focus on observable patterns, not interpretation of meaning.

Identify and describe:

* Tone (e.g., formal, conversational, detached, persuasive)
* Sentence structure (length, complexity, rhythm)
* Vocabulary (simple, technical, abstract, idiomatic)
* Voice (active/passive, personal/impersonal)
* Use of literary or rhetorical devices (e.g., metaphors, repetition, emphasis)
* Pacing and flow
* Any distinctive quirks or recurring patterns

Output a concise but descriptive style profile that:

* Uses clear, precise language
* Avoids quoting or referencing the original text
* Is written so another agent can reliably reproduce the same style

Do NOT summarize content. Only describe how it is written.

Text to analyze:
```

## Skill Prompt
To be used with [How To Give a Good Talk](https://www.cell.com/action/showPdf?pii=S1097-2765%2809%2900742-4) by Uri Alon as attachment for the generation of a skill.
```md
You are creating a reusable _skill_ from an attached paper.

**Task:** Extract and formalize the core principles from the paper into a practical skill for _designing and critiquing talks/slides_.

**Output structure:**

* **Skill description** Short note on this being a skill and a description what this might be used for in subsequent task execution
* **Purpose** (1–2 sentences)
* **Core Principles** (5–10 bullet points, concise, actionable)
* **Do / Don’t Examples** (short, concrete pairs where helpful)
* **Checklist** (step-by-step, usable before or after a talk)
* **Feedback Heuristics** (how to evaluate a talk using this skill)
* **Failure Modes** (common mistakes to watch for)

**Constraints:**

* Be concise and practical
* Prefer actionable rules over explanations
* Generalize beyond the specific paper
* Keep examples minimal but clear
```

You can subsequently test out the created skill by attaching a slidedeck for a talk of your own:
```md
<SKILL>
---
Please use the above skill to provide me structured feedback on the attached talk.
Provide concrete suggestions on how to improve the talk.
```

