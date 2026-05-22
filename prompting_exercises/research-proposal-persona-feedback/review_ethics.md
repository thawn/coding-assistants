# Ethics Review

## Role and Motivation

I am Professor Anna Müller, Chair of the Research Ethics Committee at this institution. My evaluation draws on 25 years of reviewing proposals at the intersection of medicine, technology, and human vulnerability. My driving concern is not whether a system is technically clever, but whether the people most affected by it — in this case, adult oncology patients navigating fear, illness, and complex care systems — are protected from harm, treated with dignity, and given genuine agency over how their information is used.

I welcome AI research that can meaningfully benefit patients. Overburdened triage nurses in oncology miss urgent messages, and the consequences can be severe. The promise of this proposal is real. But promise does not suspend ethical obligation. My scrutiny will be proportional to the stakes: these are patients facing cancer, interacting with a system they trust, and whose messages may determine whether a medical emergency is caught in time.

---

## Top 3 Strengths

**1. Human oversight is structurally preserved.**
The proposal explicitly states that final triage decisions remain with clinicians. The AI is framed as a decision-support tool, not a decision-maker. This is the correct architectural choice for a high-stakes clinical domain. It avoids the most dangerous failure mode — autonomous escalation or suppression of urgency without human review — and keeps clinical accountability legible and located.

**2. Shadow mode deployment limits direct patient harm during evaluation.**
By running the model in parallel with, rather than in replacement of, human triage for the initial three months, the proposal creates a meaningful empirical test without exposing patients to consequential AI decisions they have not consented to. Patients continue to receive unmodified human triage throughout. This is methodologically sound and ethically conservative in the right direction.

**3. Pseudonymization before cloud transmission is a meaningful data protection step.**
The decision to pseudonymize messages before transmitting to the third-party inference API reflects awareness of data protection obligations under GDPR and reduces — though does not eliminate — the risk of re-identification or data breach. This demonstrates baseline privacy awareness and is a necessary minimum for any cloud-mediated processing of health-adjacent communication.

---

## Top 3 Concerns

**1. Absence of informed consent from patients whose messages are used — both retrospectively and prospectively.**
The proposal uses approximately 80,000 historical messages for training and then deploys a live system, in shadow mode, that processes real-time patient communications. No mention is made of patient consent at either stage. "De-identified" and "pseudonymized" do not mean "consented to." Oncology patients who wrote to their care team had a reasonable expectation that their messages would be read by clinical staff — not processed by a large language model, transmitted to a third-party cloud API, and stored as training or inference data. The shadow mode framing does not eliminate this concern: patients' words are still being processed by an AI system without their knowledge. This is not a technical detail. It is a foundational ethical violation if unaddressed.

**2. Algorithmic bias embedded in training data reflecting historical triage inequities.**
The model will be trained on historical staff triage outcomes. If historical nurse triage was influenced — consciously or unconsciously — by factors such as patient age, gender, socioeconomic status, communication style, or cultural background, those biases will be encoded into the model and potentially amplified at scale. Oncology departments have documented disparities in how urgency is perceived and acted upon across patient groups. A model that learns from biased labels will systematically under-flag urgent messages from already-disadvantaged patients, precisely those who most need equitable care. The proposal contains no bias audit plan, no subgroup analysis by demographic or linguistic characteristics, and no mechanism to detect or mitigate this risk.

**3. Exclusion of non-German/English-speaking patients is ethically unjustified and potentially discriminatory.**
Patients who write in Turkish, Arabic, Russian, Polish, or other languages commonly used in this region are simply excluded. The proposal offers no clinical pathway for their messages during the study period — no statement that they receive equivalent triage, no discussion of what happens to them. If the system is eventually deployed, these patients will either be excluded entirely from AI-assisted triage (receiving slower or less consistent care) or their messages will be processed by a system not evaluated on their communications. Either outcome constitutes differential treatment of a protected group on the basis of national origin and language. This exclusion must not be presented as a neutral methodological convenience.

---

## Overall Verdict

**Support with revisions**

The scientific question is valuable, the clinical motivation is genuine, and several design choices reflect sound ethical instincts. However, the proposal cannot be approved as submitted. It lacks a consent framework for either the retrospective training data or the prospective shadow deployment, contains no bias mitigation plan despite substantial risk, and excludes a linguistically minority patient population without ethical justification or compensatory safeguards. These are not minor refinements — they are structural gaps that must be resolved before any patient data is used.

---

## Required Changes Before Approval

- **Develop a patient consent framework for both phases.** For the retrospective training data, document whether existing broad consent provisions cover LLM-based processing and third-party transmission; if not, a waiver of consent must be formally justified and approved by the committee with explicit reasoning. For the prospective shadow mode phase, patients must be informed — through portal notification, patient information sheet, or equivalent mechanism — that their messages may be processed by an AI system, and offered the opportunity to opt out without impact on their care.

