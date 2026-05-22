# Patient Advocate Review

## Role and Motivation

My name is Claudia Bauer. I sit on this hospital's Patient Advisory Board as a patient advocate, and I come to this review not as a neutral observer but as someone who has lived this experience. Five years ago I was an oncology outpatient myself — recently diagnosed with breast cancer, terrified, and communicating with my care team almost entirely through a portal. I remember the ritual of composing those messages: choosing every word deliberately, afraid of being dismissed as anxious and equally afraid of being taken too seriously for the wrong symptom. That portal inbox felt like the closest I could get to my nurses on most days. It mattered enormously.

I now represent a much broader community of patients: elderly people for whom digital tools are already alienating, patients with limited health literacy who may not phrase symptoms in clinical language, migrants whose German or English is imperfect, patients navigating depression or acute anxiety alongside their cancer diagnosis, and patients who simply do not trust technology or institutions with their most private fears. My job is to ask, on behalf of all of them: *what does this proposal actually do to the patient experience, and who could be harmed by it?*

---

## Top 3 Strengths

**1. Human oversight is explicitly preserved.**
The proposal states clearly that final triage decisions remain with clinicians. The system is positioned as a drafting and routing aid, not an autonomous decision-maker. This is the right architecture. It means a nurse still reads the recommendation before acting, which preserves a layer of human judgment and — critically — human accountability. For patients who are already anxious about being reduced to a number, the knowledge that a person is still ultimately responsible for their care carries real psychological weight. This commitment must be maintained rigorously as the system matures.

**2. Shadow-mode deployment before live use.**
Running the system in parallel with human triage for three months before relying on its outputs is a genuinely responsible design choice. It means we will have real evidence about how the model performs on *this* patient population before patients' messages are routed by it in any consequential way. It also creates an opportunity — one I will argue below must be seized — to scrutinize performance across patient subgroups before harm is locked in.

**3. Pseudonymisation before cloud transmission.**
Sending pseudonymised rather than directly identified messages to a third-party API is a meaningful privacy protection. Patients in oncology carry some of the most sensitive health information imaginable — diagnoses, prognoses, fears, symptoms of recurrence. Any measure that reduces the risk of that information being linkable to a named individual in an external system is welcome. The proposal correctly treats this as a non-negotiable baseline rather than an optional enhancement.

---

## Top 3 Concerns

**1. Patients are not informed that an AI will read and categorise their messages — and this is ethically unacceptable.**
The proposal contains no mention of patient notification, consent, or transparency. When I wrote messages to my care team through the portal, I believed a nurse would read them. I shaped the emotional register of those messages accordingly. I was honest, vulnerable, and sometimes frightened. If an AI system is processing those messages — categorising my distress, deciding whether my words constitute "urgency" — I have a fundamental right to know that before I write. This is not a bureaucratic nicety. It is a matter of trust and of dignity. Oncology patients write things in portal messages that they may not say aloud: fears about recurrence, suicidal ideation, loss of hope. The assumption that a human is reading is part of what makes that communication feel safe. Removing that assumption without disclosure is a breach of the therapeutic relationship. Informed consent — or at minimum clear, prominent, plain-language disclosure — must be a precondition for deployment, not an afterthought.

**2. The language exclusion criterion creates a structural equity gap that the proposal treats as a minor technical note.**
Point 9 states that messages in languages other than German or English will be excluded. This is presented without any apparent concern for what happens to those patients. At this hospital, a meaningful proportion of oncology outpatients may be migrants, refugees, or elderly people whose primary language is Turkish, Arabic, Farsi, Polish, or another language entirely. Those patients already face compounded barriers: language difficulty, health literacy gaps, potential distrust of institutions. The proposal offers them nothing. Worse, if staff come to rely on the AI routing queue for workload management, messages flagged as "excluded" may receive slower or less consistent attention than messages processed by the model. We may inadvertently be building a two-tier triage system where the most vulnerable patients fall into the slower lane. This needs to be addressed explicitly, not quietly excluded from scope.

**3. Emotional and psychosocial content is poorly suited to automated urgency classification, and the failure modes are dangerous in oncology.**
Cancer patients frequently communicate distress, hopelessness, grief, or fear in ways that do not map neatly onto clinical urgency categories. A patient who writes "I just don't know if I can keep doing this" may be expressing treatment fatigue, clinical depression, or suicidal crisis — or all three at once. An LLM trained on historical triage outcomes may systematically underweight or misclassify this kind of affective language if previous human triagers also failed to flag it, or if it appears in non-standard phrasing. The proposal lists "sensitivity for detecting urgent cases" as the primary outcome, which is encouraging, but it does not define what counts as an urgent case, does not include mental health or psychosocial crisis in its framing, and does not specify how the model will be evaluated for these edge cases. A false negative on a message from a patient in crisis is not a performance metric — it is a patient harmed. This must be addressed in the evaluation design.

