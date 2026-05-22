# Scientific Review

## Role and Motivation

I am Dr. Elena Hartmann, Principal Investigator and Senior Researcher in Biomedical Informatics at a major academic medical center. My work over the past two decades has centred on clinical natural language processing and AI-assisted decision support, and I have reviewed dozens of proposals seeking to bring large language model technology into high-stakes clinical workflows. My evaluation is driven by a single conviction: healthcare AI that is not grounded in rigorous, reproducible science is not merely unhelpful — it is dangerous. I approach this proposal with that standard in mind. Oncology patients are a particularly vulnerable population; a missed urgent message can be the difference between a salvageable complication and an irreversible one. The bar for deploying any automated triage assistant in this setting must therefore be exceptionally high.

---

## Top 3 Strengths

**1. Prospective shadow-mode validation design.**
The decision to deploy in shadow mode for three months before any operational integration is scientifically sound and ethically responsible. Shadow-mode evaluation allows the team to accumulate a prospective, temporally separated test set that is free from the retrospective data artefacts (e.g., label leakage from outcome-informed annotation) that plague so many clinical AI studies. This design also preserves clinical safety during the evaluation period, since human triage decisions remain authoritative throughout.

**2. Clinically anchored primary outcome.**
Choosing sensitivity for detecting urgent cases as the primary outcome reflects genuine clinical thinking. In a triage context, false negatives — urgent messages classified as routine — carry far greater harm than false positives. Anchoring the primary endpoint on sensitivity rather than overall accuracy or F1-score alone demonstrates that the investigators understand the asymmetric cost structure of clinical triage errors. This is more sophisticated than many proposals I have reviewed.

**3. Substantial historical dataset with linked outcomes.**
Approximately 80,000 messages linked to actual staff triage outcomes provides a credible foundation for model development. The availability of ground-truth labels derived from real clinical workflow decisions (rather than post-hoc annotations by researchers) is a meaningful scientific strength. It reduces the annotation subjectivity that commonly undermines training label quality in clinical NLP projects.

---

## Top 3 Concerns

**1. Absence of statistical power justification and undefined decision thresholds.**
The proposal states sensitivity as the primary outcome but provides no sample size calculation, no minimum clinically meaningful sensitivity threshold, and no pre-specified operating point on the ROC curve. Without these, the three-month shadow-mode period is an arbitrary duration rather than a powered study. How many urgent messages are expected during shadow mode? What is the baseline prevalence of urgent cases in the portal stream? If urgency prevalence is, say, 5%, a three-month window may yield far too few true-positive events to estimate sensitivity with acceptable precision. The proposal must include a formal power calculation specifying: (a) expected urgency prevalence, (b) minimum acceptable sensitivity with its confidence interval width, (c) required sample size, and (d) the decision threshold at which the model will be evaluated. Without these, the shadow-mode results will be uninterpretable regardless of what they show.

**2. Label quality, class definition ambiguity, and potential data leakage.**
The three urgency categories — routine, clinician review within 24 hours, immediate escalation — are not operationally defined in the proposal. Historical staff triage outcomes are used as ground truth, but nurse triage decisions are known to be inconsistent across shifts, experience levels, and message load. There is no mention of inter-annotator agreement assessment, adjudication protocols for borderline cases, or validation of the historical labels against downstream clinical events (e.g., did messages labelled "immediate escalation" actually result in urgent clinical action?). Furthermore, if the historical labels were recorded in the same EHR system from which contextual patient data may have been accessible to triaging nurses, there is a serious risk that the training labels encode information not available at triage time — a form of outcome-informed label contamination. The proposal must rigorously characterise label reliability and demonstrate that training labels are free from leakage of post-triage clinical information.

**3. External validity, distributional shift, and evaluation against inadequate baselines.**
The proposal evaluates model performance against nurse triage decisions during shadow mode — but if nurse decisions are themselves the training labels, this comparison conflates the reference standard with the evaluation criterion and risks circular validation. Beyond this circularity, there is no mention of: (a) temporal validation (is the model tested on messages from a time window entirely held out from training?), (b) comparison against a meaningful clinical baseline (e.g., a structured rule-based triage protocol, or keyword-alert systems currently in use), or (c) subgroup analyses by disease type, treatment phase, patient demographics, or message complexity. The exclusion of non-German/non-English messages is noted but not justified scientifically — this creates a known coverage gap with no characterisation of how large or clinically significant that excluded population is. A proposal for a system intended to reduce harm in oncology care must demonstrate that it does not systematically disadvantage identifiable patient subgroups.

---

## Overall Verdict

**Support with revisions**

