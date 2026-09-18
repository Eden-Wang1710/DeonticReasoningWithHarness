The relevant statute is available at `/app/statute.txt`.
Example Prolog solutions for similar problems are available at `/app/examples.txt`.


**Case Facts:**
The Obligor had posted an ICE Form I-352 immigration delivery bond as security for a bonded foreign national. ICE declared the bond breached after the bonded foreign national was not produced in response to a written request, and the Obligor appealed, seeking reinstatement of the delivery bond.

On appeal, the Obligor explained that it could not produce the bonded foreign national because the initial Form I-862 (Notice to Appear) that prompted the foreign national’s immigration proceedings did not include a time or place for the hearing. The Obligor stated that it was not made aware of any court date and that the government’s failure to provide such notice prevented production of the alien. The Obligor also argued, citing Pereira v. Sessions, that the NTA was invalid, which they said prejudiced their ability to deliver the bonded foreign national, meant removal proceedings never actually commenced, and therefore negated any substantial violation of the bond’s terms.


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