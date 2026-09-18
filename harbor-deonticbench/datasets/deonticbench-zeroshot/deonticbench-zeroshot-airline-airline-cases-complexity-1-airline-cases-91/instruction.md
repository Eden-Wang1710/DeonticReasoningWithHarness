The relevant statute is available at `/app/statute.txt`.


**Case Facts:**
Patricia is a Business Class passenger flying from San Francisco to Wuhan with the following items: 1. A backpack: 21 x 13 x 8 inches, 9 lbs; 2. A luggage box: 37 x 12 x 14 inches, 54 lbs; 3. A luggage box: 36 x 14 x 14 inches, 53 lbs; 4. A backpack: 34 x 19 x 12 inches, 77 lbs; 5. A backpack: 52 x 34 x 28 inches, 59 lbs; 6. A backpack: 40 x 26 x 20 inches, 69 lbs; 7. A luggage box: 37 x 12 x 14 inches, 54 lbs; 8. A backpack: 52 x 33 x 26 inches, 57 lbs; Patricia's flight ticket is $1154.


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