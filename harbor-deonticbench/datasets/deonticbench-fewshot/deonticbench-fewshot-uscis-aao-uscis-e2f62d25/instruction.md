The relevant statute is available at `/app/statute.txt`.
Example Prolog solutions for similar problems are available at `/app/examples.txt`.


**Case Facts:**
This matter concerns an appeal from a Texas Service Center decision in USCIS case number 25674629. The Petitioner is a physician-researcher in urologic oncology who seeks employment-based second preference immigrant classification and a national interest waiver of the job-offer requirement. The Director denied the petition, and the matter is before the Administrative Appeals Office on appeal. On appeal, the Petitioner submitted additional evidence and a brief asserting eligibility for a national interest waiver. He stated that he will continue providing clinical care to cancer patients, conduct research, lead clinical trials, work to reduce healthcare costs, and develop innovative surgical approaches to improve care for patients with cancer. In support, he submitted materials from the American Cancer Society and the National Cancer Institute concerning urologic cancers and the economic burdens of cancer care, along with expert letters discussing the implications of his research for patient treatment and recovery. The record also includes his curriculum vitae, academic records, two published articles, evidence of peer review activity, articles citing his research findings, and letters of endorsement from experts in senior academic and medical positions describing his research accomplishments, including development of surgical techniques that significantly affect patient recovery and have been used by medical centers in the United States and abroad. The record further contains evidence described as showing that he is a research physician with influential published research and surgical techniques and treatment methods adopted by others, as well as evidence described as showing broader economic and public-health benefits associated with progress in improving treatment methods for cancer and other urologic disorders.


**Question:**
Should this case be accepted or dismissed?

Review the examples in `/app/examples.txt` to understand the expected Prolog structure,
then write a complete, runnable SWI-Prolog program at `/app/solution.pl` that:
1. Encodes the relevant rules from the statute as Prolog clauses
2. Encodes the case facts as Prolog facts
3. Derives the answer to the question
4. Prints the answer on a single line in exactly this format: `Answer: <value>`
5. Calls `:- halt.`

**Use `swipl` to verify your program as you go:**
```
swipl -q -f /app/solution.pl
```
Check the output for syntax errors or warnings. If any errors appear, fix them and re-run until the program executes cleanly and prints the expected `Answer:` line.

The answer is exactly "Accepted" or "Dismissed". E.g., `Answer: Accepted`

The task is complete once `swipl -q -f /app/solution.pl` runs without errors and prints the `Answer:` line.