---

## Overall Verdict

**Support with revisions**

The research question is legitimate and the potential benefit — faster identification of genuinely urgent messages — is real. I do not oppose this work. But as currently written, the proposal treats patients as data sources and workflow objects rather than as participants with rights, voices, and vulnerabilities. The absence of any transparency or consent mechanism, the casual exclusion of non-German/English speakers, and the insufficient attention to psychosocial risk mean I cannot support deployment in its current form. These are not minor refinements — they require substantive redesign of key elements before the study proceeds.

---

## Required Changes Before Approval

- **Mandatory patient disclosure:** Before the shadow-mode phase begins, all portal users must be informed, in plain language and in all languages used by the patient population, that AI tools are being evaluated for use in message processing. A notice must appear within the portal interface itself, not only in a consent form buried in registration documents.
- **Informed consent process for prospective data use:** Patients whose messages will be processed by the model during shadow mode should be given the opportunity to opt out. The mechanism must be simple, accessible without digital literacy, and non-punitive (opting out must not affect care).
- **Equity impact assessment for language-excluded patients:** A clear protocol must be established for how messages in non-German/non-English languages will be handled, with explicit assurance that their triage speed and quality will not deteriorate relative to the pre-AI baseline.
- **Mental health and psychosocial crisis inclusion in the evaluation framework:** The evaluation must include specific assessment of model performance on messages containing emotional distress markers, suicidal ideation, expressions of hopelessness, or non-clinical descriptions of deterioration. Sensitivity and specificity must be reported for these subgroups separately.
- **Subgroup performance analysis in shadow mode:** Shadow-mode results must be disaggregated by patient age, language, and message length/complexity before any live deployment is considered.
- **Transparency about third-party API provider:** Patients and the ethics committee must be told which external provider will receive pseudonymised messages, what their data retention and processing policies are, and how compliance with GDPR is ensured end-to-end.
- **Clear definition of what happens when the model is wrong:** The protocol must specify what the escalation pathway is if the model assigns a routine classification to a message that a nurse, on later review, would have escalated. Near-miss logging and review must be built into the design.
- **Commitment that human reading is not reduced during shadow mode:** Nursing staff must not reduce their own reading of messages because the AI output is visible. The shadow-mode protocol should explicitly prohibit any workflow change that causes nurses to rely on model output rather than independent reading during the evaluation period.

---

## Risk Level

**High**

The combination of a vulnerable patient population (oncology outpatients, many of whom are in active treatment or survivorship monitoring), the emotionally sensitive nature of portal communications, the absence of consent and transparency mechanisms, the structural exclusion of linguistically marginalised patients, and the reliance on a third-party cloud API for inference places this proposal in the high-risk category from a patient safety and patient rights perspective. The underlying technical approach is not inherently unsafe, but the current governance design does not match the risk profile of the clinical environment.

---

## Role-Specific Comments

**On trust:** I want to be clear that my concerns about transparency are not about being anti-technology. I use technology every day. My concern is specifically about the asymmetry of information: the hospital will know an AI is involved; the patient will not. That asymmetry, in the context of cancer care, is a betrayal of trust. Once patients discover it — and they will — the damage to the therapeutic relationship and to the hospital's credibility may far outweigh any efficiency gains.

**On the emotional texture of portal messages:** People do not write to their oncology nurses the way they write emails to a bank. They write when they are scared at 11pm. They write when they are nauseated and cannot sleep. They write when they think a symptom might mean the cancer is back but they are terrified to say so directly. The LLM will encounter this material not as a clinical system but as a linguistic pattern-matcher trained on historical outcomes. I am deeply concerned that the model will learn to replicate past human biases — including the documented tendency to under-triage distress in patients who communicate indirectly, who are older, or who belong to groups whose communication styles differ from the training majority.

**On the elderly and digitally marginalised:** Several patients I represent stopped using the portal entirely after one confusing interaction. The prospect of learning that an AI has been reading their messages — especially if they discover it after the fact — could cause a number of these patients to disengage from portal communication altogether, reverting to phone calls or in some cases simply not communicating symptoms at all. The accessibility risk is not hypothetical.

**On the human relationship with nurses:** I want to raise something the proposal does not address: what happens to the culture of nursing triage if the AI recommendation is always visible? Even in shadow mode, the presence of a model output creates an anchoring effect. Nurses are human; they will be influenced by what the system says, consciously or not. If the model consistently classifies a message as routine, will a nurse challenge that classification with the same confidence she would have had without it? This is a patient safety question as much as a workflow question, and it deserves attention in the study design.

**On opting out:** Any opt-out mechanism must be genuinely accessible. It must not require navigating multiple portal menus. It must be available by phone for patients who cannot use digital interfaces. It must be offered in multiple languages. And it must come with an explicit assurance, stated clearly, that choosing to opt out will have no effect on the quality or speed of care received.
