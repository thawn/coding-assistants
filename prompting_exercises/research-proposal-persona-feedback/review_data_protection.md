# Data Protection Review

## Role and Motivation

I am Ingrid Schneider, Data Protection and Compliance Officer at this institution, holding a law degree and twelve years of practical experience in healthcare data governance. My mandate is to ensure that all research and clinical projects involving personal data comply with the General Data Protection Regulation (GDPR), the German Federal Data Protection Act (BDSG), the EU AI Act, and the applicable sectoral laws governing hospital data (including Landeskrankenhausgesetz provisions and the relevant state hospital act). I have personally led data breach investigations and am acutely aware of how re-identification can occur even after superficial anonymization steps — particularly in small or diagnostically homogeneous cohorts such as outpatient oncology populations.

My evaluation of this proposal is driven by a foundational conviction: patient portal messages from oncology patients are among the most sensitive categories of personal data imaginable. They combine health status (Art. 9 GDPR special category data), psychosocial content, treatment details, and often highly intimate disclosures made in a moment of vulnerability. Routing this data through a third-party cloud-hosted Large Language Model (LLM) inference API is not a routine technical decision — it is a decision with profound legal, ethical, and liability consequences that the proposal, as currently written, does not adequately address.

---

## Top 3 Strengths

**1. Human Oversight Is Explicitly Retained**
The proposal clearly states that final triage decisions remain with clinicians. This is not a trivial safeguard. Under the EU AI Act, high-risk AI systems used in healthcare (Annex III) must incorporate human oversight mechanisms. By committing to a "shadow mode" deployment in which the model's output is advisory only, the project avoids the most dangerous scenario of fully automated decision-making affecting patient safety. This design also mitigates the strictest application of GDPR Art. 22 (prohibition on solely automated decisions with significant effects), though this protection is conditional on the shadow mode discipline being enforced in practice and documented rigorously.

**2. Prospective Validation Before Clinical Integration**
The three-month shadow-mode evaluation against real nurse triage decisions is methodologically sound and demonstrates that the team intends to validate performance before any operational reliance. This staged approach allows the institution to identify systematic failure modes — particularly false negatives on urgent escalation cases — before patients are harmed. From a compliance standpoint, this phased approach also creates a window in which data protection controls can be refined before broader deployment, and it is consistent with the principle of data protection by design and by default (GDPR Art. 25).

**3. Defined Patient Population and Scope Limitation**
The proposal restricts the study to adult outpatient oncology portal users and explicitly excludes messages in languages other than German or English. While this language exclusion raises its own equity concerns (outside my direct remit), from a data governance perspective it does reduce the scope of data processing to a more auditable and bounded dataset. The relatively well-defined cohort — adults, single department, single channel — means that data lineage, retention scope, and subject rights obligations can in principle be mapped to a finite, traceable population rather than a diffuse or ambiguous one.

---

## Top 3 Concerns

**1. "Pseudonymization" Is Asserted, Not Specified — and May Be Legally Insufficient**
The proposal states that "all messages pseudonymized before transmission" to the cloud API. This single sentence is the entire technical and legal basis offered for protecting the identity of patients whose most intimate health communications are being sent to a third party. This is wholly inadequate.

Patient portal messages in oncology are not generic texts. They routinely contain: the patient's name or initials (written by the patient themselves), references to treating physicians by name, specific medication regimens, surgery dates, named family members, rare disease subtypes, and geographic references. Removing a patient ID field — the most basic form of "pseudonymization" — does not render these messages non-identifiable. Under GDPR Recital 26, data is personal if re-identification is *reasonably possible*, not merely theoretically conceivable. In a population of, say, 200 active oncology outpatients with a rare tumor type, a message describing "my third cycle of pembrolizumab after the resection last March" is effectively identifiable without any identifier field at all.

Furthermore, GDPR Art. 4(5) defines pseudonymization as a process that *reduces* re-identification risk but does not eliminate it — pseudonymized data remains personal data. Therefore, the legal basis requirements of Art. 6 and Art. 9 continue to apply in full. The proposal must specify: (a) the exact pseudonymization algorithm applied; (b) what categories of quasi-identifiers are detected and removed or replaced (NER, pattern matching, custom rules); (c) how free-text clinical content is handled; (d) who performs the pseudonymization and at what stage; and (e) what residual re-identification risk has been assessed.

**2. Third-Party Cloud API: Data Controller/Processor Relationship Is Undefined and the Legal Basis for Art. 9 Processing Is Absent**
The proposal intends to transmit patient health data to a third-party cloud-hosted LLM inference API. This creates an immediate and serious compliance problem on two fronts.

First, the third-party API provider is a *data processor* under GDPR Art. 28. This means a legally binding Data Processing Agreement (DPA) must be in place before any data is transmitted. The DPA must specify: the subject matter and duration of processing, the nature and purpose of processing, the type of personal data and categories of data subjects, the obligations and rights of the controller (the hospital), and the processor's sub-processor chain. Many commercial LLM API providers operate under terms of service that reserve the right to use submitted data for model improvement, logging, abuse detection, or other purposes — all of which would constitute unauthorized secondary processing of Art. 9 health data. The identity of the API provider is not named in the proposal, which makes any legal assessment impossible at this stage.

