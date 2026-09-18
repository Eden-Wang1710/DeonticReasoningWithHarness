The relevant statute is available at `/app/statute.txt`.


**Case Facts:**
Susan is a Business Class passenger flying from Minneapolis to Miami with the following items: 1. A backpack: 19 x 11 x 8 inches, 7 lbs; 2. A backpack: 44 x 32 x 20 inches, 51 lbs; 3. A backpack: 37 x 13 x 14 inches, 68 lbs; 4. A luggage box: 34 x 16 x 14 inches, 66 lbs; 5. A backpack: 49 x 32 x 23 inches, 96 lbs; Susan's flight ticket is $162.


**Question:**
What is the total cost (including the flight ticket fee, checked bag fees, cost of special needs) according to the policies for the passenger?

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

The answer is a whole number (total cost in dollars, no $ sign). E.g., `Answer: 1166`

The task is complete once `swipl -q -f /app/solution.pl` runs without errors and prints the `Answer:` line.