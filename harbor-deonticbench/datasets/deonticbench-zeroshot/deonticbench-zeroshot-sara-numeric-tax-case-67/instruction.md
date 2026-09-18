The relevant statute is available at `/app/statute.txt`.


**Case Facts:**
Alice got married on Dec 10th, 2009. Alice's gross income for the year 2016 is $554313. Alice files separately and takes the standard deduction. Her husband's gross income in 2016 is $56298 and he takes itemized deductions of $4421.


**Question:**
How much tax does Alice have to pay in 2016?

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