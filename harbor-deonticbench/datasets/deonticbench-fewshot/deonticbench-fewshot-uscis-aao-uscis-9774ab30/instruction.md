The relevant statute is available at `/app/statute.txt`.
Example Prolog solutions for similar problems are available at `/app/examples.txt`.


**Case Facts:**
The petitioner is a native of Afghanistan who, in 2022 at age 17, obtained an Order of Special Immigrant Juvenile Status (SIJ Order) from an Illinois juvenile court. The juvenile court order declared him dependent on the court, appointed his brother as his guardian, found that reunification with his father was not viable because of abandonment under Illinois law, and determined it was not in his best interest to return to Afghanistan and that he should remain in the United States.

In support of the juvenile court findings, the petitioner filed a Verified Motion for SIJ Legal Findings describing the factual circumstances. The Motion states that the petitioner's father is deceased, that the petitioner has been in his brother’s care and custody since the father’s death (including during their evacuation from Afghanistan and entry to the United States), and that he fears persecution by the Taliban if he returns to Afghanistan. The record includes a copy of the petitioner's father's death certificate.

The petitioner filed a Form I-360 (SIJ petition) in December 2022. The National Benefits Center director denied the petition, stating the record did not show a factual basis for the juvenile court’s determination of parental non-reunification on the ground of abandonment given that the father is deceased, and noting that the petitioner had not provided sufficient documentation to establish a reasonable factual basis for the juvenile court’s determinations.

On appeal, the petitioner submitted a brief reaffirming his eligibility and argued that the juvenile court’s SIJ Order and the Motion for SIJ Order supply the factual basis for the court’s parental reunification and best-interest determinations. He emphasized that the guardianship was sought to protect him from abandonment and to allow his brother to act as guardian because he lacks a father to provide for him.


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