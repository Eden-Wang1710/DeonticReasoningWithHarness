The relevant statute is available at `/app/statute.txt`.
Example Prolog solutions for similar problems are available at `/app/examples.txt`.


**Case Facts:**
In 2017, Alice earned $133200. Bob's income in 2017 was $44311. Alice and Bob have been married since Feb 3rd, 2017. Alice has been blind since Feb 28, 2014. Alice has paid $4525 to Charlie for work done in the year 2017. In 2017, Alice has also paid $983 into a retirement fund for Charlie, and $5322 into health insurance for Charlie, both under a plan. Alice and Bob file jointly and take the standard deduction.


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