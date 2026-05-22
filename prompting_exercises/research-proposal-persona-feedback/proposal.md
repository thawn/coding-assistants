**Project title:** AI-assisted triage of patient portal messages in outpatient oncology  
**Objective:** Develop and evaluate a large language model-based system that classifies incoming patient messages into urgency categories (routine, clinician review within 24h, immediate escalation) and drafts suggested routing recommendations for clinical staff.  
**Data:** Historical de-identified patient portal messages from the oncology department (approx. 80,000 messages) linked to eventual staff triage outcomes.  
**Methods:** Fine-tune or prompt an LLM to classify messages and provide rationale. Prospectively deploy in shadow mode for 3 months, comparing model recommendations to nurse triage decisions.  
**Primary outcome:** Sensitivity for detecting urgent cases.  
**Secondary outcomes:** Time saved for staff, agreement with human triage, clinician satisfaction.  
**Deployment plan:** Cloud-hosted inference via third-party API; all messages pseudonymized before transmission.  
**Patient group:** Adult oncology outpatients using the hospital portal.  
**Exclusions:** Messages in languages other than German or English.  
**Human oversight:** Final decisions remain with clinicians.  
**Potential benefit:** Reduced triage burden and faster response to urgent messages.