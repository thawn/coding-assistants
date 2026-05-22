## Initial Prompt
```md
I need you to create a prompt for an agentic AI. It will be started in the repository `icml-rebuttal`.

The contents of the repository are:

* paper/
  * resources/
  * tables/
  * appendix.tex
  * contents.tex
  * master_bibliography.bib
* reviews/
  * review1.md
  * review2.md
  * review3.md
  * review4.md

Prompt the agentic AI to spawn 4 subagents, each assigned to one review. Each subagent should read both the paper and its assigned review, then create a rebuttal markdown document for that review, addressing all highlighted weaknesses and questions.

Before providing answers, each subagent should briefly summarize the review, identify what is genuinely critical or severe (independent of the authors’ subjective perspective), determine what can be answered easily, and assess how likely it is that the responses will lead to an increased reviewer score.

Then, provide responses for each weakness and question. Enumerate weaknesses as (W1), (W2), ..., and questions as (Q1), (Q2), .... Each item must include a short identifying title, for example:

* **(W1) Inclusion of Llama-4** <response/answer here>

If weaknesses or questions are not provided as a bullet-point or enumerated list, extract them from the text.

Where appropriate, provide a direct answer. If further investigation is required (e.g., experiments, literature review, verifying how many references are peer-reviewed, or evaluating the effect of ensembling), instead write:
**(W1) title** TODO: describe what needs to be checked, experimented, or researched to provide a meaningful answer.

If you cannot answer a question at all, explicitly state that.

Provide a prompt that instructs the agentic AI to spawn 4 subagents to carry out this task, one per review.

```


