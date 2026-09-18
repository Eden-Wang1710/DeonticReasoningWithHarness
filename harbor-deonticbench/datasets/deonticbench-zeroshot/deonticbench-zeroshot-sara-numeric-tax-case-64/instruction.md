The relevant statute is available at `/app/statute.txt`.


**Case Facts:**
Alice has a brother, Bob, who was born January 31st, 2014. Alice's gross income in 2015 was $260932. Bob lived at Alice's house in 2015. For 2015, Alice takes the standard deduction.


**Question:**
How much tax does Alice have to pay in 2015?

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

The answer is a whole number (dollar amount, no $ sign). E.g., `Answer: 1166`

The task is complete once `swipl -q -f /app/solution.pl` runs without errors and prints the `Answer:` line.