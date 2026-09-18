The relevant statute is available at `/app/statute.txt`.
Example Prolog solutions for similar problems are available at `/app/examples.txt`.


**Case Facts:**
Alice and Harold got married on Sep 3rd, 1992. Harold and Alice have a son, born Jan 25th, 2000. Harold died on Feb 28th, 2016. They had been living in the same house since 1993, maintained by Alice. Alice and her son continued doing so after Harold's death. Alice's gross income for the year 2017 was $236422. Alice has employed Bob, Cameron, Dan, Emily, Fred and George for agricultural labor from Sep 9th to Oct 1st 2017, and paid them $5012 each. Alice takes the standard deduction in 2017.


**Question:**
How much tax does Alice have to pay in 2017?

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

The answer is a whole number (dollar amount, no $ sign). E.g., `Answer: 1166`

The task is complete once `swipl -q -f /app/solution.pl` runs without errors and prints the `Answer:` line.