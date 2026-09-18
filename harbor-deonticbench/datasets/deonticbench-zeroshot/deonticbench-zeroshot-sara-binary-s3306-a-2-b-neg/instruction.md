The relevant statute is available at `/app/statute.txt`.


**Case Facts:**
Alice has employed Bob, Cameron, Dan, Emily, Fred and George for agricultural labor on various occasions during the year 2017: - Jan 24: Bob, Cameron, Dan, Emily and Fred - Feb 4: Bob, Cameron and Fred - Mar 3: Bob, Cameron, Dan, Emily and Fred - Mar 18: Cameron, Dan, Emily, Fred and George - Apr 1: Bob, Cameron, Dan, Fred and George - May 9: Cameron, Dan, Emily, Fred and George - Oct 14: Bob, Cameron, Dan, Emily and George - Oct 25: Bob, Emily, Fred and George - Nov 8: Bob, Cameron, Emily, Fred and George - Nov 22: Bob, Cameron, Dan, Emily and Fred - Dec 1: Bob, Cameron, Dan, Emily and George - Dec 2: Bob, Cameron, Dan, Emily and George


**Question:**
Section 3306(a)(2)(B) applies to Alice for the year 2017.

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