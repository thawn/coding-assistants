# Multi-Stakeholder Review Summary
## AI-Assisted Triage of Patient Portal Messages in Outpatient Oncology

---

## Overview of Verdicts

| Reviewer | Role | Verdict | Risk Level |
|---|---|---|---|
| Dr. Elena Hartmann | Principal Investigator / Scientific Reviewer | Support with revisions | High |
| Dr. Marcus Weber & Sandra Koch | Clinical Practitioner (Oncologist / Nurse Lead) | Support with revisions | High |
| Ingrid Schneider | Data Protection / Compliance Officer | **Major concerns** | High |
| Prof. Anna Müller | Research Ethics / IRB Reviewer | Support with revisions | High |
| Claudia Bauer | Patient Advocate / Patient Representative | Support with revisions | High |

> **All five reviewers independently assigned a High risk level.** The data protection reviewer is the sole voice calling for a complete hold until blocking legal issues are resolved; the remaining four support conditional progression with substantive revisions.

---

## Points Most Stakeholders Support

**1. Shadow-mode prospective deployment (endorsed by all five reviewers)**
Every reviewer independently praised the decision to run the model in parallel with — not instead of — human triage for three months before any operational integration. This was seen as scientifically sound, ethically conservative in the right direction, and a practical safety measure that protects patients during evaluation.

**2. Human oversight retained throughout (endorsed by all five reviewers)**
The explicit commitment that final triage decisions remain with clinicians was universally acknowledged as the correct architectural choice. It avoids the most dangerous failure mode (fully automated escalation decisions), mitigates GDPR Art. 22 concerns around solely automated consequential decisions, and preserves clinical accountability.

**3. Sensitivity for urgent cases as primary outcome (endorsed by scientific and clinical reviewers)**
Framing the primary outcome around sensitivity rather than accuracy or F1 reflects an appropriate understanding of the asymmetric cost of triage errors in oncology. False negatives (missed urgent cases) carry far greater clinical harm than false positives. Both scientific and clinical reviewers viewed this as more sophisticated than typical clinical AI proposals.

**4. Pseudonymization before cloud transmission (acknowledged by all five, though with major caveats)**
All reviewers recognised the step of pseudonymizing messages before API transmission as a meaningful baseline commitment. However, every reviewer — most forcefully the data protection officer — noted that as stated, it is a label rather than a specification, and that pseudonymized health data remains personal data under GDPR.

---

## Points of Strongest Concern

**1. Absence of patient transparency and consent (raised by ethics, patient advocate, data protection)**
No reviewer found any consent or notification mechanism for patients. Patients whose historical messages form the training data were never asked. Patients whose live messages will be processed during shadow mode are not informed. Oncology patients write in a context of profound trust and vulnerability; processing their communications with a cloud-hosted LLM without disclosure is an ethical breach and, in the data protection officer's assessment, a GDPR Art. 13/14 violation independent of all other compliance requirements.

**2. Language exclusion creates a structural equity and safety gap (raised by all five reviewers)**
The exclusion of messages in languages other than German or English — affecting patients with Turkish, Arabic, Farsi, Polish, and other language backgrounds — was the single concern raised by every reviewer. Clinical reviewers called it "clinically unacceptable without mitigation"; ethics called it "ethically unjustified and potentially discriminatory"; the patient advocate warned of a two-tier triage system; the scientific reviewer flagged an uncharacterised coverage gap; the data protection officer noted a bounded but auditable scope. None accepted the exclusion as a neutral technical convenience.

**3. Pseudonymization is underspecified and may be legally insufficient (raised by data protection, ethics, scientific, clinical)**
The proposal's single sentence — "all messages pseudonymized before transmission" — was insufficient for every reviewer who examined it. Oncology portal messages routinely contain quasi-identifiers (patient-written names, drug regimens, surgery dates, rare diagnoses) that survive the removal of ID fields. Under GDPR Recital 26, re-identification risk determines legal status, not the label applied. No technical specification, NER pipeline, re-identification risk assessment, or residual risk evaluation is provided.

**4. No Data Protection Impact Assessment (DPIA) (blocking concern raised by data protection; noted by ethics)**
GDPR Art. 35 mandates a DPIA for large-scale systematic processing of special category health data and for profiling. This project satisfies all three mandatory criteria. The absence of any DPIA is not a procedural gap — it is a legal barrier. The data protection officer's position is that no data access can begin until a completed, approved DPIA is in place.

**5. Bias in training data will encode historical triage inequities (raised by scientific, clinical, ethics, patient advocate)**
The model learns to replicate historical nurse triage decisions. If historical triage was influenced by patient age, gender, ethnicity, communication style, or socioeconomic status — as documented in multiple oncology settings — those biases will be encoded and potentially amplified at scale. No bias audit, subgroup analysis, or mitigation plan is included in the proposal. This concern was characterised as a structural risk, not a minor methodological limitation.

---

## Stakeholder-Specific Concerns

