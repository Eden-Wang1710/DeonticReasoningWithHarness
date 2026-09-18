The relevant statute is available at `/app/statute.txt`.


**Case Facts:**
In 2019, Alice was paid $34510. Alice has a brother, Charlie, whose son Bob lived at Alice's place in 2019, a house that she maintains. In 2019, Charlie had a different principal place of abode, and Bob had no income. Alice takes the standard deduction in 2019.


**Question:**
How much tax does Alice have to pay in 2019?

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