Second, and more fundamentally: what is the legal basis under GDPR Art. 9(2) for processing special category health data? The proposal does not state one. The most plausible candidates are Art. 9(2)(j) — processing for scientific research purposes with appropriate safeguards under Union or Member State law — or Art. 9(2)(h) — processing for healthcare purposes. For Art. 9(2)(j) to apply, the processing must be genuinely necessary for the research objective and accompanied by appropriate safeguards such as pseudonymization and data minimization. Merely labeling data as "pseudonymized" does not satisfy this requirement. For Art. 9(2)(h), the processing must be carried out by a health professional subject to professional secrecy or by another person subject to an equivalent obligation of secrecy — a commercial LLM API provider almost certainly does not meet this standard. This is a blocking compliance gap.

**3. LLM Memorization, Inference Risk, and the Absence of a DPIA**
The proposal involves fine-tuning an LLM on 80,000 historical patient portal messages. This creates a category of risk that is not addressed anywhere in the document: the risk that the trained or fine-tuned model *memorizes* training data and can reproduce it — either verbatim or through targeted inference. This is not a theoretical concern. Empirical research has demonstrated that LLMs can reproduce training examples when prompted appropriately, and that even partial memorization can allow reconstruction of individual records. If the fine-tuned model is subsequently shared, published, or deployed more broadly, patient data embedded in model weights could be exposed.

Additionally, the prospective shadow-mode deployment will involve real-time transmission of *current* patient messages — not historical data — to the cloud API. These messages have not undergone the same retrospective de-identification workflow described for the training set. The proposal does not describe any real-time pseudonymization pipeline, its latency, its error rate, or how failures are detected and handled.

Finally, and critically: GDPR Art. 35(1) mandates a Data Protection Impact Assessment (DPIA) for processing likely to result in a high risk to the rights and freedoms of natural persons. Art. 35(3)(b) specifically requires a DPIA for large-scale processing of special category data. Art. 35(3)(a) requires a DPIA for systematic evaluation of personal aspects including profiling. This project — fine-tuning an LLM on 80,000 oncology patient messages, deploying it via third-party API for real-time classification and routing — plainly satisfies all three criteria. There is no mention of a DPIA in the proposal. This omission is not a procedural oversight; it is a legal requirement. Without a completed and approved DPIA, this project cannot proceed.

---

## Overall Verdict

**Major Concerns**

This proposal cannot be approved in its current form. It lacks a specified legal basis for processing Art. 9 health data, does not identify the third-party data processor or confirm a compliant DPA exists, offers no technically specified pseudonymization methodology, and has not conducted the mandatory DPIA under GDPR Art. 35. The scientific objective is legitimate and the clinical motivation is sound, but the data protection and legal infrastructure required to support this work is almost entirely absent from the proposal. The required changes below must be addressed in full before any data processing begins — including any preparatory access to the historical message dataset.

---

## Required Changes Before Approval

- **Conduct and submit a full DPIA** (GDPR Art. 35) covering both the retrospective training phase and the prospective shadow deployment, including likelihood and severity of risks to data subjects, mitigating measures, and residual risk assessment. The DPIA must be approved by this office before data access is granted.

- **Name the third-party LLM API provider** and submit a draft Data Processing Agreement (Art. 28 GDPR) for legal review. The DPA must explicitly prohibit the provider from using submitted data for model training, logging beyond operational necessity, or any purpose other than returning inference results. Sub-processor chains must be disclosed in full.

- **Provide a technically detailed pseudonymization specification**: name the NER system, regex/pattern rules, or other mechanisms used; specify which quasi-identifier categories are targeted (names, dates, drug names combined with rare diagnosis, physician names, geographic references); provide a sample re-identification risk assessment for the oncology cohort; and describe how pseudonymization failures are detected and handled at runtime.

- **Establish and document the Art. 9(2) legal basis** for both the training and deployment phases. If relying on Art. 9(2)(j) (scientific research), provide the specific Union or Member State legal provision invoked and demonstrate that pseudonymization and data minimization requirements are met. If relying on another basis, provide legal justification with reference to applicable law.

- **Assess and document LLM memorization risk** for any fine-tuned model: include a plan for membership inference testing, describe access controls on the fine-tuned model weights, and specify whether the model will be retained, published, or transferred after the project.

- **Describe the real-time pseudonymization pipeline** for the prospective shadow deployment phase: architecture, latency, error handling, audit logging, and fallback behavior when pseudonymization cannot be confirmed before transmission.

- **Define data retention and deletion policies** for: the historical training dataset, the fine-tuned model weights, the prospective shadow-mode message logs, API request/response logs held by the third-party provider, and any derived outputs (e.g., urgency classifications linked to patient encounters).

- **Implement and document audit logging and access controls** for all personnel and systems that can access the training data, the model, and the shadow-mode outputs. Access should be on a need-to-know basis with role-based authorization and tamper-evident logs.

