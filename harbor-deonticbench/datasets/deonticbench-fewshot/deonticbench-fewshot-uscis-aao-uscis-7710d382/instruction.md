The relevant statute is available at `/app/statute.txt`.
Example Prolog solutions for similar problems are available at `/app/examples.txt`.


**Case Facts:**
The petitioner filed Form I-360 in October 2020, asserting that he was an abused parent of his U.S. citizen daughter, S‑R‑C. In his initial and subsequent personal statements he described a long pattern of his daughter's disrespectful and hurtful conduct beginning in high school: she became distant, moved out at age 16 and blocked contact, frequently reminded him that he was undocumented while she was a U.S. citizen, mocked his English and appearance, laughed at him and tried to denigrate him, and frequently threatened to remove herself and her children from his life. He said this conduct has significantly affected his mental health and self‑confidence. He also stated that if he or his wife decline requests to babysit her children she responds with the silent treatment and threatens to withhold access to the grandchildren. The petitioner reported that his daughter was given a credit card in his name, which she charged to the maximum and left unpaid for seven months without informing him. He provided medical records showing a diagnosis of epilepsy and said his doctor advised him to avoid strong emotions or arguments that could trigger seizures; he stated his daughter is aware of his condition but is inconsiderate or dismissive. Third‑party letters from his nephew and another child described similar conduct by the daughter continuing into her early and mid‑20s and noted the emotional toll on the family. After the initial denial, the petitioner filed motions to reopen and reconsider and supplemented the record with a brief, an additional personal statement, third‑party attestations, medical records, and a credit card statement; those motions were dismissed, and he then submitted an appeal brief.

The petitioner is appealing because he contends the prior decision was incorrect and that the evidence he submitted shows he was subjected to extreme cruelty by his daughter; he seeks review of that determination.


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