The proposal addresses a genuine clinical need and shows methodological awareness in several respects. However, it cannot be approved in its current form. The absence of a statistical power analysis renders the evaluation plan scientifically uninterpretable. The label quality and potential leakage issues threaten the validity of both training and evaluation. The baseline comparison strategy is insufficient. These are not minor gaps; they are fundamental scientific requirements. Substantial revision is necessary before this work can produce findings that the field — or clinical decision-makers — can trust.

---

## Required Changes Before Approval

- **Power calculation**: Provide a formal sample size and power justification for the shadow-mode evaluation, specifying urgency prevalence assumptions, target sensitivity, acceptable 95% CI width, and minimum required number of urgent-case events.
- **Pre-specified decision threshold**: Define and justify the model operating point (sensitivity/specificity trade-off) that will be used for all primary outcome analyses, registered before shadow-mode data collection begins.
- **Operationalise urgency categories**: Provide explicit, clinician-consensus-derived definitions for each of the three triage classes, including examples and exclusion criteria, adjudicated by at least two senior clinicians.
- **Inter-rater reliability assessment**: Report inter-annotator agreement (Cohen's κ or equivalent) on a representative sample of historical labels; establish an adjudication protocol for disagreements.
- **Label leakage audit**: Document what information was available to nurses at the time of triage and demonstrate that training labels do not encode post-triage clinical outcomes or retrospectively available patient data.
- **Temporal train/validation/test split**: Ensure the test set is drawn exclusively from a time window after the training period ends; document the split dates explicitly.
- **Meaningful clinical baseline**: Include at minimum one non-LLM comparator — a rule-based keyword triage system, the current manual workflow benchmark, or both — to contextualise model performance.
- **Subgroup analyses plan**: Pre-specify subgroup analyses by cancer type, treatment phase, patient age, and any sociodemographic variables available, with appropriate multiple comparisons adjustment.
- **Characterise excluded language population**: Report the volume and urgency profile of messages in languages other than German and English; discuss the equity implications of their exclusion.
- **Third-party cloud transmission risk assessment**: Provide a detailed data governance analysis — including re-identification risk under pseudonymisation — for cloud-hosted inference; confirm compliance with applicable data protection regulations (GDPR in particular, given the German-language inclusion).
- **Protocol pre-registration**: Register the full evaluation protocol (hypotheses, outcomes, thresholds, analysis plan) on a recognised clinical trial or study registry before shadow-mode deployment begins.

---

## Risk Level

**High**

**Justification**: The patient population is oncology outpatients — a group with high symptom burden, time-sensitive complications (febrile neutropenia, bleeding, thromboembolic events), and significant vulnerability. A false-negative triage error in this population can directly result in patient harm or death. The current proposal lacks the statistical rigour to reliably characterise the system's error rate; it transmits sensitive patient data to a third-party cloud infrastructure with only pseudonymisation as protection; and it has not demonstrated superiority — or even non-inferiority — to existing triage practice. Until these gaps are addressed, the scientific and patient-safety risk of proceeding is high.

---

## Role-Specific Comments

**On LLM calibration and rationale quality**: The proposal mentions that the model will provide a "rationale" for its routing recommendation. In a clinical context, a plausible-sounding but incorrect rationale may increase clinician automation bias — staff may defer to a confidently stated wrong recommendation. The proposal must include an evaluation of rationale quality and a study of how staff interact with model explanations during shadow mode (e.g., do nurses override the model more or less when a rationale is provided?). This is not a secondary consideration; it directly affects patient safety.

**On fine-tuning versus prompting**: The proposal offers "fine-tune or prompt an LLM" as alternatives without committing to a design. These are substantively different methodologies with different failure modes, reproducibility properties, and regulatory implications. The final protocol must specify the approach, the base model, the versioning strategy, and how model updates will be managed over time. A fine-tuned model evaluated at one checkpoint may perform differently after subsequent updates to the base model.

**On concept drift and post-deployment monitoring**: Shadow mode captures a three-month window, but oncology portal communication patterns shift with treatment guidelines, seasonal illness burden, and institutional workflows. The proposal has no plan for post-deployment performance monitoring, drift detection, or model retraining governance. For a system intended for sustained operational use, this is a significant scientific and safety omission.

**On the agreement metric as secondary outcome**: "Agreement with human triage" as a secondary outcome is circular if human triage decisions also constitute the training labels and the shadow-mode reference standard. The investigators should instead use agreement with an independent clinical adjudication panel as the reference, at least for a representative subsample, to break this circularity.

**On clinician satisfaction as an outcome**: Satisfaction is a legitimate secondary outcome, but the measurement instrument must be pre-specified and validated. An ad hoc post-deployment survey will not produce data of sufficient scientific quality to support publication or policy decisions. I recommend adopting or adapting a validated instrument (e.g., the System Usability Scale or a domain-specific variant) and registering it alongside the primary outcome.