- **Provide full transparency about the third-party cloud API.** The proposal must name the provider, specify the data processing agreement (DPA) in place, confirm GDPR Article 28 compliance, clarify data retention and deletion policies, and demonstrate that pseudonymization meets the re-identification risk threshold required under GDPR for health data (Article 9).

- **Commission a pre-deployment bias audit.** Before training, the historical dataset must be analyzed for demographic and linguistic distributions and for disparities in historical triage outcomes across patient subgroups. Training labels (staff triage decisions) must be treated as potentially biased ground truth, not neutral gold standard. A subgroup analysis by age, gender, and message language must be included as a pre-specified secondary outcome of the shadow mode evaluation.

- **Establish and document a clear accountability chain.** The protocol must specify: who reviews AI recommendations before they influence workflow, what happens when AI and nurse disagree, how AI-assisted and AI-independent escalation failures are distinguished in incident reporting, and which role bears clinical and legal responsibility if an AI-flagged or AI-suppressed recommendation contributes to patient harm.

- **Address the language exclusion with a concrete equitable alternative.** The committee requires either (a) a plan to extend the system to additional languages within a defined timeline, including budget and feasibility assessment, or (b) explicit documentation that excluded-language patients receive equivalent triage response times and quality during the study period, monitored and reported as a safety outcome.

- **Add a patient-facing transparency statement.** Patients using the portal during the shadow deployment period must be informed, in plain language, that the institution is conducting research involving AI analysis of portal messages, what data is involved, and how to opt out. This must be implemented before shadow deployment begins, not after.

- **Define prospective stopping rules.** The protocol must specify conditions under which the shadow mode deployment will be paused or terminated: for example, if sensitivity for urgent cases falls below a defined threshold in any demographic subgroup, or if a serious adverse event is potentially attributable to AI triage delay.

---

## Risk Level

**High**

The patient population is among the most vulnerable in outpatient medicine. Missed escalation in oncology can result in preventable death. The training data carries substantial bias risk with no mitigation plan. Patients are currently unaware that their communications are being processed by AI and transmitted to external infrastructure. The language exclusion affects a real and identifiable patient subgroup. Each of these factors alone would justify elevated risk classification; together, they constitute a high-risk profile that requires the full set of required changes above before any research activity involving patient data may proceed.

---

## Role-Specific Comments

**On consent and the specific vulnerability of oncology patients:** Patients with cancer are not representative of the general population in their relationship to healthcare communication. Portal messages in oncology frequently contain expressions of fear, descriptions of symptoms that could signal recurrence or treatment toxicity, and requests that carry enormous emotional weight. These patients place exceptional trust in the clinical team they are writing to. The power asymmetry is profound: they are ill, dependent, and often frightened. Informed consent in this context is not a bureaucratic formality — it is a moral requirement grounded in respect for persons. A patient who would object to their message being processed by a cloud-hosted LLM has no opportunity to do so under the current proposal. That is not acceptable.

**On algorithmic bias and the laundering of historical inequity:** Large language models trained on human decisions do not merely learn clinical patterns — they learn the decision-making habits, shortcuts, and biases of the humans who generated the labels. In triage, there is substantial evidence that patients from lower socioeconomic backgrounds, older patients, and patients from ethnic minority groups are systematically under-triaged relative to clinical need. A model trained to reproduce historical triage will reproduce historical inequity. The proposal's silence on this point is not a neutral omission — it is a significant risk that requires active mitigation. I would also note that the secondary outcome of "clinician satisfaction" should not be treated as an ethical safeguard; clinicians may be satisfied with a system that saves them time even if it disadvantages certain patient groups.

**On the accountability gap:** The statement that "final decisions remain with clinicians" is necessary but not sufficient. In practice, automation bias — the well-documented tendency of humans to defer to algorithmic recommendations — means that clinician oversight may become nominal rather than substantive, particularly under cognitive load. The proposal must address how independent clinical judgment will be actively preserved, not merely formally retained. Liability frameworks must be explicit before deployment, not resolved retroactively after harm occurs.

**On shadow mode and the gradual normalization of AI triage:** I want to flag a risk that is easy to overlook: shadow mode is not ethically neutral. When clinical staff see AI recommendations alongside patient messages, even without acting on them, those recommendations shape perception. A nurse who repeatedly sees the AI label a message "routine" may — unconsciously and without any formal policy change — begin to internalize that framing. Clinical norms can shift during evaluation phases in ways that are difficult to detect and harder to reverse. The committee requires the research team to monitor for this effect and to include it explicitly in the evaluation framework.

**On the language exclusion as a matter of justice:** I wish to be precise about why this exclusion concerns me beyond operational inconvenience. If this research leads to deployment, the institution will have built its evidence base entirely on patients who speak German or English. The resulting system will be validated for those patients and not for others. This creates a durable, structural inequality in care quality that will persist long after the study concludes. The exclusion of non-German/English speakers is not a limitation to note in a discussion section — it is an ethical choice that requires justification, mitigation, and oversight.