### Scientific Reviewer (Dr. Hartmann)
- No statistical power calculation, no pre-specified sensitivity threshold, no minimum urgent-case event count for the shadow period — making results uninterpretable regardless of outcome.
- Training and evaluation use the same label source (historical nurse decisions), risking circular validation. No independent clinical adjudication of labels is described.
- No meaningful clinical baseline comparator (e.g., rule-based keyword system or current manual workflow) is included.
- The choice between fine-tuning and prompting is left open; these have fundamentally different failure modes, reproducibility properties, and regulatory implications.
- No post-deployment monitoring plan for concept drift over time.

### Clinical Reviewer (Dr. Weber & Koch)
- Complete absence of failure mode and effects analysis (FMEA). The dangerous failure is not a crash but a plausible-looking, confidently worded wrong classification that nurses accept under cognitive load.
- Treatment context (current regimen, cycle day, prior toxicity) is absent from message text alone. A message that is urgent on day 8 of CHOP chemotherapy is routine in another context — and the model will not know the difference.
- The "3am legibility problem": LLM rationale output will be skimmed in seconds under high workload; it must be short, structured, and symptom-specific, not probabilistic prose. This was never evaluated.
- Override governance is entirely undeveloped. "Final decisions remain with clinicians" is a declaration, not a protocol.

### Data Protection / Compliance Officer (Ingrid Schneider)
- The third-party API provider is not named. No Data Processing Agreement (DPA) under GDPR Art. 28 is mentioned. Many commercial LLM providers reserve rights to use submitted data for model improvement, which would constitute unauthorised secondary processing of Art. 9 health data.
- The legal basis under GDPR Art. 9(2) for processing special category health data is not stated in the proposal. Without one, all processing from first data access is potentially unlawful.
- LLM fine-tuning on 80,000 patient messages creates memorisation risk: models can reproduce training examples under targeted prompting, meaning patient data could be embedded in and extracted from model weights.
- The proposal conflates "de-identified" (section 3) with "pseudonymized" (section 7) — legally and technically distinct terms under EU law.
- EU AI Act high-risk classification obligations (Annex III, healthcare AI) have not been assessed or acknowledged.

### Ethics / IRB Reviewer (Prof. Müller)
- Accountability gap: the statement "final decisions remain with clinicians" does not address automation bias — the documented tendency to defer to algorithmic recommendations under cognitive load. Liability frameworks must be explicit before deployment.
- Shadow mode is not ethically neutral. Nurses who repeatedly see AI recommendations internalise them even without acting on them; clinical norms can shift during evaluation in ways that are difficult to detect and hard to reverse.
- The language exclusion is characterised not as an operational limitation but as an ethical choice that creates durable structural inequality in care quality for a protected group.
- "Clinician satisfaction" as a secondary outcome is insufficient as an ethical safeguard; clinicians may be satisfied with a system that saves time even if it disadvantages certain patient groups.

### Patient Advocate (Claudia Bauer)
- Portal messages in oncology are written under conditions of fear and trust: patients may disclose suicidal ideation, fears of recurrence, or grief in ways they would not voice aloud. Processing this communication without disclosure is a betrayal of the therapeutic relationship.
- Psychosocial and mental health crisis content is poorly suited to urgency classification trained on historical outcomes; past human triagers may themselves have under-flagged such content. False negatives here are not performance metrics — they are patients in crisis who were missed.
- The opt-out mechanism (not currently proposed) must be accessible by phone, available in multiple languages, and free of any care consequence — otherwise it is not meaningful consent.
- Elderly and digitally marginalised patients who learn retrospectively that AI has been reading their messages may disengage from portal communication entirely, creating a downstream safety risk.
- Anchoring effect: even in shadow mode, the perpetual visibility of AI recommendations changes how nurses read messages. This patient safety concern is unaddressed in the design.

---

## Disagreements Between Stakeholders

| Topic | Position |
|---|---|
| **Overall approval** | Data protection calls for a complete hold pending legal remediation. All others support conditional progression with revisions. |
| **Pseudonymization** | Data protection treats the current specification as a blocking legal gap. Ethics and patient advocate view it as a meaningful but insufficient step. Scientific and clinical reviewers note governance and technical concerns but treat it as correctable. |
| **Language exclusion** | Ethics frames it primarily as a justice and anti-discrimination issue. Clinical frames it as a patient safety and equity gap. Patient advocate frames it as a structural vulnerability issue for already-marginalised patients. Scientific frames it as a coverage and generalisability gap. Data protection views scope limitation as a governance advantage — the one reviewer to note a partial governance benefit. |
| **Shadow mode** | All agree it is the right design, but for partly different reasons: scientific reviewers value the prospective test set; clinical reviewers value the preserved human-first decision chain; ethics notes the shadow mode is not ethically neutral and can shift norms; patient advocates are concerned that nurse reading behaviour will change even before deployment. |
| **Consent for retrospective training data** | Ethics and patient advocate call for explicit consent mechanisms or formally justified waivers. Data protection specifically advises *against* retrospective consent (citing power imbalance and operational infeasibility), recommending the Art. 9(2)(j) research exemption with documented safeguards instead. |