- **Address data subject rights** (GDPR Art. 15–22): specify how patients whose historical messages are used in training can exercise rights of access, erasure, or objection; describe how objection to processing would be operationalized post-hoc (e.g., re-training without affected records); and ensure the patient information notice (Datenschutzhinweis) is updated to cover AI-assisted triage processing.

- **Specify whether EU data residency is guaranteed** for the cloud API. If data will be transferred outside the EEU, a legal transfer mechanism under GDPR Chapter V (SCCs, adequacy decision) must be in place and documented before transmission.

- **Address EU AI Act classification**: confirm whether the system is classified as a high-risk AI system under Annex III (AI systems used in safety components of healthcare); if so, document the conformity assessment obligations, logging requirements, and transparency obligations that must be met prior to deployment.

---

## Risk Level

**High**

The combination of the following factors places this project in the highest risk category:

1. **Special category data at scale** — 80,000 oncology patient portal messages, supplemented by real-time message streams, constitute large-scale processing of Art. 9 health data in one of the most sensitive clinical contexts.
2. **Third-party cloud processing** — transmission of health data to an unspecified commercial API provider with unverified data governance practices represents an uncontrolled data export.
3. **LLM-specific risks** — fine-tuning on identifiable patient text introduces memorization risk that is absent from conventional statistical models; this risk persists in the model weights after training concludes.
4. **Re-identification risk in small cohorts** — oncology outpatient populations are often small, diagnostically specific, and self-descriptive in their portal communications, making pseudonymization technically difficult to achieve robustly.
5. **Absence of DPIA** — the single most important procedural safeguard required by law for this type of processing has not been initiated.
6. **Unclear legal basis** — without a documented Art. 9(2) basis, every act of processing is potentially unlawful from the moment data is first accessed.

Until the required changes are addressed, no data access, API integration, or model training activity should proceed.

---

## Role-Specific Comments

**On BDSG Sec. 22 and sectoral research law:** Under BDSG § 22(1)(b), processing of special category data for scientific research is permissible if it serves a legitimate public interest, the research cannot reasonably be conducted with anonymized data, and appropriate safeguards are in place. The proposal does not demonstrate that anonymization is technically infeasible (which, given the nature of the data, may be true — but must be argued explicitly). Additionally, the relevant state hospital act (Landeskrankenhausgesetz) may impose additional restrictions on secondary use of patient data for research purposes that go beyond GDPR; these must be reviewed by legal counsel before the project proceeds.

**On the concept of "de-identified" versus "pseudonymized" versus "anonymized":** The proposal uses the term "de-identified" in section 3 and "pseudonymized" in section 7. These are not synonymous, and neither is equivalent to anonymized. Under EU law, only truly anonymized data — where re-identification is no longer reasonably possible by any party — falls outside the scope of GDPR entirely. The proposal should clarify which legal status is claimed for the processed data, provide the technical and statistical basis for that claim, and acknowledge that the institution remains the data controller for pseudonymized data regardless of what steps are taken before transmission.

**On purpose limitation (GDPR Art. 5(1)(b)):** The stated purpose is triage classification and routing recommendation. Any secondary use of the model outputs, the training data, or the shadow-mode logs — including publication of example messages, model probing, or benchmarking against other datasets — would constitute new processing requiring a fresh legal basis and, likely, a DPIA amendment. This must be explicitly prohibited in the project protocol and the DPA.

**On consent as a legal basis:** I anticipate that some colleagues may suggest obtaining patient consent (Art. 6(1)(a) / Art. 9(2)(a)) as the solution to the legal basis problem for retrospective processing of 80,000 historical messages. I strongly advise against this approach for the historical dataset: consent obtained retrospectively from patients already in an oncology care relationship is unlikely to be freely given within the meaning of GDPR Recital 43, given the inherent power imbalance. Furthermore, retrospective consent from 80,000 patients is operationally implausible. The research exemption under Art. 9(2)(j) with robust safeguards is the appropriate pathway — but it must be properly documented and implemented.

**On the EU AI Act high-risk classification:** AI systems used in healthcare decision support — particularly those affecting triage and escalation decisions — are strong candidates for classification as high-risk systems under Annex III of the EU AI Act. If this system is so classified, the institution as deployer (and potentially as developer, depending on whether fine-tuning constitutes substantial modification) must comply with obligations including: registration in the EU database for high-risk AI systems, technical documentation, conformity assessment, logging of system operation, transparency toward patients, and human oversight measures. The compliance roadmap for the EU AI Act obligations should be developed in parallel with the DPIA, not deferred until deployment.

**On data subject notification:** Patients who are actively using the portal during the shadow deployment phase will have their messages processed by an AI system. Even if human oversight is retained, this constitutes automated processing of their health data by a new system they have not been informed about. GDPR Art. 13/14 transparency obligations require that the hospital's privacy notice be updated to disclose this processing before the shadow deployment begins. Failure to do so is an independent GDPR violation regardless of whether any other requirement is met.
