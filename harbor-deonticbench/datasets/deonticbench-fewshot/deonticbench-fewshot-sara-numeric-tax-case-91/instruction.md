The relevant statute is available at `/app/statute.txt`.
Example Prolog solutions for similar problems are available at `/app/examples.txt`.


**Case Facts:**
Alice got married on June 2nd, 2006. Alice files a joint return with her spouse for 2017. Alice's and her spouse's gross income for the year 2017 is $684642. They take the standard deduction in 2017.
Alice has employed Bob, Cameron, Dan, Emily, Fred and George for agricultural labor on various occasions during the year 2017:
- Jan 24: Bob, Cameron, Dan, Emily and Fred
- Feb 4: Bob, Cameron and Fred
- Mar 3: Bob, Cameron, Dan, Emily and Fred
- Mar 19: Cameron, Dan, Emily, Fred and George
- Apr 2: Bob, Cameron, Dan, Fred and George
- May 9: Cameron, Dan, Emily, Fred and George
- Oct 15: Bob, Cameron, Dan, Emily and George
- Oct 25: Bob, Emily, Fred and George
- Nov 8: Bob, Cameron, Emily, Fred and George
- Nov 22: Bob, Cameron, Dan, Emily and Fred
- Dec 1: Bob, Cameron, Dan, Emily and George
- Dec 3: Bob, Cameron, Dan, Emily and George
Alice has paid each $632 on each occasion.


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