## Prompt created by Meta-Prompting
```md
You are working inside the repository **`icml-rebuttal`**.

## Goal

Create **4 separate rebuttal draft markdown files**, one per review, by spawning **4 subagents in parallel**.
Each subagent should take ownership of **exactly one review** and produce a structured rebuttal analysis + draft responses for that review.

---

## Repository structure

* `paper/`

  * `resources/`
  * `tables/`
  * `appendix.tex`
  * `contents.tex`
  * `master_bibliography.bib`
* `reviews/`

  * `review1.md`
  * `review2.md`
  * `review3.md`
  * `review4.md`

---

## High-level instructions

1. **Spawn 4 subagents in parallel**:

   * Subagent 1 → `reviews/review1.md`
   * Subagent 2 → `reviews/review2.md`
   * Subagent 3 → `reviews/review3.md`
   * Subagent 4 → `reviews/review4.md`

2. Each subagent must:

   * Read and understand the **paper**:

     * `paper/contents.tex`
     * `paper/appendix.tex`
     * `paper/tables/` (inspect relevant table files)
     * `paper/resources/` if needed
     * `paper/master_bibliography.bib` if needed for checking claims about references/literature
   * Read and analyze its assigned review file thoroughly.
   * Identify:

     * explicit **weaknesses**
     * explicit **questions**
     * **implicit concerns** if the reviewer did not provide clean bullet points
   * Produce a **review-specific rebuttal markdown file**.

3. Save outputs as:

   * `reviews/rebuttal_review1.md`
   * `reviews/rebuttal_review2.md`
   * `reviews/rebuttal_review3.md`
   * `reviews/rebuttal_review4.md`

4. After all 4 subagents finish, create a short master summary file:

   * `reviews/rebuttal_overview.md`
   * This should contain:

     * one-paragraph summary per reviewer
     * top critical risks across all reviews
     * recurring themes across reviewers
     * which TODOs require experiments vs. paper-text clarification vs. literature checks

---

## Important behavioral constraints

* Be **unbiased** and do **not** assume the authors are right.
* Distinguish between:
  * reviewer misunderstandings that can be clarified easily
  * legitimate serious weaknesses
  * issues that require new evidence/analysis/experiments
* Do **not** fabricate claims about the paper.
* Base every answer on what is actually in the repository.
* If something cannot be answered from the current paper text alone, explicitly mark it as a **TODO**.
* If a question requires:
  * a new experiment,
  * a literature check,
  * counting/validating references,
  * checking peer-reviewed status,
  * checking ablation results,
  * checking effect of ensembling,
  * checking whether a model/dataset/baseline was omitted,
    then **do not invent the answer**. Instead, mark it as a TODO with a concrete action.

---

## Required output format for each review file

Each file `reviews/rebuttal_reviewX.md` must follow this exact structure:

# Review X Rebuttal Draft

## 1. Review Summary

Provide a **brief neutral summary** of the review:

* what the reviewer liked
* what the reviewer criticized
* what their main concerns are
* any indication of score/confidence if present

## 2. Criticality Assessment (Unbiased)

Assess the review from a neutral program-committee perspective.

Include:

* **Severe / high-risk concerns**: issues that could materially justify rejection if unanswered
* **Moderate concerns**: valid but likely addressable
* **Minor / easily addressable concerns**: misunderstandings, missing clarifications, wording, omitted explanations, presentation issues

Be explicit and concise.

## 3. Rebuttal Potential Assessment

Estimate how likely it is that a strong rebuttal could improve the reviewer’s score.

Use a short structured format like:

* **Likelihood of score increase:** Low / Medium / High
* **Why:** 2–5 bullet points
* **Best strategy:** e.g. clarify misunderstanding, point to appendix, propose promised camera-ready fix, provide quick extra analysis, etc.

## 4. Extracted Weaknesses and Questions

Extract and normalize the reviewer’s concerns into a clean list.

Rules:

* If the reviewer already gives weaknesses/questions in bullet or numbered form, preserve them but normalize wording.
* If not, **extract them from prose**.
* Separate into:

  * **Weaknesses**
  * **Questions**
* Number them as:

  * `(W1), (W2), ...`
  * `(Q1), (Q2), ...`
* Give each item a **short identifying title/headline**

Example:

* **(W1) Missing comparison to Llama-4**
* **(W2) Unclear calibration metric choice**
* **(Q1) Why was ensembling omitted?**

## 5. Draft Responses / Action Items

For every extracted weakness/question, provide one entry in this format:

* **(W1) Short title** <direct rebuttal response if answerable from the paper>

OR

* **(W1) Short title**
  **TODO:** <specific investigation needed to answer properly>

Rules:

* If the issue is answerable from the current paper text, give a **direct draft rebuttal response**.
* If the issue requires checking the paper more carefully (e.g. appendix/table details), do that and answer if possible.
* If it requires new work (experiment, literature review, reference validation, deeper audit), mark:

  * `**TODO:** ...`
* If it cannot currently be answered at all, say so explicitly.

### Style requirements for responses

* Responses should be written as **draft rebuttal language** suitable for ICML author response.
* Be concise, precise, professional, and non-defensive.
* Avoid overclaiming.
* Where possible:

  * point to sections/tables/appendix evidence
  * suggest clarifications that can be added in rebuttal
  * suggest camera-ready commitments only if appropriate

## 6. Suggested Final Rebuttal Priorities

End with:

* Top 3 points to emphasize in the actual rebuttal to this reviewer
* Top 3 TODOs that would most improve persuasiveness
* Any dangerous concessions to avoid

---

## Detailed subagent instructions

Each subagent should follow this procedure:

1. **Read the assigned review fully**.
2. **Parse the structure of the review**:
   * summary / strengths / weaknesses / questions / score / confidence if available
3. **Read the paper files**:
   * start with `paper/contents.tex`
   * then `paper/appendix.tex`
   * inspect `paper/tables/` for any relevant quantitative evidence
   * consult `paper/master_bibliography.bib` only if the review raises literature/reference concerns
4. **Map each reviewer concern to evidence**:
   * answered in main paper
   * answered in appendix
   * partially answered
   * not answered
5. **Classify each concern**:
   * misunderstanding / clarification
   * legitimate but rebuttable
   * requires additional analysis
   * likely cannot be salvaged
6. **Draft responses conservatively**:
   * only use claims supported by repository contents
   * if unsupported, use TODO
7. **Write the output markdown file**.

---

## Quality bar

The outputs should be useful for authors preparing a real ICML rebuttal.

That means:

* clear extraction of reviewer concerns even when the review is messy
* realistic assessment of what actually matters
* honest separation of:

  * “we can answer now”
  * “we need to check”
  * “we need new evidence”
* rebuttal-ready wording, not just notes
* explicit TODOs that can be delegated immediately

---

## Final orchestration instructions

1. Spawn all 4 subagents in parallel.
2. Wait for all 4 to complete.
3. Verify that all files exist:
   * `reviews/rebuttal_review1.md`
   * `reviews/rebuttal_review2.md`
   * `reviews/rebuttal_review3.md`
   * `reviews/rebuttal_review4.md`
4. Then synthesize:
   * `reviews/rebuttal_overview.md`

### `reviews/rebuttal_overview.md` format

Include:

* one subsection per review:
  * reviewer stance
  * main risks
  * likely rebuttal leverage
* cross-review recurring themes
* highest-value global fixes to mention across multiple rebuttals
* consolidated TODO list categorized as:
  * **Experiments / analyses**
  * **Paper-text clarifications**
  * **Literature / citation checks**
  * **Appendix/table evidence to surface more clearly**

---

## Important reminder

Do **not** merely summarize the reviews.
The task is to produce **actionable rebuttal drafts** with:

* neutral review assessment
* realistic severity analysis
* estimated score-improvement potential
* extracted weaknesses/questions
* direct rebuttal responses where possible
* TODOs where more work is required

Begin now by spawning the 4 subagents.
```