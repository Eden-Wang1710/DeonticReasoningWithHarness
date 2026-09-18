The relevant statute is available at `/app/statute.txt`.


**Case Facts:**
Jennifer is a Business Class passenger flying from San Francisco to New York with the following items: 1. A backpack: 19 x 13 x 8 inches, 10 lbs; 2. A backpack: 43 x 19 x 19 inches, 84 lbs; 3. A luggage box: 35 x 16 x 12 inches, 52 lbs; 4. A backpack: 50 x 28 x 25 inches, 52 lbs; 5. A backpack: 37 x 13 x 14 inches, 69 lbs; Jennifer's flight ticket is $159.


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