The relevant statute is available at `/app/statute.txt`.
Example Prolog solutions for similar problems are available at `/app/examples.txt`.


**Case Facts:**
The applicant is a native and citizen of Mexico who applied to adjust status to lawful permanent resident and was found inadmissible for fraud or misrepresentation. She sought a waiver of that inadmissibility and appealed the denial of her waiver application. After the appeal, she filed a combined motion to reopen and a motion to reconsider.

In support of her motions, the applicant and her representatives submitted factual statements describing her caregiving role for her mother, who is a U.S. citizen and the applicant’s qualifying relative. The applicant lives about a block from her mother, who is 86 years old and widowed; the mother currently resides with the applicant’s brother. The applicant states that she regularly transports her mother to medical appointments and grocery shopping, cooks, cleans, and does her mother’s laundry. Four of the applicant’s sisters live farther away (about 30 minutes to six hours), and the applicant’s siblings submitted statements saying they either could not provide care if the applicant moved to Mexico or that they could not provide the same level of care because of distance and other commitments. The brother who lives with the mother said he “maybe” could provide care but that “it would not be the same for my mom because of the time” the mother and applicant spend together. The applicant also submitted a letter from her daughter reiterating that, although the grandmother lives with the brother, she feels most comfortable with the applicant’s care and that other siblings do not look after her in the same way.

In her Form I-290B statement and in a brief from her attorney, the applicant argued that the decision denying the waiver failed to consider the totality of the evidence showing that her mother’s advanced age, widowhood, and the particular close relationship and practical care the applicant provides would cause the mother extreme hardship if the applicant were required to move to Mexico. Medical documentation submitted noted the mother’s chronic conditions and medication use.


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