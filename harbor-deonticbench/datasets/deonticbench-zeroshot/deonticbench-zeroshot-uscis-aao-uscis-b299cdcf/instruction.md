The relevant statute is available at `/app/statute.txt`.


**Case Facts:**
The petitioner entered the United States in February 1994 under the Visa Waiver Program and was authorized to remain only until May 1994. U.S. Immigration and Customs Enforcement later issued an order of removal against him for overstaying his VWP admission.

In 2018 the petitioner’s adult child filed a Form I-130 petition on his behalf; that petition was approved in 2019. Also in 2018 the petitioner submitted a Form I-485 application to adjust status based on the I-130; that I-485 was denied in 2019. In 2020 the petitioner filed a Form I-212 (Application for Permission to Reapply for Admission) and a second Form I-485; the field office director denied both applications.

On appeal the petitioner contends his Form I-212 should be granted. He argues he is deserving of a favorable exercise of discretion, cites a USCIS policy memorandum concerning adjustment eligibility for Visa Waiver Program entrants, and states that he would experience “extreme hardship” if he were forced to leave the United States. These contentions and the cited memorandum form the basis of his appeal.


**Question:**
Should this case be accepted or dismissed?

Write a complete, runnable SWI-Prolog program at `/app/solution.pl` that:
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