---

## Top 5 Recommended Revisions

### 1. Establish a patient transparency and consent framework before any data access
*(Unanimously required by ethics, patient advocate, data protection)*

Before the shadow-mode phase begins: update the portal privacy notice to disclose AI-assisted processing; provide a plain-language patient information sheet (in all languages used by the patient population); implement a meaningful, accessible opt-out mechanism with no care consequences. For the retrospective training dataset: determine whether existing broad consent covers LLM-based third-party processing; if not, obtain a formally justified and IRB-approved consent waiver. This is a precondition for all other work.

### 2. Complete and submit a DPIA; name the API provider and execute a GDPR Art. 28 DPA
*(Required by data protection; supported by ethics and clinical)*

A full Data Protection Impact Assessment covering both the retrospective training and prospective shadow deployment phases must be completed and approved by the Data Protection Officer before any patient data is accessed. The third-party LLM API provider must be named, and a legally binding Data Processing Agreement must be in place explicitly prohibiting secondary use of submitted data. The legal basis under GDPR Art. 9(2) must be documented in full. EU AI Act classification under Annex III must be assessed.

### 3. Provide a technically specified pseudonymization methodology with re-identification risk assessment
*(Required by data protection; strongly supported by scientific, clinical, ethics)*

The proposal must specify the exact pseudonymization pipeline: NER system used, quasi-identifier categories targeted (names, dates, drug regimens combined with rare diagnoses, physician names, geographic markers), handling of free-text clinical content, runtime error detection, and fallback behavior. A re-identification risk assessment appropriate to the oncology cohort must be conducted and submitted. The real-time pseudonymization pipeline for shadow-mode inference must be separately described and validated.

### 4. Add a formal statistical power calculation and pre-specify all primary analysis parameters
*(Required by scientific reviewer; strongly supported by clinical)*

Before shadow-mode deployment begins: provide a formal power calculation specifying assumed urgency prevalence, target sensitivity, acceptable 95% confidence interval width, and required number of urgent-case events. Pre-register the decision threshold (sensitivity/specificity operating point), the temporal train/validation/test split dates, and the minimum acceptable sensitivity for live deployment approval. Include at least one non-LLM clinical baseline comparator (e.g., current manual workflow or keyword-alert system). Register the full protocol on a recognised study registry.

### 5. Conduct a pre-training bias audit and mandate subgroup performance analyses
*(Required by ethics; strongly supported by scientific, clinical, patient advocate)*

Before model training begins: audit the historical 80,000-message dataset for systematic patterns in staff triage decisions across patient subgroups (age, gender, language, cancer type, treatment phase). Document disparities and treat historical labels as potentially biased ground truth rather than neutral gold standard. Pre-specify subgroup analyses by demographic and linguistic characteristics as mandatory secondary outcomes of the shadow evaluation. Report separately on model performance for messages with emotional distress markers and psychosocial crisis content.

---

## Final Overall Recommendation

**Conditional approval — do not proceed until blocking items are resolved.**

This proposal addresses a genuine and serious clinical need. The shadow-mode design is exemplary, the primary outcome is clinically anchored, and the team has demonstrated baseline awareness of data governance and patient safety. Four of five reviewers support the project proceeding in principle.

However, the proposal has three categories of blocking gap that must be fully resolved before any patient data is accessed or any deployment activity begins:

1. **Legal and regulatory gaps** (no DPIA, no named API provider, no documented GDPR Art. 9(2) legal basis) that render current planned processing potentially unlawful;
2. **Ethical gaps** (no patient transparency or consent framework, no bias mitigation plan, no accountability chain) that fail to meet the minimum ethical standards for research involving a vulnerable population; and
3. **Scientific gaps** (no power calculation, circular validation design, no clinical baseline, no pre-specified thresholds) that would make the study results scientifically uninterpretable.

None of these is insurmountable. With substantive revision — particularly the five priority revisions above — this project could become approvable, scientifically credible, and genuinely beneficial to patients and clinical staff alike. The committee recommends resubmission after the required changes are addressed, with particular urgency given to the DPIA, the patient consent framework, and the bias audit protocol.

---

*Summary compiled from five independent stakeholder reviews:*
- `review_scientific.md` — Dr. Elena Hartmann, Principal Investigator / Scientific Reviewer
- `review_clinical.md` — Dr. Marcus Weber & Sandra Koch, Clinical Practitioner (Oncologist / Nurse Lead)
- `review_data_protection.md` — Ingrid Schneider, Data Protection / Compliance Officer
- `review_ethics.md` — Prof. Anna Müller, Research Ethics / IRB Reviewer
- `review_patient_advocate.md` — Claudia Bauer, Patient Advocate / Patient Representative
