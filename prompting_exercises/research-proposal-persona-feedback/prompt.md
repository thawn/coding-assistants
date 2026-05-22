**Task:**  
You are coordinating a multi-stakeholder review of a life sciences research proposal.

You will:

1. Read the proposal in `proposal.md`
2. Create 5 reviewer subagents. For each of the subagents, create a comprehensive detailed role prompt, detailing motivation and what is important to them. The individual roles are detailed in `stakeholders.md`.
3. Each reviewer must assume the role and independently evaluate the proposal from their assigned perspective
4. Each reviewer must write a markdown review file:  
   * `review_scientific.md`  
   * `review_clinical.md`  
   * `review_data_protection.md`  
   * `review_ethics.md`  
   * `review_patient_advocate.md`
5. After all review files are complete, read all 5 files and create `summary.md`

**Instructions for each reviewer:**  
Use the following structure for the review:

* Own Role and motivation
* Top 3 strengths
* Top 3 concerns
* Overall verdict (Support / Support with revisions / Major concerns)
* Required changes before approval
* Risk level (Low / Medium / High)
* Role-specific comments

**Instructions for final summary:**  
Summarize:

* points most stakeholders support
* points of strongest concern
* stakeholder-specific concerns
* disagreements between stakeholders
* top 5 recommended revisions
* final overall recommendation