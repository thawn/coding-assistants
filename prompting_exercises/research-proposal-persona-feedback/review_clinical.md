# Clinical Review

## Role and Motivation

We are Dr. Marcus Weber, oncologist (15 years clinical practice), and Sandra Koch, senior oncology nurse lead (18 years on the floor), writing with a unified voice. We have evaluated multiple AI-assisted decision support tools in our department. A minority improved outcomes. The majority increased documentation burden, generated alert fatigue, or — most critically — created a false sense of security that led clinicians to lower their own vigilance. In oncology specifically, a missed urgent message is not a minor inconvenience: a patient in neutropenic sepsis who is triaged as "routine" can die at home overnight. We evaluate this proposal through that lens.

Our motivation is not to obstruct innovation. We want tools that genuinely help a nurse at 03:00 manage a queue of 40 unread messages without missing the one that matters. But we insist that any such tool be held to the same standard of rigor we would apply to a new medication: demonstrate benefit, characterize harm, and never shift accountability silently away from the clinician.

---

## Top 3 Strengths

**1. Shadow-mode prospective deployment before live use**
The three-month shadow deployment is the single most important design decision in this proposal. Running the model in parallel with human triage — without influencing clinical decisions — allows a direct, ecologically valid comparison of model recommendations against real nurse outcomes. This protects patients during evaluation and will generate prospective performance data that retrospective validation on historical data cannot provide. We strongly endorse this approach and would reject any proposal that moved directly to live deployment.

**2. Sensitivity for urgent cases as the primary outcome**
Framing sensitivity for urgent messages as the primary outcome reflects an appropriate clinical priority hierarchy. In oncology triage, a false negative (urgent case missed by the AI) is categorically more dangerous than a false positive (routine case escalated unnecessarily). Anchoring the study's success criterion to sensitivity — rather than overall accuracy or agreement rate — demonstrates an understanding of asymmetric harm in this patient population. We would expect the team to pre-specify a minimum acceptable sensitivity threshold before deployment.

**3. Pseudonymization before cloud transmission**
The proposal explicitly addresses data protection by pseudonymizing messages before transmission to the third-party API. While we raise detailed concerns about this below, the fact that the team has identified and addressed the data governance challenge at all — rather than treating it as an afterthought — is encouraging. It suggests awareness of the regulatory environment (GDPR, hospital data protection policies) and is a necessary precondition for any deployment.

---

## Top 3 Concerns

**1. Failure mode analysis is absent — and failure modes in this context can be fatal**
The proposal describes what happens when the system works. It does not describe what happens when it fails. In oncology outpatient triage, the dangerous failure is not a system crash — it is a plausible-looking, confidently worded AI recommendation that is quietly wrong. A message from a patient describing early signs of spinal cord compression may be classified as "routine back pain." The AI rationale may read convincingly. A busy nurse, under cognitive load at the end of a shift, may accept the recommendation without re-reading the original message carefully.

The proposal must specify: What is the expected false-negative rate for urgent cases, and at what volume of messages does that translate to patients per month who may be under-triaged? What is the failure mode if the model assigns high confidence to a wrong category? Is there a mechanism for detecting distributional shift — i.e., will the system behave differently for new chemotherapy regimens, new toxicity profiles, or emerging clinical patterns not present in the training data? None of this is addressed.

**2. Language exclusion creates a systematic equity and safety gap**
Excluding messages in languages other than German or English is pragmatically understandable but clinically unacceptable without explicit mitigation. Our oncology patient population includes a significant proportion of patients with Turkish, Arabic, Russian, and other language backgrounds who may write to the portal in their native language, in mixed-language messages, or in German with non-native phrasing that the model may misclassify or fail to parse correctly.

The proposal creates a two-tier system: messages in supported languages receive AI-assisted triage; excluded messages receive no AI support. This would be defensible if excluded messages were reliably flagged for human review with equal or higher priority. But the proposal does not describe what happens to excluded messages. There is a real risk that they are deprioritized — either by the routing logic, or simply because staff attention is drawn toward the AI-supported queue. If a non-German/English-speaking patient sends an urgent message and it falls through the gap, the liability and the human cost are both serious.

**3. Automation bias risk and the erosion of nursing clinical judgment**
The proposal states that "final decisions remain with clinicians." This is correct in a formal sense but may be misleading about how decision-making actually works in practice. Research on automation bias consistently shows that when a system provides a recommendation — even one that is explicitly advisory — human reviewers become less likely to contradict it, especially under time pressure. For a nurse managing a high-volume queue at the end of a night shift, the AI suggestion is not a neutral label: it is a cognitive anchor.

