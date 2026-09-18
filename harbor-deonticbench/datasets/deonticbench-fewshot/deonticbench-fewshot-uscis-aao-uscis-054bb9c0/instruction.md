The relevant statute is available at `/app/statute.txt`.
Example Prolog solutions for similar problems are available at `/app/examples.txt`.


**Case Facts:**
The petitioner is a foreign-born youth who, in 2022 at age 17, obtained a Family Division custody order from the Fifteenth Judicial Circuit Court in Florida awarding legal and physical custody to his uncle. The custody petition and court findings state that the petitioner had lived with his uncle for four years at the time the custody petition was filed and that the uncle was providing full-time care. The court found the petitioner was within its jurisdiction and that reunification with his parents was not viable due to neglect: the petitioner began working at about age ten so he could eat, his parents were unable to provide necessary care for his development and education, his parents failed to provide proper food, and his father brought him to the United States at age 12 and abandoned him nine months later. The petitioner used this custody order as the basis for filing a Form I-360 (SIJ petition) in November 2022.

The National Benefits Center director denied the SIJ petition, stating that the custody order did not explain why it would not be in the petitioner’s best interest to be returned to Guatemala and that the record lacked the factual basis for a best-interest determination to show the petition was bona fide. The petitioner appealed that denial and submitted a brief asserting his eligibility for Special Immigrant Juvenile status.


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