The relevant statute is available at `/app/statute.txt`.


**Case Facts:**
Alice's father, Bob, was paid $3200 in 2017 for services performed for Johns Hopkins University. Alice was enrolled at Johns Hopkins University and attending classes from August 29, 2015 to May 30th, 2019.


**Question:**
Section 3306(c)(10)(A)(ii) applies to Bob's employment situation in 2017.

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

The answer is exactly "Entailment" (the claim is true given the statute and facts) or "Contradiction" (the claim is false). E.g., `Answer: Entailment`

The task is complete once `swipl -q -f /app/solution.pl` runs without errors and prints the `Answer:` line.