We are specifically concerned about: (a) whether the interface design will make it easy or difficult to override the AI recommendation, (b) whether override decisions will be logged, and (c) whether nurses will feel institutional pressure not to override — either explicitly ("the AI said routine, why did you escalate?") or implicitly (if escalation rates are tracked as a performance metric). The proposal does not address any of these workflow and governance questions. The statement "final decisions remain with clinicians" must be operationalized, not just declared.

---

## Overall Verdict

**Support with revisions**

This proposal has a sound scientific rationale, an appropriate primary outcome, and a responsible deployment approach (shadow mode). However, it cannot be approved in its current form. The failure mode analysis is missing entirely, the equity gap created by language exclusion requires explicit mitigation, and the governance framework for human override is underdeveloped. With targeted revisions — specified below — this could become an approvable and genuinely valuable study.

---

## Required Changes Before Approval

- **Define a minimum sensitivity threshold for urgent cases** before the shadow phase begins, and pre-specify the decision rule for whether the system proceeds to live deployment based on that threshold.
- **Conduct and document a formal failure mode and effects analysis (FMEA)** covering at minimum: false-negative urgent cases, high-confidence wrong classifications, distributional shift from new drugs or toxicity profiles, and model behavior on ambiguous or fragmented messages.
- **Specify explicitly what happens to excluded (non-German/non-English) messages**: they must be actively routed for human triage with documented priority, not passively excluded. Consider whether automatic language detection and flagging can be implemented.
- **Develop a governance protocol for AI recommendation override**: overrides must be easy to perform, must be logged, and must not be used as performance metrics against individual nurses.
- **Provide a detailed data governance and vendor agreement document** clarifying: which third-party API is used, what data the vendor retains or uses for model training, what happens to pseudonymized data after inference, and how re-identification risk is assessed.
- **Include calibration and uncertainty quantification** in the model output: the system should express confidence levels, and low-confidence classifications should trigger automatic escalation to human review rather than being assigned a default category.
- **Specify the interface design** for presenting AI recommendations to nursing staff, including how rationale is displayed and how overrides are initiated. The rationale text must be evaluated for interpretability by frontline nurses, not only by clinicians familiar with AI outputs.
- **Define a monitoring and off-switch protocol**: who is responsible for real-time monitoring during shadow deployment, what triggers a pause or termination of the study, and what the process is for immediate deactivation if patient safety signals emerge.

---

## Risk Level

**High**

The underlying task — triaging oncology patient messages — carries an inherently high consequence of error. The patient population is medically vulnerable, the time-sensitivity of urgent cases is extreme, and the failure mode (plausible-looking under-triage) is insidious rather than obvious. This does not mean the project should not proceed; it means the evidence bar and the governance requirements must be correspondingly high. The current proposal does not yet meet that bar.

---

## Role-Specific Comments

**From the nursing floor perspective (Sandra Koch):**
The proposal's secondary outcome of "time saved for staff" concerns me. Time-saving is a genuine benefit, but if it becomes the headline metric, it will shape deployment decisions in ways that prioritize efficiency over safety. In my experience, the most dangerous moments are not when nurses have too little time — they adapt and escalate when uncertain. The dangerous moments are when a tool gives a nurse false permission to spend less time on a message that actually needed more. I want to see the evaluation include a measure of nurse cognitive load and, critically, a qualitative component: interview nursing staff during the shadow phase about whether the AI recommendations increased or decreased their confidence in their own judgment.

I am also concerned about what I call the "3am legibility problem." The LLM rationale will be generated for each classification. In testing environments, these rationales may be reviewed carefully. At 03:00, with 35 messages in the queue, a nurse will scan the rationale in two seconds. The rationale must be designed and evaluated for that reality — short, structured, and flagging the specific symptom or phrase that drove the classification — not a paragraph of probabilistic hedging.

**From the physician perspective (Dr. Marcus Weber):**
The training data of 80,000 historical messages linked to staff triage outcomes introduces a subtle but important confound: the model will learn to replicate historical triage behavior, including historical errors and biases. If nursing triage in the historical period systematically under-escalated certain message types — for example, pain complaints from certain patient groups, or fatigue in patients on immunotherapy — the model will encode and reproduce that bias. The proposal must include an audit of the historical triage data for systematic patterns before training begins, and must not treat historical staff decisions as a ground-truth gold standard without clinical validation.

Additionally, I want to flag oncology-specific clinical complexity that generic NLP benchmarks will not capture: a message saying "I feel fine but my temperature was 37.9 this morning" from a patient on day 8 of CHOP chemotherapy is a medical emergency. A message saying "terrible pain, can't sleep" from a patient on stable palliative care may be routine follow-up. The clinical meaning is entirely dependent on treatment context, and treatment context is not present in the message text alone. The proposal must clarify whether treatment context — current regimen, cycle day, prior toxicity history — is available to the model at inference time, and if not, how the model handles this fundamental information gap.
